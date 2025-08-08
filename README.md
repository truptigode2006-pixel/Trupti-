#include <iostream>
using namespace std;

int n;

class bank {
public:
    int acc_no;
    int total_am = 0;
    string name;

    void accept_name();
    void display();
    void deposit();
    void withdraw();
};

void bank::accept_name() {
    cin.ignore();
    cout << "\nEnter the following details:\n";
    cout << "Enter the account holder's full name: ";
    getline(cin, name);
    cout << "Enter the account number: ";
    cin >> acc_no;
}

void bank::display() {
    cout << "\n--- Account Details ---\n";
    cout << "Name: " << name << "\n";
    cout << "Account Number: " << acc_no << "\n";
    cout << "Current Balance: " << total_am << "\n";
}

void bank::deposit() {
    int deposit_amo;
    cout << "\nEnter amount to deposit: ";
    cin >> deposit_amo;

    if (deposit_amo <= 0) {
        cout << "You can't deposit 0 or negative amount.\n";
    } else {
        total_am += deposit_amo;
        cout << "Deposit successful. New Balance: " << total_am << "\n";
    }
}

void bank::withdraw() {
    int withdraw_amo;
    cout << "\nEnter amount to withdraw: ";
    cin >> withdraw_amo;

    if (withdraw_amo > total_am) {
        cout << "Insufficient balance! Withdrawal failed.\n";
    } else {
        total_am -= withdraw_amo;
        cout << "Withdrawal successful. Remaining Balance: " << total_am << "\n";
    }
}

bank b[100];

int main() {
    int ch, i;
    cout << "Enter the number of people: ";
    cin >> n;

    do {
        cout << "\nMenu:\n";
        cout << "1. Accept details\n";
        cout << "2. Display details\n";
        cout << "3. Deposit amount\n";
        cout << "4. Withdraw amount\n";
        cout << "5. Search by account number\n";
        cout << "0. Exit\n";
        cout << "Enter your choice: ";
        cin >> ch;

        switch (ch) {
            case 1:
                for (i = 0; i < n; i++) {
                    cout << "\n--- Entering data for Person " << (i + 1) << " ---\n";
                    b[i].accept_name();
                }
                break;

            case 2:
                for (i = 0; i < n; i++) {
                    b[i].display();
                }
                break;

            case 3: {
                int acc_no_deposit;
                cout << "\nEnter account number to deposit into: ";
                cin >> acc_no_deposit;
                bool found = false;
                for (i = 0; i < n; i++) {
                    if (b[i].acc_no == acc_no_deposit) {
                        b[i].deposit();
                        found = true;
                        break;
                    }
                }
                if (!found)
                    cout << "Account not found.\n";
                break;
            }

            case 4: {
                int acc_no_withdraw;
                cout << "\nEnter account number to withdraw from: ";
                cin >> acc_no_withdraw;
                bool found = false;
                for (i = 0; i < n; i++) {
                    if (b[i].acc_no == acc_no_withdraw) {
                        b[i].withdraw();
                        found = true;
                        break;
                    }
                }
                if (!found)
                    cout << "Account not found.\n";
                break;
            }

            case 5: {
                int num;
                cout << "\nEnter the account number for searching: ";
                cin >> num;
                bool found = false;
                for (i = 0; i < n; i++) {
                    if (b[i].acc_no == num) {
                        cout << "Person found.\n";
                        b[i].display();
                        found = true;
                        break;
                    }
                }
                if (!found)
                    cout << "Account not found.\n";
                break;
            }

            case 0:
                cout << "Exiting the program.\n";
                break;

            default:
                cout << "Invalid choice. Please enter 0 to 5.\n";
        }

    } while (ch != 0);

    return 0;
}
