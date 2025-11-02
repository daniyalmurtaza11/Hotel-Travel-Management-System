#include <iostream>
#include <string>
using namespace std;
class Hotel {
private:
    int roomNumber[10];
    int isBooked[10];         
    string guestName[10];
    int roomPrice[10];        
public:
    Hotel() {
        for (int i = 0; i < 10; i++) {
            roomNumber[i] = i + 1;
            isBooked[i] = 0; 
            guestName[i] = "None";

            if (i < 5)
                roomPrice[i] = 3000;  
            else
                roomPrice[i] = 5000;  
        }
    }

    void showRooms() {
        cout << "\n--- All Rooms ---\n";
        for (int i = 0; i < 10; i++) {
            cout << "Room " << roomNumber[i]
                 << " | Floor " << (i < 5 ? 1 : 2)
                 << " | Price: Rs." << roomPrice[i]
                 << " | Status: " << (isBooked[i] == 1 ? "Booked by " + guestName[i] : "Available")
                 << endl;
        }
    }

    void showFloorRooms(int floor) {
        cout << "\n--- Floor " << floor << " Rooms ---\n";
        int start = (floor == 1) ? 0 : 5;
        int end = (floor == 1) ? 5 : 10;

        for (int i = start; i < end; i++) {
            cout << "Room " << roomNumber[i]
                 << " | Price: Rs." << roomPrice[i]
                 << " | Status: " << (isBooked[i] == 1 ? "Booked by " + guestName[i] : "Available")
                 << endl;
        }
    }

    void bookRoom(string name) {
        int floor;
        cout << "\nSelect floor (1 or 2): ";
        cin >> floor;

        if (floor != 1 && floor != 2) {
            cout << "? Invalid floor number.\n";
            return;
        }
        showFloorRooms(floor);

        int choice;
        cout << "\nEnter room number to book: ";
        cin >> choice;

        if (choice < 1 || choice > 10) {
            cout << "? Invalid room number.\n";
            return;
        }

        int index = choice - 1;
        if (isBooked[index] == 0) {
            isBooked[index] = 1;
            guestName[index] = name;
            cout << "? Room " << choice << " booked successfully by " << name << "!\n";
        } else {
            cout << "? Room already booked!\n";
        }
    }

    void viewBookings() {
        cout << "\n--- Current Hotel Bookings ---\n";
        int any = 0;
        for (int i = 0; i < 10; i++) {
            if (isBooked[i] == 1) {
                cout << "Room " << roomNumber[i]
                     << " (Floor " << (i < 5 ? 1 : 2) << ") - Rs." << roomPrice[i]
                     << " booked by " << guestName[i] << endl;
                any = 1;
            }
        }
        if (any == 0)
            cout << "No rooms booked yet.\n";
    }
};
class Travel {
private:
    string packageNames[3] = {"City Tour", "Mountain Trip", "Desert Safari"};
    int packagePrice[3] = {5000, 10000, 7000};
    int isPackageBooked[3] = {0, 0, 0};
    string bookedBy[3];

public:
    void showPackages() {
        cout << "\n--- Travel Packages ---\n";
        for (int i = 0; i < 3; i++) {
            cout << i + 1 << ". " << packageNames[i]
                 << " - Rs." << packagePrice[i]
                 << " - " << (isPackageBooked[i] == 1 ? "Booked by " + bookedBy[i] : "Available") << endl;
        }
    }

    void bookPackage(string name) {
        showPackages();
        int choice;
        cout << "\nEnter package number to book: ";
        cin >> choice;

        if (choice < 1 || choice > 3) {
            cout << "? Invalid choice.\n";
            return;
        }

        int index = choice - 1;
        if (isPackageBooked[index] == 0) {
            isPackageBooked[index] = 1;
            bookedBy[index] = name;
            cout << "? Package \"" << packageNames[index] << "\" booked successfully by " << name << "!\n";
        } else {
            cout << "? Package already booked!\n";
        }
    }

    void viewBookedPackages() {
        cout << "\n--- Booked Travel Packages ---\n";
        int any = 0;
        for (int i = 0; i < 3; i++) {
            if (isPackageBooked[i] == 1) {
                cout << packageNames[i] << " booked by " << bookedBy[i] << endl;
                any = 1;
            }
        }
        if (any == 0)
            cout << "No packages booked yet.\n";
    }
};
class ManagementSystem {
private:
    Hotel hotel;
    Travel travel;

public:
    void menu() {
        int choice;
        string name;

        cout << "OWNER : DANIYAL MURTAZA "<<endl;
        cout<< " Email : daniyalmurtaza1122@gmail.com"<<endl;
        cout<<" For Custom made Touarism Package Contact the number given Below: "<<endl;
        cout<<"      03263345020  "<<endl;
        cout << "   HOTEL & TRAVEL MANAGEMENT SYSTEM "<<endl;
        

        while (true) {
            cout << "\nMain Menu:\n";
            cout << "1. Hotel Services\n";
            cout << "2. Travel Services\n";
            cout << "3. Exit\n";
            cout << "Please Make your choice: ";
            cin >> choice;

            if (choice == 1)
                hotelMenu();
            else if (choice == 2)
                travelMenu();
            else if (choice == 3) {
                cout << "Thank you for using our system. Have a nice Day ahead!\n";
                break;
            } else
                cout << "The choice you have made is Invalid!Please Try again.\n";
        }
    }
    void hotelMenu() {
        int choice;
        string name;

        while (true) {
            cout << "\n--- Hotel Menu ---\n";
            cout << "1. View All Rooms\n";
            cout << "2. View Floor Rooms\n";
            cout << "3. Book a Room\n";
            cout << "4. View Bookings\n";
            cout << "5. Back to Main Menu\n";
            cout << "Enter your choice: ";
            cin >> choice;

            if (choice == 1)
                hotel.showRooms();
            else if (choice == 2) {
                int floor;
                cout << "Enter floor (1 or 2): ";
                cin >> floor;
                hotel.showFloorRooms(floor);
            } else if (choice == 3) {
                cout << "Enter your name: ";
                cin >> name;
                hotel.bookRoom(name);
            } else if (choice == 4)
                hotel.viewBookings();
            else if (choice == 5)
                break;
            else
                cout << "Invalid choice! Try again.\n";
        }
    }

    void travelMenu() {
        int choice;
        string name;

        while (true) {
            cout << "\n--- Travel Menu ---\n";
            cout << "1. View Packages\n";
            cout << "2. Book a Package\n";
            cout << "3. View Booked Packages\n";
            cout << "4. Back to Main Menu\n";
            cout << "Enter your choice: ";
            cin >> choice;

            if (choice == 1)
                travel.showPackages();
            else if (choice == 2) {
                cout << "Enter your name: ";
                cin >> name;
                travel.bookPackage(name);
            } else if (choice == 3)
                travel.viewBookedPackages();
            else if (choice == 4)
                break;
            else
                cout << "Invalid choice! Try again.\n";
        }
    }
};
int main() {
    ManagementSystem system;
    system.menu();
    return 0;
}

