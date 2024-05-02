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
