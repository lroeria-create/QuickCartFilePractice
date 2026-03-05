# QuickCartFilePractice
Coursera-Practice
Hello Everyone

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package motorph.quickcartfilepractice;

/**
 *
 * @author HP
 */
import java.io.FileReader;
import java.io.BufferedReader;
import java.io.FileWriter;
import java.io.BufferedWriter;
import java.io.IOException;
import java.util.ArrayList;

public class QuickCartFilePractice {

    // Read items from items.txt
    public static ArrayList<String> readItemsFromFile() {

        ArrayList<String> items = new ArrayList<>();

        try {

            BufferedReader reader = new BufferedReader(new FileReader("items.txt"));
            String line;

            while ((line = reader.readLine()) != null) {

                items.add(line);

            }

            reader.close();

        } catch (IOException e) {

            System.out.println("Error reading items.txt");

        }

        return items;
    }

    // Write receipt to receipt.txt
    public static void writeReceiptToFile(String message) {

        try {

            BufferedWriter writer = new BufferedWriter(new FileWriter("receipt.txt"));

            writer.write(message);

            writer.close();

            System.out.println("Receipt successfully written to receipt.txt");

        } catch (IOException e) {

            System.out.println("Error writing receipt.txt");

        }

    }

    // Extract price from line like "Milk,80"
    public static double parsePrice(String line) {

        String[] parts = line.split(",");

        return Double.parseDouble(parts[1]);

    }

    // Discount method
    public static double applyDiscount(double total) {

        double discount = 0;

        if (total > 1000) {

            discount = total * 0.10; // 10%

        } else if (total > 500) {

            discount = total * 0.05; // 5%

        }

        return total - discount;

    }

    public static void main(String[] args) {

        ArrayList<String> items = readItemsFromFile();

        double subtotal = 0;

        String receiptItems = "";

        System.out.println("Checkout Summary:");

        for (String item : items) {

            double price = parsePrice(item);

            System.out.println(item);

            subtotal += price;

            // Split item name and price
            String[] parts = item.split(",");

            receiptItems += parts[0] + " - " + parts[1] + "\n";

        }

        double finalTotal = applyDiscount(subtotal);

        double discount = subtotal - finalTotal;

        System.out.println("Subtotal: " + subtotal);
        System.out.println("Discount: " + discount);
        System.out.println("Final Total: " + finalTotal);

        // Receipt format
        String receipt =
                """
                QuickCart Receipt
                -----------------------
                Items Purchased:
                """
                + receiptItems + "\n"
                + "Subtotal: " + subtotal + "\n"
                + "Discount: " + discount + "\n"
                + "Final Total: " + finalTotal + "\n";

        writeReceiptToFile(receipt);
    }
}

