# Bank-Management-System
# Bank Management System – Mini Project (Java)


import java.util.*;

class BankAccount {
    private String accountHolderName;
    private String accountNumber;
    private double balance;

    public BankAccount(String accountHolderName, String accountNumber, double initialBalance) {
        this.accountHolderName = accountHolderName;
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public String getAccountHolderName() {
        return accountHolderName;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: ₹" + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrew: ₹" + amount);
        } else {
            System.out.println("Invalid or insufficient balance.");
        }
    }

    public void displayDetails() {
        System.out.println("\nAccount Holder: " + accountHolderName);
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Balance: ₹" + balance);
    }
}

public class BankManagementSystem {
    private static Map<String, BankAccount> accounts = new HashMap<>();
    private static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        // 🎉 Welcome Message with Your Name
        System.out.println("==================================");
        System.out.println("  Welcome to the Bank Management System");
        System.out.println("        Created by: Souvik Saha");
        System.out.println("==================================");

        int choice;
        do {
            System.out.println("\n=== BANK MANAGEMENT MENU ===");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Check Balance");
            System.out.println("5. Display All Accounts");
            System.out.println("6. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1 -> createAccount();
                case 2 -> depositMoney();
                case 3 -> withdrawMoney();
                case 4 -> checkBalance();
                case 5 -> displayAllAccounts();
                case 6 -> System.out.println("Exiting... Thank you!");
                default -> System.out.println("Invalid choice! Please try again.");
            }
        } while (choice != 6);
    }

    private static void createAccount() {
        sc.nextLine(); // consume newline
        System.out.print("Enter account holder name: ");
        String name = sc.nextLine();
        System.out.print("Enter account number: ");
        String accNumber = sc.nextLine();
        System.out.print("Enter initial deposit amount: ");
        double amount = sc.nextDouble();

        BankAccount account = new BankAccount(name, accNumber, amount);
        accounts.put(accNumber, account);
        System.out.println("Account created successfully!");
    }

    private static void depositMoney() {
        System.out.print("Enter account number: ");
        String accNumber = sc.next();
        BankAccount account = accounts.get(accNumber);

        if (account != null) {
            System.out.print("Enter deposit amount: ");
            double amount = sc.nextDouble();
            account.deposit(amount);
        } else {
            System.out.println("Account not found!");
        }
    }

    private static void withdrawMoney() {
        System.out.print("Enter account number: ");
        String accNumber = sc.next();
        BankAccount account = accounts.get(accNumber);

        if (account != null) {
            System.out.print("Enter withdrawal amount: ");
            double amount = sc.nextDouble();
            account.withdraw(amount);
        } else {
            System.out.println("Account not found!");
        }
    }

    private static void checkBalance() {
        System.out.print("Enter account number: ");
        String accNumber = sc.next();
        BankAccount account = accounts.get(accNumber);

        if (account != null) {
            System.out.println("Current Balance: ₹" + account.getBalance());
        } else {
            System.out.println("Account not found!");
        }
    }

    private static void displayAllAccounts() {
        if (accounts.isEmpty()) {
            System.out.println("No accounts found!");
        } else {
            for (BankAccount account : accounts.values()) {
                account.displayDetails();
                System.out.println("---------------------");
            }
        }
    }
}

