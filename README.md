import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.Scanner;

public class MemoryGame {

    public static void main(String[] args) {
        String[] cards = {"A", "A", "B", "B", "C", "C", "D", "D"};
        List<String> cardList = Arrays.asList(cards);
        Collections.shuffle(cardList);

        String[] board = new String[cards.length];
        Arrays.fill(board, "*");

        Scanner scanner = new Scanner(System.in);
        int guesses = 0;
        int pairsFound = 0;

        while (pairsFound < cards.length / 2) {
            printBoard(board);
            System.out.print("Enter first card index (0-" + (cards.length - 1) + "): ");
            int index1 = scanner.nextInt();
            System.out.print("Enter second card index (0-" + (cards.length - 1) + "): ");
            int index2 = scanner.nextInt();

            if (index1 == index2 || !board[index1].equals("*") || !board[index2].equals("*")) {
                System.out.println("Invalid choice. Try again.");
            } else {
                guesses++;
                board[index1] = cardList.get(index1);
                board[index2] = cardList.get(index2);

                if (board[index1].equals(board[index2])) {
                    pairsFound++;
                    System.out.println("Match found!");
                } else {
                    System.out.println("No match.");
                    board[index1] = "*";
                    board[index2] = "*";
                }
            }
        }

        System.out.println("You won in " + guesses + " guesses!");
        scanner.close();
    }

    private static void printBoard(String[] board) {
        for (String card : board) {
            System.out.print(card + " ");
        }
        System.out.println();
    }
}
