# 1

import java.util.concurrent.*;

public class ThreadExample {

    public static void main(String[] args) {
        int num = 5; 
        Future<Integer> oddSeriesResult = executor.submit(() -> oddSeries(num));
        Future<Integer> squareResult = executor.submit(() -> square(num));
        Future<Integer> factorialResult = executor.submit(() -> fact(num));
        executor.shutdown();

        try {
            executor.awaitTermination(10, TimeUnit.SECONDS);
            int oddSum = oddSeriesResult.get();
            int squareNum = squareResult.get();
            int factorialNum = factorialResult.get();

            int finalAnswer = oddSum + squareNum + factorialNum;

            System.out.println("Final Answer: " + finalAnswer);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }

    public static int oddSeries(int num) {
        int sum = 0;
        for (int i = 1; i <= num; i += 2) {
            sum += i;
        }
        return sum;
    }

    public static int square(int num) {
        return num * num;
    }

    public static int fact(int num) {
        if (num == 0 || num == 1) {
            return 1;
        }
        int factorial = 1;
        for (int i = 2; i <= num; i++) {
            factorial *= i;
        }
        return factorial;
    }
}


===============================================================================

2

import java.util.Scanner;

class Employee {
    private int Eno;
    private String EmpName;
    private String Department;
    private String Designation;
    private double Salary;

    public Employee(int Eno, String EmpName, String Department, String Designation, double Salary) {
        this.Eno = Eno;
        this.EmpName = EmpName;
        this.Department = Department;
        this.Designation = Designation;
        this.Salary = Salary;
    }

    public void getData() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter Employee Number:");
        this.Eno = scanner.nextInt();
        scanner.nextLine(); 
        System.out.println("Enter Employee Name (Format: FirstName Middlename Surname):");
        this.EmpName = scanner.nextLine();
        System.out.println("Enter Department:");
        this.Department = scanner.nextLine();
        System.out.println("Enter Designation:");
        this.Designation = scanner.nextLine();
        System.out.println("Enter Salary:");
        this.Salary = scanner.nextDouble();
    }

   
    public void displayData() {
        System.out.println("\nEmployee Details:");
        System.out.println("Employee Number: " + Eno);
        System.out.println("Employee Name: " + EmpName.toUpperCase()); // Display name in upper case
        System.out.println("Department: " + Department);
        System.out.println("Designation: " + Designation);
        System.out.println("Salary: $" + Salary);
        
     
        double incentiveAmount = incentive();
        System.out.println("Incentive: $" + incentiveAmount);
        
       
        double totalSalary = Salary + incentiveAmount;
        System.out.println("Total Salary (including incentive): $" + totalSalary);
    }

    private double incentive() {
        double incentive = 0.0;

        if (EmpName.split(" ")[2].equalsIgnoreCase("Modi")) {
            incentive = 0.1 * Salary;
        }
        
        if (EmpName.split(" ")[0].equalsIgnoreCase("Ram")) {
            incentive = 0.15 * Salary;
        }
        
        if (EmpName.toLowerCase().contains("indra")) {
            incentive = 0.07 * Salary;
        }
        
        if (EmpName.length() > 7 && EmpName.charAt(7) == 'i') {
            incentive = 0.05 * Salary;
        }

        return incentive;
    }
}

public class EmployeeManagementSystem {
    public static void main(String[] args) {
        Employee employee = new Employee(0, "", "", "", 0.0);

        employee.getData();
        employee.displayData();
    }
}

