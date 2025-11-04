package oops_lab;

import java.util.*;

class Account {
    String custName;
    int accno;
    double balance;

    Account(String custName, int accno, double balance){
        this.custName = custName;
        this.accno = accno;
        this.balance = balance;
    }

    void viewBalance(){
        System.out.println("Balance: " + balance);
    }

    void withdraw(double amt){
        balance -= amt;
    }

    void deposit(double amt){
        balance += amt;
    }
}

class SavingsAccount extends Account {
    double interestRate = 0.06;

    SavingsAccount(String n, int a, double b){
        super(n,a,b);
    }

    void withdraw(double amt){
        if(balance < amt){
            System.out.println("Overdraw not allowed");
        } else {
            balance -= amt;
        }
    }

    void deposit(double amt){
        balance += amt + (amt * interestRate);
    }
}

class CurrentAccount extends Account {
    double serviceCharge = 0.035;

    CurrentAccount(String n, int a, double b){
        super(n,a,b);
    }

    void withdraw(double amt){
        double overdraw = amt - balance;
        balance -= amt;
        if(overdraw > 0){
            balance -= overdraw * serviceCharge;
        }
    }

    void deposit(double amt){
        balance += amt;
    }
}

public class BankDemo {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        Account ref;

        System.out.println("1. Savings Account");
        System.out.println("2. Current Account");
        System.out.print("Select Account Type: ");
        int ch = sc.nextInt();

        if(ch == 1){
            ref = new SavingsAccount("Jeffy",101,10000);
        } else {
            ref = new CurrentAccount("Jeffy",102,5000);
        }

        while(true){
            System.out.println("\n1. Deposit\n2. Withdraw\n3. View Balance\n4. Exit");
            System.out.print("Enter choice: ");
            int op = sc.nextInt();

            switch(op){
                case 1:
                    System.out.print("Enter amount: ");
                    ref.deposit(sc.nextDouble());
                    break;
                case 2:
                    System.out.print("Enter amount: ");
                    ref.withdraw(sc.nextDouble());
                    break;
                case 3:
                    ref.viewBalance();
                    break;
                case 4:
                    System.exit(0);
                default:
                    System.out.println("Invalid");
            }
        }
    }
}
