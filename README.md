/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.chatapp;

import java.util.Scanner;
 
/*
 * ChatApp is where the program begins.
 * It displays the welcome screen and main menu,
 * then sends the user to register, log in, or exit.
 */
public class ChatApp {
 
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
 
        // Show the welcome banner when the app launches
        displayWelcomeBanner();
 
        String menuChoice;
 
        // Keep showing the main menu until the user exits
        do {
            displayMainMenu();
            menuChoice = input.nextLine().trim();
            System.out.println("\n_________________________\n");
            processMenuChoice(menuChoice, input);
        } while (!menuChoice.equals("3"));
 
        input.close();
    }
 
    // Prints the SwiftChat welcome banner
    public static void displayWelcomeBanner() {
        System.out.println("**************************************************************************");
        System.out.println("  WELCOME TO SWIFTCHAT");
        System.out.println("**************************************************************************\n");
    }
 
    // Prints the three main menu options
    public static void displayMainMenu() {
        System.out.println("===== SWIFTCHAT MAIN MENU =====");
        System.out.println("1. Register a new account");
        System.out.println("2. Log in to SwiftChat");
        System.out.println("3. Exit");
        System.out.print("\nEnter your choice (1-3): ");
    }
 
    // Handles what happens based on which option the user picks
    public static void processMenuChoice(String menuChoice, Scanner input) {
        switch (menuChoice) {
 
            case "1":
                // Take the user through the registration process
                String registrationResult = AccountManager.registerNewUser(input);
                System.out.println("\n" + registrationResult + "\n");
                break;
 
            case "2":
                // Take the user through the login process
                boolean loggedIn = LoginHandler.runLoginProcess(input);
                // Open the messaging screen if login was successful
                if (loggedIn) {
                    MessageService.openMessagingScreen(input);
                }
                break;
 
            case "3":
                // User chose to exit the app
                System.out.println("Thanks for using SwiftChat. Goodbye!");
                break;
 
            default:
                // User typed something outside 1-3
                System.out.println("Invalid option. Please enter 1, 2 or 3.");
        }
    }
}
