# DEP-2
%Task 2

#include <iostream>
#include <vector>
#include <string>

class Contact {
public:
    std::string name;
    std::string phoneNumber;

    Contact(std::string n, std::string p) : name(n), phoneNumber(p) {}
};

class ContactManager {
private:
    std::vector<Contact> contacts;

public:
    void addContact(const std::string& name, const std::string& phoneNumber) {
        contacts.emplace_back(name, phoneNumber);
        std::cout << "Contact added: " << name << " - " << phoneNumber << "\n";
    }

    void viewContacts() {
        if (contacts.empty()) {
            std::cout << "No contacts available.\n";
            return;
        }

        std::cout << "Contacts List:\n";
        for (size_t i = 0; i < contacts.size(); ++i) {
            std::cout << i + 1 << ". " << contacts[i].name << " - " << contacts[i].phoneNumber << "\n";
        }
    }

    void deleteContact(size_t index) {
        if (index < 1 || index > contacts.size()) {
            std::cout << "Invalid contact index.\n";
            return;
        }
        contacts.erase(contacts.begin() + index - 1);
        std::cout << "Contact deleted.\n";
    }
};

void showMenu() {
    std::cout << "\nContact Management System\n";
    std::cout << "1. Add Contact\n";
    std::cout << "2. View Contacts\n";
    std::cout << "3. Delete Contact\n";
    std::cout << "4. Exit\n";
}

int main() {
    ContactManager manager;
    int choice;
    std::string name, phoneNumber;

    while (true) {
        showMenu();
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1:
                std::cout << "Enter name: ";
                std::cin.ignore(); // Ignore the newline character
                std::getline(std::cin, name);
                std::cout << "Enter phone number: ";
                std::getline(std::cin, phoneNumber);
                manager.addContact(name, phoneNumber);
                break;
            case 2:
                manager.viewContacts();
                break;
            case 3:
                size_t index;
                std::cout << "Enter contact number to delete: ";
                std::cin >> index;
                manager.deleteContact(index);
                break;
            case 4:
                std::cout << "Exiting...\n";
                return 0;
            default:
                std::cout << "Invalid choice. Please try again.\n";
        }
    }
    return 0;
}

