import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Contact {
    private String name;
    private String phoneNumber;
    private String email;

    public Contact(String name, String phoneNumber, String email) {
        this.name = name;
        this.phoneNumber = phoneNumber;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "Name: " + name + ", Phone: " + phoneNumber + ", Email: " + email;
    }
}

class AddressBook {
    private List<Contact> contacts;

    public AddressBook() {
        contacts = new ArrayList<>();
    }

    public void addContact(Contact contact) {
        contacts.add(contact);
    }

    public void viewContacts() {
        if (contacts.isEmpty()) {
            System.out.println("No contacts in the address book.");
        } else {
            for (Contact contact : contacts) {
                System.out.println(contact);
            }
        }
    }

    public Contact searchContactByName(String name) {
        for (Contact contact : contacts) {
            if (contact.getName().equalsIgnoreCase(name)) {
                return contact;
            }
        }
        return null; 
    }
}

interface Menu {
    void showMenu();
}

class AddressBookMenu implements Menu {
    private AddressBook addressBook;
    private Scanner scanner;

    public AddressBookMenu() {
        addressBook = new AddressBook();
        scanner = new Scanner(System.in);
    }

    public void showMenu() {
        int choice;
        do {
            System.out.println("\nAddress Book Menu:");
            System.out.println("1. Add a new contact");
            System.out.println("2. View all contacts");
            System.out.println("3. Search for a contact by name");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine();
            switch (choice) {
                case 1:
                    addNewContact();
                    break;
                case 2:
                    addressBook.viewContacts();
                    break;
                case 3:
                    searchContact();
                    break;
                case 4:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);
    }

    private void addNewContact() {
        System.out.print("Enter name: ");
        String name = scanner.nextLine();
        System.out.print("Enter phone number: ");
        String phoneNumber = scanner.nextLine();
        System.out.print("Enter email address: ");
        String email = scanner.nextLine();

        Contact contact = new Contact(name, phoneNumber, email);
        addressBook.addContact(contact);
        System.out.println("Contact added successfully.");
    }

    private void searchContact() {
        System.out.print("Enter the name to search: ");
        String name = scanner.nextLine();
        Contact contact = addressBook.searchContactByName(name);
        if (contact != null) {
            System.out.println("Contact found: " + contact);
        } else {
            System.out.println("Contact not found.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        AddressBookMenu menu = new AddressBookMenu();
        menu.showMenu();
    }
}
