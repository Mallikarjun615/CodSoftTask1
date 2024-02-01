import java.util.Random;
import java.util.Scanner;

public class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        int minRange = 1;
        int maxRange = 100;
        int maxAttempts = 10;
        int score = 0;

        System.out.println("Welcome to the Number Guessing Game!");

        do {
            int targetNumber = getRandomNumber(minRange, maxRange);
            int attempts = 0;
            boolean guessedCorrectly = false;

            System.out.println("\nI've selected a number between " + minRange + " and " + maxRange + ". Try to guess it!");

            while (attempts < maxAttempts) {
                System.out.print("Enter your guess: ");
                int userGuess = scanner.nextInt();
                attempts++;

                if (userGuess == targetNumber) {
                    System.out.println("Congratulations! You guessed the correct number in " + attempts + " attempts.");
                    guessedCorrectly = true;
                    break;
                } else if (userGuess < targetNumber) {
                    System.out.println("Too low. Try again.");
                } else {
                    System.out.println("Too high. Try again.");
                }
            }

            if (!guessedCorrectly) {
                System.out.println("Sorry! You've reached the maximum number of attempts. The correct number was: " + targetNumber);
            }

            score += guessedCorrectly ? 1 : 0;

            System.out.print("\nDo you want to play again? (yes/no): ");
        } while (scanner.next().equalsIgnoreCase("yes"));

        System.out.println("\nThanks for playing! Your total score is: " + score);

        // Close the scanner to prevent resource leak
        scanner.close();
    }

    private static int getRandomNumber(int min, int max) {
        return new Random().nextInt(max - min + 1) + min;
    }
}
