package praktikum;

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Anggoro Nur Arifin - 20230801135
// Praktikum Pemrograman Berorientasi Objek

public class program {
    private static List<String> history = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String continueCalculation = "y";

        while (continueCalculation.equalsIgnoreCase("y")) {
            clearScreen();

            System.out.println("Kalkulator 2 Angka Sederhana dengan Riwayat dan Presisi");
            System.out.println("Operator yang valid: +, -, *, /, %");
            System.out.println("Contoh : 3 * 5");
            System.out.print("\nInput Angka (misal: 3 + 5 atau ketik 'riwayat' untuk melihat riwayat): ");

            String input = scanner.nextLine();

            if (input.equalsIgnoreCase("riwayat")) {
                showHistory();
                continue;
            }

            String[] parts = input.split(" ");

            if (parts.length != 3) {
                System.out.println("Input tidak valid. Pastikan format: angka operator angka (contoh: 1 + 2)");
                continue;
            }

            double num1;
            double num2;

            try {
                num1 = Double.parseDouble(parts[0]);
                num2 = Double.parseDouble(parts[2]);
            } catch (NumberFormatException e) {
                System.out.println("Input angka tidak valid. Harap masukkan angka yang benar.");
                continue;
            }

            String operator = parts[1];
            double result = 0;

            switch (operator) {
                case "+":
                    result = num1 + num2;
                    break;
                case "-":
                    result = num1 - num2;
                    break;
                case "*":
                    result = num1 * num2;
                    break;
                case "/":
                    if (num2 != 0) {
                        result = num1 / num2;
                    } else {
                        System.out.println("Error: Pembagian dengan nol tidak diperbolehkan.");
                        continue;
                    }
                    break;
                case "%":
                    result = num1 % num2;
                    break;
                default:
                    System.out.println("Operator tidak valid. Gunakan +, -, *, /, atau %.");
                    continue;
            }

            // Membatasi hasil ke 2 angka desimal
            String formattedResult = String.format("%.2f", result);
            System.out.println("Hasil: " + formattedResult);
            history.add(input + " = " + formattedResult);

            System.out.print("\nLanjut Menghitung? (y/n): ");
            continueCalculation = scanner.nextLine();
        }

        if (askForExit(scanner)) {
            System.out.println("Program selesai.");
        } else {
            System.out.println("Program diulang.");
        }
    }

    public static void clearScreen() {
        System.out.print("\033[H\033[2J");
        System.out.flush();
    }

    public static void showHistory() {
        if (history.isEmpty()) {
            System.out.println("Riwayat kosong.");
        } else {
            System.out.println("Riwayat perhitungan:");
            for (String entry : history) {
                System.out.println(entry);
            }
        }
    }

    public static boolean askForExit(Scanner scanner) {
        System.out.print("Yakin ingin keluar? (y/n): ");
        String exitChoice = scanner.nextLine();
        return exitChoice.equalsIgnoreCase("y");
    }
}


