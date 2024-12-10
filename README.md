#include <iostream>
#include <vector>
#include <string>

struct Task {
    std::string description;
    bool isCompleted;

    Task(std::string desc) : description(desc), isCompleted(false) {}
};

void displayMenu() {
    std::cout << "\nTo-Do List Manager\n";
    std::cout << "1. Add Task\n";
    std::cout << "2. View Tasks\n";
    std::cout << "3. Mark Task as Completed\n";
    std::cout << "4. Remove Task\n";
    std::cout << "5. Exit\n";
    std::cout << "Choose an option: ";
}

void addTask(std::vector<Task>& tasks) {
    std::cout << "Enter task description: ";
    std::string description;
    std::cin.ignore();
    std::getline(std::cin, description);
    tasks.emplace_back(description);
    std::cout << "Task added successfully.\n";
}

void viewTasks(const std::vector<Task>& tasks) {
    if (tasks.empty()) {
        std::cout << "No tasks available.\n";
        return;
    }
    std::cout << "\nTasks:\n";
    for (size_t i = 0; i < tasks.size(); ++i) {
        std::cout << i + 1 << ". " << tasks[i].description
                  << " [" << (tasks[i].isCompleted ? "Completed" : "Pending") << "]\n";
    }
}

void markTaskAsCompleted(std::vector<Task>& tasks) {
    if (tasks.empty()) {
        std::cout << "No tasks available to mark as completed.\n";
        return;
    }
    viewTasks(tasks);
    std::cout << "Enter the task number to mark as completed: ";
    int taskNumber;
    std::cin >> taskNumber;
    if (taskNumber < 1 || taskNumber > tasks.size()) {
        std::cout << "Invalid task number.\n";
    } else {
        tasks[taskNumber - 1].isCompleted = true;
        std::cout << "Task marked as completed.\n";
    }
}
void removeTask(std::vector<Task>& tasks) {
    if (tasks.empty()) {
        std::cout << "No tasks available to remove.\n";
        return;
    }
    viewTasks(tasks);
    std::cout << "Enter the task number to remove: ";
    int taskNumber;
    std::cin >> taskNumber;
    if (taskNumber < 1 || taskNumber > tasks.size()) {
        std::cout << "Invalid task number.\n";
    } else {
        tasks.erase(tasks.begin() + taskNumber - 1);
        std::cout << "Task removed successfully.\n";
    }
}
int main() {
    std::vector<Task> tasks;
    int choice;
    do {
        displayMenu();
        std::cin >> choice;
        switch (choice) {
            case 1:
                addTask(tasks);
                break;
            case 2:
                viewTasks(tasks);
                break;
            case 3:
                markTaskAsCompleted(tasks);
                break;
            case 4:
                removeTask(tasks);
                break;
            case 5:
                std::cout << "Exiting program. Goodbye!\n";
                break;
            default:
                std::cout << "Invalid option. Please try again.\n";
        }
    } while (choice != 5);
    return 0;
}
