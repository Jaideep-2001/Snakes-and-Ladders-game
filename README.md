# Snakes-and-Ladders-game
sample code
import java.util.HashMap;
import java.util.Map;
import java.util.Random;
import java.util.Scanner;

public class SnakesAndLadders {
    // Define the game board as a HashMap
    private Map<Integer, Integer> board = new HashMap<>();
    private int currentPlayer = 1;
    private boolean gameOver = false;

    // Define the snakes and ladders as a HashMap
    private static final Map<Integer, Integer> snakesAndLadders = new HashMap<>();
    static {
        snakesAndLadders.put(4, 14);
        snakesAndLadders.put(9, 31);
        snakesAndLadders.put(17, 7);
        snakesAndLadders.put(20, 38);
        snakesAndLadders.put(28, 84);
        snakesAndLadders.put(40, 59);
        snakesAndLadders.put(51, 67);
        snakesAndLadders.put(54, 34);
        snakesAndLadders.put(62, 19);
        snakesAndLadders.put(63, 81);
        snakesAndLadders.put(64, 60);
        snakesAndLadders.put(71, 91);
        snakesAndLadders.put(87, 24);
        snakesAndLadders.put(93, 73);
        snakesAndLadders.put(95, 75);
        snakesAndLadders.put(99, 78);
    }

    // Constructor to initialize the game board
    public SnakesAndLadders() {
        for (int i = 1; i <= 100; i++) {
            board.put(i, i);
        }
        for (Map.Entry<Integer, Integer> entry : snakesAndLadders.entrySet()) {
            board.put(entry.getKey(), entry.getValue());
        }
    }

    // Method to roll the dice and move the current player
    public void rollDice() {
        Random rand = new Random();
        int roll = rand.nextInt(6) + 1;
        System.out.println("Player " + currentPlayer + " rolled a " + roll);

        int newPosition = board.get(currentPlayer) + roll;
        if (newPosition > 100) {
            newPosition = 100 - (newPosition - 100);
        }

        int oldPosition = board.get(currentPlayer);
        board.put(currentPlayer, newPosition);
        System.out.println("Player " + currentPlayer + " moved from " + oldPosition + " to " + newPosition);

        if (newPosition == 100) {
            System.out.println("Player " + currentPlayer + " wins!");
            gameOver = true;
        } else if (snakesAndLadders.containsKey(newPosition)) {
            int nextPosition = snakesAndLadders.get(newPosition);
            board.put(currentPlayer, nextPosition);
            System.out.println("Player " + currentPlayer + " climbed a ladder to " + nextPosition);
        }
    }

    // Method to switch to the next player
    public void nextPlayer() {
        if (currentPlayer == 1) {
            currentPlayer = 2;
        } else {
            currentPlayer = 1;
        }
    }

    // Method to run the game
    public void play() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to Snakes and Ladders!");

        while (!gameOver) {
            System.out.println("Player " + currentPlayer + "'s turn. Press enter to roll the dice.");
            scanner.nextLine();
            rollDice();
            nextPlayer();
        }

        scanner.close();
    }

    // Main method to start the game
    public static void main(String[] args
