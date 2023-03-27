import java.util.*;

class BankAccount {
    int balance;
    int prevTransaction;
    String customerName;
    String customerId;
    int flag = 0;


    BankAccount(String cName, String cId) {
        customerName = cName;
        customerId = cId;
    }


    void checkId() {

        System.out.println("Welcome " + customerName);
        System.out.println();
        System.out.print("Please enter the Customer ID or PIN: ");
        Scanner id = new Scanner(System.in);
        String chk = id.nextLine();
        if (chk.equals(customerId)) {

            showMenu();
        } else {
            System.out.println("=================================");
            System.out.println("Wrong Login!!");
            System.out.println("=================================");

            if (flag < 3) {
                flag++;
                checkId();
            }
        }
    }

    void deposit(int amount) {
        if (amount != 0) {
            balance = balance + amount;
            prevTransaction = amount;
        }
    }

    void withdraw(int amount) {
        if (this.balance > amount) {
            balance = balance - amount;
            prevTransaction = -amount;
        } else {

            System.out.println("=================================");
            System.out.println("Sufficient Balance not available for the withdrawl!");
            System.out.println("=================================");
        }
    }

    void getPrevTransaction() {
        if (prevTransaction > 0) {
            System.out.println("Deposited: " + prevTransaction);
        } else if (prevTransaction < 0) {
            System.out.println("Withdraw: " + Math.abs(prevTransaction));
        } else {
            System.out.println("No Transaction Occured ");
        }
    }

    public void transfer(double amount, BankAccount acc) {
        if (this.balance < amount) {

            System.out.println("=================================");
            System.out.println("Transfer Fails due to insufficient balance!");
            System.out.println("=================================");
        } else {
            this.balance -= amount;
            acc.balance += amount;
            System.out.println("Account of " + this.customerName + " becomes $" + this.balance);
            System.out.println("Account of " + acc.customerName + " becomes $" + acc.balance);
            System.out.println("\n");
        }
    }

    private void showMenu() {
        char option;
        Scanner sc = new Scanner(System.in);
        System.out.println("Welcome " + customerName);
        System.out.println("Your ID is  " + customerId);
        do {
            System.out.println();
            System.out.println();
            System.out.println("A. Check Balance");
            System.out.println("B. Deposit");
            System.out.println("C. Withdraw");
            System.out.println("D. Previous Transaction");
            System.out.println("E. Transfer");
            System.out.println("F. Exit");

            System.out.println("=================================");
            System.out.println("Enter the option");
            System.out.println("=================================");
            option = sc.next().charAt(0);
            option = Character.toUpperCase(option);
            System.out.println();

            switch (option) {
                case 'A' -> {
                    System.out.println("***************");
                    System.out.println("Balance " + balance);
                    System.out.println("******************");
                    System.out.println();
                }
                case 'B' -> {
                    System.out.println("***************");
                    System.out.println("Enter the amount to deposit");
                    System.out.println("***************");
                    int amount = sc.nextInt();
                    deposit(amount);
                    System.out.println();
                }
                case 'C' -> {
                    System.out.println("***************");
                    System.out.println("Enter the amount to withdraw");
                    System.out.println("*************");
                    int amount2 = sc.nextInt();
                    withdraw(amount2);
                    System.out.println();
                }
                case 'D' -> {
                    System.out.println("*****************");
                    getPrevTransaction();
                    System.out.println("**********************");
                    System.out.println();
                }
                case 'E' -> {
                    System.out.println("***************");
                    System.out.println("To whom");
                    BankAccount bb = new BankAccount("Raj", "1002");
                    System.out.println(bb.customerName);
                    System.out.println("***************");
                    System.out.println("Amount to Transfer");
                    double am = sc.nextDouble();
                    System.out.println("***************");
                    transfer(am, bb);
                }
                case 'F' -> System.out.println("***************");
                default -> System.out.println("Invalid Option!!! Please Enter Again");
            }

        } while (option != 'F');
        System.out.println("ThankYou For using our services");

    }


    public class ATMinterface {
        public static void main(String[] args) {
            BankAccount ba = new BankAccount("Shiva", "1000");
            ba.checkId();
        }

    }
}

