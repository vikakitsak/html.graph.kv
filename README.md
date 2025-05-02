import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;
import javafx.collections.*;

public class CleaningScheduleApp extends Application {

    public static class ScheduleEntry {
        private final String date;
        private final String room;
        private final CheckBox done;

        public ScheduleEntry(String date, String room, boolean isDone) {
            this.date = date;
            this.room = room;
            this.done = new CheckBox();
            this.done.setSelected(isDone);
            // Збереження статусу в пам'ять можна реалізувати через Preferences API
        }

        public String getDate() { return date; }
        public String getRoom() { return room; }
        public CheckBox getDone() { return done; }
    }

    @Override
    public void start(Stage primaryStage) {
        TableView<ScheduleEntry> table = new TableView<>();

        TableColumn<ScheduleEntry, String> dateCol = new TableColumn<>("Дата");
        dateCol.setCellValueFactory(cellData -> new ReadOnlyStringWrapper(cellData.getValue().getDate()));

        TableColumn<ScheduleEntry, String> roomCol = new TableColumn<>("Черга кімнати");
        roomCol.setCellValueFactory(cellData -> new ReadOnlyStringWrapper(cellData.getValue().getRoom()));

        TableColumn<ScheduleEntry, CheckBox> doneCol = new TableColumn<>("Позначено виконаним");
        doneCol.setCellValueFactory(cellData -> new ReadOnlyObjectWrapper<>(cellData.getValue().getDone()));

        table.getColumns().addAll(dateCol, roomCol, doneCol);

        ObservableList<ScheduleEntry> data = FXCollections.observableArrayList(
            new ScheduleEntry("3 травня", "2 кім.", false),
            new ScheduleEntry("5 травня", "1 кім.", false),
            new ScheduleEntry("7 травня", "2 кім.", false),
            new ScheduleEntry("9 травня", "1 кім.", false),
            new ScheduleEntry("11 травня", "2 кім.", false),
            new ScheduleEntry("13 травня", "1 кім.", false),
            new ScheduleEntry("15 травня", "2 кім.", false),
            new ScheduleEntry("17 травня", "1 кім.", false),
            new ScheduleEntry("19 травня", "2 кім.", false),
            new ScheduleEntry("21 травня", "1 кім.", false),
            new ScheduleEntry("23 травня", "2 кім.", false),
            new ScheduleEntry("25 травня", "1 кім.", false),
            new ScheduleEntry("27 травня", "2 кім.", false),
            new ScheduleEntry("29 травня", "1 кім.", false),
            new ScheduleEntry("31 травня", "2 кім.", false)
        );

        table.setItems(data);

        VBox root = new VBox(table);
        Scene scene = new Scene(root, 600, 500);

        primaryStage.setTitle("Графік прибирання (травень 2025)");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
