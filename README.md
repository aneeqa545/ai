#include <iostream>
#include <queue>
#include <vector>

class Patient {
public:
    int age;
    std::string name;

    Patient(std::string n, int a) : name(n), age(a) {}

    bool operator<(const Patient& p) const {
        return getPriority(age) < getPriority(p.age);
    }

private:
    static int getPriority(int age) {
        if (age >= 60)
            return 1;
        else if (age > 50)
            return 2;
        else if (age > 40)
            return 3;
        else if (age > 30)
            return 4;
        else
            return 5;
    }
};

class PatientQueue {
private:
    std::priority_queue<Patient> pq;

public:
    void addPatient(const Patient& p) {
        pq.push(p);
    }

    void removePatient() {
        if (!pq.empty()) {
            pq.pop();
            std::cout << "Patient removed successfully." << std::endl;
        } else {
            std::cout << "No patients in the queue." << std::endl;
        }
    }

    void displayPatients() {
        if (pq.empty()) {
            std::cout << "No patients in the queue." << std::endl;
            return;
        }

        // Copy the priority queue to a temporary queue to display patients
        std::priority_queue<Patient> temp = pq;

        std::cout << "Patients in the queue:" << std::endl;
        while (!temp.empty()) {
            Patient p = temp.top();
            std::cout << "Name: " << p.name << ", Age: " << p.age << std::endl;
            temp.pop();
        }
    }
};

int main() {
    PatientQueue pq;
    int choice;
    std::string name;
    int age;

    while (true) {
        std::cout << "\nHospital Patient Management System" << std::endl;
        std::cout << "1. Enter patient details" << std::endl;
        std::cout << "2. Remove a patient" << std::endl;
        std::cout << "3. Display patients" << std::endl;
        std::cout << "4. Exit" << std::endl;
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1:
                std::cout << "Enter patient's name: ";
                std::cin.ignore();
                std::getline(std::cin, name);
                std::cout << "Enter patient's age: ";
                std::cin >> age;
                pq.addPatient(Patient(name, age));
                break;
            case 2:
                pq.removePatient();
                break;
            case 3:
                pq.displayPatients();
                break;
            case 4:
                std::cout << "Exiting program." << std::endl;
                return 0;
            default:
                std::cout << "Invalid choice. Please try again." << std::endl;
        }
    }
    return 0;
}
