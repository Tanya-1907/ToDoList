import java.util.ArrayList;
import java.util.Scanner;

// Class to represent a Task
class Task {
    String description;      // Task details
    boolean isCompleted;     // Completion status

    // Constructor to initialize a new task
    Task(String description) {
        this.description = description;
        this.isCompleted = false;
    }

    // Mark the task as complete
    void markAsCompleted() {
        isCompleted = true;
    }

    // Represent the task as a string
    @Override
    public String toString() {
        return (isCompleted ? "[✔] " : "[ ] ") + description;
    }
}

// Main class containing the application logic
public class ToDoListApp {
    // Data structure to store tasks
    static ArrayList<Task> tasks = new ArrayList<>();
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int choice;

        // Main menu loop
        do {
            System.out.println("\n====== TO-DO LIST MENU ======");
            System.out.println("1. Add Task");
            System.out.println("2. Delete Task");
            System.out.println("3. Display Tasks");
            System.out.println("4. Mark Task as Completed");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            // Handle user choice
            switch (choice) {
                case 1 -> addTask();
                case 2 -> deleteTask();
                case 3 -> displayTasks();
                case 4 -> markTaskAsComplete();
                case 5 -> System.out.println("Exiting the app. Goodbye!");
                default -> System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 5);
    }

    // Method to add a new task
    static void addTask() {
        System.out.print("Enter task description: ");
        String desc = scanner.nextLine();
        tasks.add(new Task(desc));
        System.out.println("Task added.");
    }

    // Method to delete a task
    static void deleteTask() {
        displayTasks();
        System.out.print("Enter task number to delete: ");
        int index = scanner.nextInt();
        if (index >= 1 && index <= tasks.size()) {
            tasks.remove(index - 1);
            System.out.println("Task deleted.");
        } else {
            System.out.println("Invalid task number.");
        }
    }

    // Method to display all tasks
    static void displayTasks() {
        if (tasks.isEmpty()) {
            System.out.println("No tasks to display.");
            return;
        }
        System.out.println("\n--- TO-DO LIST ---");
        int i = 1;
        for (Task task : tasks) {
            System.out.println(i + ". " + task);
            i++;
        }
    }

    // Method to mark a task as completed
    static void markTaskAsComplete() {
        displayTasks();
        System.out.print("Enter task number to mark as complete: ");
        int index = scanner.nextInt();
        if (index >= 1 && index <= tasks.size()) {
            tasks.get(index - 1).markAsCompleted();
            System.out.println("Task marked as completed.");
        } else {
            System.out.println("Invalid task number.");
        }
    }
}

