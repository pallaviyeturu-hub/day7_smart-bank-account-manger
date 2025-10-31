# day7_smart-bank-account-manger
In this  program smark bank account manger by using this program we will check deposit money,bank balance,withdraw money 
#include <stdio.h>

int main() {
    int choice;
    long long balance = 10000LL;
    long long amount;
    long long bonus;

    // welcome (optional)
    // printf("Welcome to Smart Bank Account Manager\n");

    do {
        printf("\n1. Deposit Money\n");
        printf("2. Withdraw Money\n");
        printf("3. Check Balance\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        if (scanf("%d", &choice) != 1) {
            // invalid input: clear stdin and continue
            int c;
            while ((c = getchar()) != '\n' && c != EOF) {}
            choice = 0;
        }

        if (choice == 1) {
            printf("Enter amount to deposit: ");
            if (scanf("%lld", &amount) != 1) { amount = 0; }
            bonus = 0;
            if (amount > 25000) {
                bonus = amount / 100; // 1% bonus
                printf("Bonus of \u20B9%lld added!\n", bonus);
            }
            balance = balance + amount + bonus;
            // service charge for successful transaction
            balance -= 5;
            printf("Service charge \u20B95 applied.\n");
            printf("Updated Balance: \u20B9%lld\n", balance);
        }
        else if (choice == 2) {
            printf("Enter amount to withdraw: ");
            if (scanf("%lld", &amount) != 1) { amount = 0; }
            if (amount > balance) {
                printf("Withdrawal not allowed! Insufficient balance.\n");
            } else {
                balance -= amount;
                balance -= 5; // service charge
                printf("Service charge \u20B95 applied.\n");
                printf("Updated Balance: \u20B9%lld\n", balance);
            }
        }
        else if (choice == 3) {
            printf("Current Balance: \u20B9%lld\n", balance);
        }
        else if (choice == 4) {
            printf("Thank you for banking with us!\n");
        }
        else {
            if (choice != 0) // ignore when scanf failed
                printf("Invalid choice! Please try again.\n");
        }

        // clear newline leftover before next loop iteration (safe)
        int ch;
        while ((ch = getchar()) != '\n' && ch != EOF) {}

    } while (choice != 4);

    return 0;
}
