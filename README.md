# CashRegisterProject-FINAL
A Cash Register System inspired by Mang Inasal.

import java.util.*;
import java.util.regex.*;
import java.io.*;
public class Main {
    static Scanner input = new Scanner(System.in);
    static String entering;
    static String employeeName;
    static String employeePassword;
    static String signupPassword;
    static String date;
    static double change;
    static String email;
    static String customerNumber;
    static  ArrayList<String> workerName = new ArrayList<>(); //add employeeName
    static  ArrayList<String> workerPassword = new ArrayList<>(); //add employeePassword

    public static void display(ArrayList<String> orderName) {
        for (int i = 0; i < orderName.size(); i++) {
            System.out.println(orderName.get(i));
        }
    }

    public static void pricing(ArrayList<Double> priceTag) {
        for (int i = 0; i < priceTag.size(); i++) {
            System.out.println(priceTag.get(i));
        }
    }

    public static void quanti(ArrayList<Integer> itemQuantity) {
        for (int i = 0; i < itemQuantity.size(); i++) {
            System.out.println(itemQuantity.get(i));
        }
    }

    public static void sn(ArrayList<String> storedNames) {
        for (int i = 0; i < storedNames.size(); i++) {
            System.out.println(storedNames.get(i));
        }
    }

    public static void sp(ArrayList<String> storedPasswords) {
        for (int i = 0; i < storedPasswords.size(); i++) {
            System.out.println(storedPasswords.get(i));
        }
    }



    //Mang Inasal Menu
    public static void menu() {
        System.out.println("-----------------------------------");
        System.out.println("Welcome to Mang Inasal!");
        System.out.println(" \"Ihaw-Sarap, Unli-Saya\" ");
        System.out.println("-----------------------------------");

        System.out.println("Menu:");
        System.out.println("\n[Meals]");
        System.out.print("PM1-" + " Chicken Inasal Leg w/rice ");
        System.out.println("[P99]");

        System.out.print("PM2-" + " Chicken Inasal Breast w/rice ");
        System.out.println("[P105.00]");

        System.out.print("PM3-" + " Pork BBQ (2 pieces) w/rice ");
        System.out.println("[P95.75]");

        System.out.print("PM4-" + " Pork Sisig w/rice ");
        System.out.println("[P85.99]");

        System.out.print("PM5-" + " Chicken Inasal Breast w/Halo-Halo ");
        System.out.println("[P115.99]");

       System.out.print("PM6- " + " Bangus Inihaw w/rice ");
        System.out.println("[P99.00]");

        System.out.println("\n[UNLI RICE]");
        System.out.print("UR-" + " Unli Rice Plate ");
        System.out.println("[P15.00]");

        System.out.println("\n[Drinks & DESSERTS]");
        System.out.print("DST1-" + " Halo-Halo ");
        System.out.println("[P20.00]");


        System.out.print("DST2-" + " Leche Flan ");
        System.out.println("[P15.00]");

        System.out.print("D1-" + " Iced Tea ");
        System.out.println("[P10.00]");

        System.out.print("D2-" + " Coca-Cola ");
        System.out.println("[P11.00]");

        System.out.println("-----------------------------------");

    }

    //Employee Register system
    public static void userLogIn() {

        System.out.println("-----------------------------------");
        System.out.println("MANG INASAL CASH REGISTER SYSTEM");
        System.out.println("Sign in or Log in to use.");
        System.out.println("-----------------------------------");

        while (true){
            while(true) {
                System.out.println("Month//Day//Year > 05292025");
                System.out.print("Input the date today: ");
                date = input.nextLine();

                // Regex for 8 digits: 2 for month, 2 for day, 4 for year
                Pattern datePattern = Pattern.compile("^\\d{8}$");
                Matcher dateMatcher = datePattern.matcher(date);
                boolean dateMatches = dateMatcher.matches();

                if (dateMatches) {
                    break;
                } else {
                    System.out.println("-----------------------------------");
                    System.out.println("Please input a valid date.");
                    System.out.println("-----------------------------------");
                    continue;
                }
            }

            System.out.print("Sign up [SU] or Log-in? [LI]: ");
            entering = input.nextLine();
            if(entering.isEmpty()){

                System.out.println("-----------------------------------");
                System.out.println("Please input a valid method.");
                System.out.println("This space cannot be empty");
                System.out.println("-----------------------------------");

            } else if(entering.equalsIgnoreCase("SU") || entering.equalsIgnoreCase("signup") ||
                    entering.equalsIgnoreCase("sign-up") || entering.equalsIgnoreCase("LI") ||
                    entering.equalsIgnoreCase("login") || entering.equalsIgnoreCase("log-in")){
                break;
            } else {
                System.out.println("-----------------------------------");
                System.out.println("Please input a valid method.");
                System.out.println("-----------------------------------");
                continue;
            }
        }

        if ((entering.equalsIgnoreCase("li") || entering.equalsIgnoreCase("login") || entering.equalsIgnoreCase("log-in"))) {

            while (true) {
                System.out.println("-----------------------------------");
                System.out.print("Please input your employee name: ");
                employeeName = input.nextLine();

                System.out.print("Please input your password: ");
                employeePassword = input.nextLine();

                //asked AI on how to get the saved user info from the txt file
                try (BufferedReader reader = new BufferedReader(new FileReader("WorkerProfiles.txt"))) {
                    String line;
                    boolean found = false;

                    while ((line = reader.readLine()) != null) {
                        String[] parts = line.split(" ");
                        if (parts.length >= 2) {
                            String savedName = parts[0];
                            String savedPass = parts[1];

                            if (savedName.equals(employeeName) && savedPass.equals(employeePassword)) {
                                found = true;
                                break;
                            }
                        }
                    }
                    //end of AI help

                    if (found) {
                        System.out.println("-----------------------------------");
                        System.out.println("Employee user accepted!");
                        System.out.println(" \"Love the Flavors, Love the Philippines\".");
                        break;
                    } else {
                        System.out.println("-----------------------------------");
                        System.out.println("Invalid username or password.");
                        System.out.println("Please try again.");
                        continue;
                    }
                } catch (Exception e) {
                    throw new RuntimeException(e);
                }
            }

        } else if (entering.equalsIgnoreCase("su") || entering.equalsIgnoreCase("signup") || entering.equalsIgnoreCase("sign-up")){

            System.out.println("-----------------------------------");
            System.out.print("Please input a name to sign up: ");
            employeeName = input.nextLine();

            Pattern signupPattern = Pattern.compile("^[a-zA-Z]{5}$|^[a-zA-Z]{15}$");
            Matcher signupMatcher = signupPattern.matcher(employeeName);
            boolean signupMatches = signupMatcher.matches();


            if(employeeName.isEmpty()){
                System.out.println("-----------------------------------");
                System.out.println("This space cannot be empty.");
                System.out.println("Please input a valid name");

            } else if(!signupMatches){
                System.out.println("-----------------------------------");
                System.out.println("Please input a valid name to sign up");
                System.out.println("A username must contain [5] or [15] characters.");
                System.out.println("Please try again.");
            }

            while(true) {
                if (!signupMatches) {
                    System.out.println("-----------------------------------");
                    System.out.print("Please input a name to sign up: ");
                    employeeName = input.nextLine();

                    if(employeeName.isEmpty()){
                        System.out.println("-----------------------------------");
                        System.out.println("This space cannot be empty.");
                        System.out.println("Please input a valid name");
                        continue;
                    }

                    if(employeeName.length() == 5 || employeeName.length() == 15){
                        signupMatches = true;
                        break;
                    }

                    System.out.println("-----------------------------------");
                    System.out.println("Please input a valid name to sign up");
                    System.out.println("A username must contain [5] or [15] characters.");
                    System.out.println("Please try again.");
                    continue;
                } else {
                    signupMatches = true;
                    break;
                }
            }


            if(signupMatches){
                System.out.println("Name " + "[" + employeeName + "]" + " registered!");
                System.out.println("-----------------------------------");

                while (true) {
                    System.out.print("Create a valid password: ");
                    signupPassword = input.nextLine();

                    //Asked AI for help on passwordPattern
                    //requires at least one small letter, uppercase letter, and number
                    Pattern passwordPattern = Pattern.compile("^(?=.*[a-z])(?=.*[0-9])(?=.*[A-Z])[a-zA-Z0-9]{8}$");
                    Matcher passwordMatcher = passwordPattern.matcher(signupPassword);
                    boolean passwordMatches = passwordMatcher.matches();

                    if(signupPassword.isEmpty()){
                        System.out.println("-----------------------------------");
                        System.out.println("This space cannot be empty.");
                        System.out.println("Please input a valid password.");
                        System.out.println("-----------------------------------");
                        continue;
                    }

                    if (passwordMatches) {
                        System.out.println("-----------------------------------");
                        System.out.println("The password for " + employeeName + " has been registered!");
                        System.out.println("-----------------------------------");
                        System.out.println("Registered employee name: " + employeeName);
                        System.out.println("Your account has been successfully registered!");
                        workerName.add(employeeName); //save it to the arraylist
                        workerPassword.add(signupPassword);

                        try(BufferedWriter writer = new BufferedWriter(new FileWriter("WorkerProfiles.txt", true))){
                            for(int i = 0; i < workerName.size(); i++) {
                                if(i < workerName.size()) {
                                    writer.write(workerName.get(i) + " " + workerPassword.get(i));
                                    writer.newLine();
                                    writer.close();
                                }
                            }
                        }catch (Exception e){
                            System.out.println("An error has been discovered by the system!");
                            System.out.println(e.getMessage());
                        }
                        break;
                    } else if (!passwordMatches) {
                        System.out.println("-----------------------------------");
                        System.out.println("A Password must at least contain:");
                        System.out.println("ONE lowercase letter, UPPERCASE LETTER, and DIGIT.");
                        System.out.println("-----------------------------------");
                        System.out.println("A Password must also be 8 characters in length.");
                        System.out.println("-----------------------------------");
                        continue;
                    }
                }
            }
        }
    }



    //use substring to edit employee name?

    public static void main(String[] args) {
        ArrayList<String> orderName = new ArrayList<String>();
        ArrayList<Double> priceTag = new ArrayList<Double>();
        ArrayList<Integer> itemQuantity = new ArrayList<Integer>();


        //The values used (for the do while loop and the computation of price and quantity)
        //If I'm correct, if a value is inside a loop or specific curly brackets, the other values outside don't detect it
        String options = "y";
        double processedPayment = 0.00;
        double total = 0.00;
        int quantity = 0;
        String payment;
        String delete = "n";
        String orderRemove = "";
        String discount = "n";
        double seniorDiscount = 0.0;
        double discountedTotal = total;
        boolean contAction = true;
        double numPayment = 0.0;
        double sufPayment = 0.0;
        double sufficient = 0.00;
        String userInput;
        String membership;
        String sufficientAmount = "0";
        String dineOrTake;
        String tableNumber = "00";

        userLogIn(); //Register system

        menu(); //Menu display


        do{ //full order loop

            //Add dine in or take out
            while(true){
                System.out.print("Dine in [DN] or Take Out? [TO]: ");
                dineOrTake = input.nextLine();

                if(dineOrTake.equalsIgnoreCase("dn") ||  dineOrTake.equalsIgnoreCase("dine in") || dineOrTake.equalsIgnoreCase("dinein")){
                    break;
                } else if(dineOrTake.equalsIgnoreCase("to") || dineOrTake.equalsIgnoreCase("take out") || dineOrTake.equalsIgnoreCase("takeout")){
                    break;
                } else if(dineOrTake.isEmpty()){
                    System.out.println("-----------------------------------");
                    System.out.println("Please choose a valid answer.");
                    System.out.println("This space cannot be empty");
                    System.out.println("-----------------------------------");
                    continue;
                } else {
                    System.out.println("-----------------------------------");
                    System.out.println("Please input a valid answer.");
                    System.out.println("-----------------------------------");
                    continue;
                }
            }

            if(dineOrTake.equalsIgnoreCase("dn") ||  dineOrTake.equalsIgnoreCase("dine in") || dineOrTake.equalsIgnoreCase("dinein")) {
                while (true) {
                    System.out.println("-----------------------------------");
                    System.out.print("Enter table number: ");
                    tableNumber = input.nextLine();

                    Pattern tablePattern = Pattern.compile("^[0-9]{2}$");
                    Matcher tableMatcher = tablePattern.matcher(tableNumber);
                    boolean isTableMatch = tableMatcher.matches();

                    if (isTableMatch) {
                        System.out.println("Table number \"" + tableNumber + "\" has been registered!");
                        System.out.println("-----------------------------------");
                        break;
                    } else {
                        System.out.println("Please use the proper format.");
                        System.out.println("EX: 07");
                        continue;
                    }
                }
            }

        do { //do you want to keep ordering loop

            do { //Enter order name loop
                System.out.print("Enter order name (Enter stop to end): ");
                userInput = input.nextLine();

                switch (userInput) {
                    case "PM1":
                    case "pm1":
                        priceTag.add(99.00);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 99.00;
                        orderName.add(userInput);
                        break;

                    case "PM2":
                    case "pm2":
                        priceTag.add(105.00);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 105.00;
                        orderName.add(userInput);
                        break;

                    case "PM3":
                    case "pm3":
                        priceTag.add(95.75);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 95.75;
                        orderName.add(userInput);
                        break;

                    case "PM4":
                    case "pm4":
                        priceTag.add(85.99);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 85.99;
                        orderName.add(userInput);
                        break;

                    case "PM5":
                    case "pm5":
                        priceTag.add(115.99);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 115.99;
                        orderName.add(userInput);
                        break;

                    case "PM6":
                    case "pm6":
                        priceTag.add(99.00);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 99.00;
                        orderName.add(userInput);
                        break;

                    case "DST1":
                    case "dst1":
                        priceTag.add(20.00);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 20.00;
                        orderName.add(userInput);
                        break;

                    case "DST2":
                    case "dst2":
                        priceTag.add(15.00);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 15.00;
                        orderName.add(userInput);
                        break;

                    case "D1":
                    case "d1":
                        priceTag.add(10.00);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 10.00;
                        orderName.add(userInput);
                        break;

                    case "D2":
                    case "d2":
                        priceTag.add(11.00);
                        itemQuantity.add(1);
                        quantity = quantity + 1;
                        total += 11.00;
                        orderName.add(userInput);
                        break;

                    case "UR":
                    case "ur":
                        if(dineOrTake.equalsIgnoreCase("dn") ||  dineOrTake.equalsIgnoreCase("dine in") || dineOrTake.equalsIgnoreCase("dinein")) {
                            priceTag.add(15.00);
                            itemQuantity.add(1);
                            quantity = quantity + 1;
                            total += 15.00;
                            orderName.add(userInput);
                            break;
                        } else {
                            System.out.println("-----------------------------------");
                            System.out.println("NOTE: You cannot order UNLIMITED RICE [UR] for Take Out.");
                            System.out.println("-----------------------------------");
                            continue;
                        }

                    default:
                        if (userInput.isBlank() || itemQuantity.isEmpty()) {
                            System.out.println("-----------------------------------");
                            System.out.println("Please input a valid order.");
                            System.out.println("An order cannot be empty.");
                            System.out.println("-----------------------------------");
                            continue;
                        } else if (userInput.equalsIgnoreCase("stop")) {
                            break;
                        } else {
                            System.out.println("-----------------------------------");
                            System.out.println("Please input a registered order name.");
                            System.out.println("-----------------------------------");
                            continue;
                        }

                }


                if (userInput.equalsIgnoreCase("stop")) {

                    while (true) {
                        System.out.println("-----------------------------------");
                        System.out.print("Are you a senior citizen? y/n: ");
                        discount = input.nextLine();

                        if (discount.equalsIgnoreCase("n") || discount.equalsIgnoreCase("no")) {
                            options = "n";
                            break;
                        }

                        if (discount.equalsIgnoreCase("y")) {
                            System.out.println("-----------------------------------");
                            System.out.printf("Original Price: P%.2f", total);
                            System.out.println("");
                            System.out.println("-----------------------------------");

                            seniorDiscount = total * 0.15;
                            discountedTotal = total - seniorDiscount;
                            System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                            System.out.println("A 15% Senior Citizen Discount has been added!");
                            options = "n";
                            break;
                        } else {
                            System.out.println("-----------------------------------");
                            System.out.println("Please input a valid option.");
                            continue;
                        }
                    }

                        while (true) {
                            System.out.println("-----------------------------------");
                            System.out.print("Do you want to continue ordering? y/n: ");
                            options = input.nextLine();

                            if (options.equalsIgnoreCase("n") || options.equalsIgnoreCase("no")) {
                                break;
                            } else if (options.equalsIgnoreCase("y") || options.equalsIgnoreCase("yes")) {
                               break;
                            } else {
                                System.out.println("Please input a valid option.");
                                continue;
                            }
                        }
                    }

            }while(options.equalsIgnoreCase("y"));

        } while (options.equalsIgnoreCase("y"));




        System.out.println("-----------------------------------");
        System.out.println("Quantity of items: " + quantity);
        System.out.println("Orders Added:" + orderName);
        System.out.println("Price(s): " + priceTag);
        System.out.printf("\nTotal: P%.2f%n", total);
            if(discount.equalsIgnoreCase("y")){
                seniorDiscount = total * 0.15;
                discountedTotal = total - seniorDiscount;
                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
            }
        System.out.println("-----------------------------------");

        while(true){
            if(quantity >= 2){
                System.out.print("Do you want to remove an order? y/n: ");
                options = input.nextLine();
                System.out.println("-----------------------------------");

                if(options.equalsIgnoreCase("y") || options.equalsIgnoreCase("yes")){
                    break;
                } else if(options.equalsIgnoreCase("n") || options.equalsIgnoreCase("no")){
                    break;
                } else {
                    System.out.println("Please input a valid option.");
                    System.out.println("-----------------------------------");
                    continue;
                }
            } else {
                break;
            }
        }

        do { //Full remove order loop

            do { //Remove functionality loo

                do{ //Removing items loops
                    if (quantity < 2) {
                        System.out.println("[YOU CAN NO LONGER REMOVE ANYMORE ITEMS.]");
                        System.out.println("-----------------------------------");
                        options = "n";
                        break; // Exit removal step
                    }

                    if(options.equalsIgnoreCase("y")) {
                        if (quantity >= 2) {
                            System.out.print("Type the order you want to remove (Enter stop to end): ");
                            orderRemove = input.nextLine();
                            System.out.println("-----------------------------------");


                            if ((orderRemove.equalsIgnoreCase("stop"))) {
                                options = "n";
                                break;
                            } else if (!orderName.contains(orderRemove)) { //Makes sure that it does not return an error
                                System.out.println("Please input a valid order name!");
                                System.out.println("-----------------------------------");
                                continue;
                            } else {
                                switch (orderRemove) {
                                    case "PM1":
                                    case "pm1":

                                            if (orderName.contains(orderRemove)) {
                                                int index = orderName.indexOf(orderRemove);
                                                itemQuantity.remove(index);
                                                orderName.remove(index);
                                                priceTag.remove(index);
                                                quantity -= 1;
                                                total -= 99.00;

                                                System.out.println("PM1 Removed");
                                                System.out.println("Orders Left:" + orderName);
                                                System.out.println("Individual orders: " + itemQuantity);
                                                System.out.println("Quantity: " + quantity + " order(s)");
                                                System.out.println("Price(s): " + priceTag);
                                                System.out.printf("Total: P%.2f%n", total);
                                                if (discount.equalsIgnoreCase("y")) {
                                                    seniorDiscount = total * 0.15;
                                                    discountedTotal = total - seniorDiscount;
                                                    System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                                }
                                                System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "PM2":
                                    case "pm2":

                                        if (orderName.contains(orderRemove)){

                                            int index = orderName.indexOf(orderRemove);
                                            itemQuantity.remove(index);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            quantity -= 1;
                                            total -= 105.00;

                                            System.out.println("PM2 Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            System.out.printf("Total: P%.2f%n", total);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "pm3":
                                    case "PM3":
                                            if (orderName.contains(orderRemove)) {

                                                int index = orderName.indexOf(orderRemove);
                                                priceTag.remove(index);
                                                orderName.remove(index);
                                                itemQuantity.remove(index);
                                                quantity -= 1;
                                                total -= 95.75;

                                                System.out.println("PM3 Removed");
                                                System.out.println("Orders Left:" + orderName);
                                                System.out.println("Individual orders: " + itemQuantity);
                                                System.out.println("Quantity: " + quantity + " order(s)");
                                                System.out.println("Price(s): " + priceTag);
                                                System.out.printf("Total: P%.2f%n", total);
                                                if (discount.equalsIgnoreCase("y")) {
                                                    seniorDiscount = total * 0.15;
                                                    discountedTotal = total - seniorDiscount;
                                                    System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                                }
                                                System.out.println("-----------------------------------");
                                            }
                                        break;

                                    case "pm4":
                                    case "PM4":
                                        if (orderName.contains(orderRemove)) {

                                            int index = orderName.indexOf(orderRemove);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            itemQuantity.remove(index);
                                            quantity -= 1;
                                            total -= 85.99;

                                            System.out.println("PM4 Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.printf("Total: P%.2f%n", total);
                                            System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "pm5":
                                    case "PM5":
                                        if (orderName.contains(orderRemove)) {

                                            int index = orderName.indexOf(orderRemove);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            itemQuantity.remove(index);
                                            quantity -= 1;
                                            total -= 115.99;

                                            System.out.println("PM5 Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            System.out.printf("Total: P%.2f%n", total);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "pm6":
                                    case "PM6":
                                        if (orderName.contains(orderRemove)) {

                                            int index = orderName.indexOf(orderRemove);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            itemQuantity.remove(index);
                                            quantity -= 1;
                                            total -= 99.00;

                                            System.out.println("PM6 Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            System.out.printf("Total: P%.2f%n", total);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "dst1":
                                    case "DST1":
                                        if (orderName.contains(orderRemove)) {

                                            int index = orderName.indexOf(orderRemove);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            itemQuantity.remove(index);
                                            quantity -= 1;
                                            total -= 20.00;

                                            System.out.println("DST1 Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            System.out.printf("Total: P%.2f%n", total);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "dst2":
                                    case "DST2":
                                        if(orderName.contains(orderRemove)){

                                            int index = orderName.indexOf(orderRemove);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            itemQuantity.remove(index);
                                            quantity -= 1;
                                            total -= 15;

                                            System.out.println("DST2 Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            System.out.printf("Total: P%.2f%n", total);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "d1":
                                    case "D1":
                                        if (orderName.contains(orderRemove)) {

                                            int index = orderName.indexOf(orderRemove);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            itemQuantity.remove(index);
                                            quantity -= 1;
                                            total -= 10.00;

                                            System.out.println("D1 Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            System.out.printf("Total: P%.2f%n", total);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "d2":
                                    case "D2":
                                        if (orderName.contains(orderRemove)) {

                                            int index = orderName.indexOf(orderRemove);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            itemQuantity.remove(index);
                                            quantity -= 1;
                                            total -= 11.00;

                                            System.out.println("D2 Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            System.out.printf("Total: P%.2f%n", total);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.println("-----------------------------------");
                                        }
                                        break;

                                    case "UR":
                                    case "ur":
                                        if(orderName.contains(orderRemove)){

                                            int index = orderName.indexOf(orderRemove);
                                            orderName.remove(index);
                                            priceTag.remove(index);
                                            itemQuantity.remove(index);
                                            quantity -= 1;
                                            total -= 15.00;

                                            System.out.println("UR Removed");
                                            System.out.println("Orders Left:" + orderName);
                                            System.out.println("Individual orders: " + itemQuantity);
                                            System.out.println("Quantity: " + quantity + " order(s)");
                                            System.out.println("Price(s): " + priceTag);
                                            System.out.printf("Total: P%.2f%n", total);
                                            if (discount.equalsIgnoreCase("y")) {
                                                seniorDiscount = total * 0.15;
                                                discountedTotal = total - seniorDiscount;
                                                System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                                            }
                                            System.out.println("-----------------------------------");

                                        }
                                        break;


                                }
                            }
                        }
                    }



                }while(options.equalsIgnoreCase("y"));

                System.out.println("Orders Added:" + orderName);
                System.out.println("Individual orders: " + itemQuantity);
                System.out.println("Price(s): " + priceTag);

            System.out.printf("Total: P%.2f%n", total);
                if(discount.equalsIgnoreCase("y")){
                    seniorDiscount = total * 0.15;
                    discountedTotal = total - seniorDiscount;
                    System.out.printf("Discounted Price: P%.2f\n", discountedTotal);
                }

                while(true){
                    System.out.print("Enter payment amount: ");
                    payment = input.nextLine();

                    Pattern payPattern = Pattern.compile("^[0-9]\\d*\\.*+[0-9]*$");
                    Matcher payMatcher = payPattern.matcher(payment);
                    boolean payIsMatch = payMatcher.matches();

                    if(payIsMatch){
                        numPayment = Double.parseDouble(payment);
                        if (discount.equalsIgnoreCase("y")) {
                            seniorDiscount = total * 0.15;
                            discountedTotal = total - seniorDiscount;
                            processedPayment = numPayment - discountedTotal;
                        } //unsure
                        break;
                    } else {
                        System.out.println("-----------------------------------");
                        System.out.println("Please input an integer or number,");
                        System.out.println("-----------------------------------");
                        continue;
                    }
                }

            if(quantity >= 2){
                while(true){
                    System.out.println("-----------------------------------");
                    System.out.print("Do you want to remove any items before purchase? y/n: ");
                    options = input.nextLine();

                    if(options.equalsIgnoreCase("y") || options.equalsIgnoreCase("yes")||
                            options.equalsIgnoreCase("n") || options.equalsIgnoreCase("no")){
                        break;
                    }

                                if(options.isEmpty()){
                                    System.out.println("-----------------------------------");
                                    System.out.println("This space cannot be empty.");
                                    System.out.println("Please input a valid option,");
                                    continue;
                                } else {
                                    System.out.println("-----------------------------------");
                                    System.out.println("Please input a valid answer.");
                                    continue;
                                }
                            }
                    }


        } while (options.equalsIgnoreCase("y"));

        }while(options.equalsIgnoreCase("y"));

            if(dineOrTake.equalsIgnoreCase("dn") ||  dineOrTake.equalsIgnoreCase("dine in") || dineOrTake.equalsIgnoreCase("dinein")) {
                System.out.println("-----------------------------------");
                System.out.println("Table number: " + tableNumber);
            }

            System.out.println("-----------------------------------");
                System.out.println("Cashier name: "  + employeeName);
                System.out.println("Orders Added:" + orderName);
                System.out.println("Individual orders: " + itemQuantity);
                System.out.println("Price(s): " + priceTag);
                System.out.println("Quantity: " + quantity + " order(s)");
            if (discount.equalsIgnoreCase("y")) {
                System.out.println("Senior Citizen Discount Status: [ACTIVE]");
                System.out.printf("Total (Before Discount): P%.2f%n", total);
                System.out.printf("Discounted Price: P%.2f%n", discountedTotal);
            } else {
                System.out.printf("Total: P%.2f%n", total);
            }

            numPayment = Math.round(numPayment * 100.0) / 100.0; //AI written, rounds of the payment number to 0.15 instead of 0.156247
            //checks if it is discounted or not
            double effectiveTotal = discount.equalsIgnoreCase("y") || discount.equalsIgnoreCase("yes") ? discountedTotal : total;
            effectiveTotal = Math.round(effectiveTotal * 100.0) / 100.0; //the final price

            if (numPayment < effectiveTotal) { //Ai added to my code
                System.out.printf("Payment: Insufficient Amount! (P%.2f)%n", numPayment);
                System.out.println("Please pay the sufficient amount.");
                System.out.println("-----------------------------------");
                //end of AI help

                while(true){
                    System.out.println("[Type \"CANCEL\" to scrap order]");
                    System.out.print("Enter sufficient amount: ");
                    sufficientAmount = input.nextLine();

                    if (sufficientAmount.equalsIgnoreCase("cancel")) {
                        System.out.println("The order has been cancelled.");
                        break;
                    }

                    Pattern sufPattern = Pattern.compile("^[0-9]\\d*\\.*[0-9]*");
                    Matcher sufMatcher = sufPattern.matcher(sufficientAmount);
                    boolean sufIsMatch = sufMatcher.matches();

                    if(sufIsMatch){
                        sufPayment = Double.parseDouble(sufficientAmount);

                        if(discount.equalsIgnoreCase("y")){
                            seniorDiscount = total * 0.15;
                            discountedTotal = total - seniorDiscount;
                            sufficient = sufPayment - discountedTotal;
                        } else {
                            sufficient = sufPayment - total;
                        }

                        final double EPSILON = 0.01; // Small margin of error (1 cent)

                        double requiredTotal = discount.equalsIgnoreCase("y") ? discountedTotal : total;
                        sufficient = sufPayment - requiredTotal;

                        if(sufficient + EPSILON >= 0){
                            System.out.printf("Payment: P%.2f%n", sufPayment);
                            System.out.printf("Change: P%.2f%n", sufficient);
                            System.out.println("-----------------------------------");
                            System.out.println("[THIS TRANSACTION HAS BEEN COMPLETED!]");
                            break;
                        }

                        if (sufPayment < total || sufPayment < discountedTotal){
                            System.out.println("-----------------------------------");
                            System.out.println("Please input a sufficient amount.");
                            System.out.println("-----------------------------------");
                            continue;
                        }

                    } else {
                        System.out.println("-----------------------------------");
                        System.out.println("Please input a valid number or integer.");
                        System.out.println("-----------------------------------");
                        continue;
                    }
                }


            } else {
                change = numPayment - effectiveTotal;

                if (change == -0.0) change = 0.0; // Fix -0.00 display

                System.out.printf("Payment: P%.2f%n", numPayment);
                System.out.printf("Change: P%.2f%n", change);
                System.out.println("[THIS TRANSACTION HAS BEEN COMPLETED!]");
            }
                System.out.println("-----------------------------------");


            while(true){
                System.out.print("Do you want to apply for a membership? y/n: "); //Get customer details
                membership = input.nextLine();

                if(membership.equalsIgnoreCase("y") || membership.equalsIgnoreCase("yes")){
                    break;
                } else if(membership.isEmpty()){
                    System.out.println("-----------------------------------");
                    System.out.println("Please choose a valid option.");
                    System.out.println("This space cannot be empty");
                    System.out.println("-----------------------------------");
                    continue;
                } else if(membership.equalsIgnoreCase("n") || membership.equalsIgnoreCase("no")){
                    break;
                } else {
                    System.out.println("-----------------------------------");
                    System.out.println("Please input a valid option.");
                    continue;

                }

            }

            if(membership.equalsIgnoreCase("y") || membership.equalsIgnoreCase("yes")){
                while(true) {
                    System.out.println("-----------------------------------");
                    System.out.println("(EX: john123@gmail.com or john@gmail.com): ");
                    System.out.print("Please input customers personal email: ");
                    email = input.nextLine();

                    //Regex email
                    Pattern pattern = Pattern.compile("^[A-Za-z]+[0-9]*+@[a-z]+\\.[a-z]{3}$");
                    Matcher matcher = pattern.matcher(email);
                    boolean isMatch = matcher.matches();

                    if(email.isEmpty()){
                        System.out.println("-----------------------------------");
                        System.out.println("Please choose a valid option.");
                        System.out.println("This space cannot be empty");
                        System.out.println("-----------------------------------");
                        continue;
                    }

                    if (isMatch) {
                        System.out.println("-----------------------------------");
                        System.out.println(email + " has been registered!");
                        break;
                    } else {
                        System.out.println("-----------------------------------");
                        System.out.println("Please input a valid email/gmail account.");
                        continue;
                    }
                }

                    while(true){
                        System.out.println("-----------------------------------");
                        System.out.print("Please enter customers number (EX: 09925188614): ");
                        customerNumber = input.nextLine();

                        //Regex number
                        Pattern numPattern = Pattern.compile("^[0]+[0-9]{10}$");
                        Matcher numMatcher = numPattern.matcher(customerNumber);
                        boolean numMatch = numMatcher.matches();

                        if(customerNumber.isEmpty()){
                            System.out.println("-----------------------------------");
                            System.out.println("Please choose a valid option.");
                            System.out.println("This space cannot be empty");
                            continue;
                        }

                        if(numMatch){
                            System.out.println("-----------------------------------");
                            System.out.println(customerNumber + " has been registered!");
                            System.out.println("-----------------------------------");
                            break;
                        } else {
                            System.out.println("-----------------------------------");
                            System.out.println("Please input a valid number.");
                            continue;
                        }
                    }

            }

            int receiptNum = 1;
            while (new File("transactions" + "[" + receiptNum  + "]" + ".txt").exists()) {
                receiptNum++;
            } //checks if the file name or the receipt name exists

            String fileName = "transactions" + "[" + receiptNum  + "]" + ".txt";

            try(BufferedWriter writer = new BufferedWriter(new FileWriter("transactions" + "[" + receiptNum  + "]" + ".txt"))){
                writer.write("========== RECEIPT ==========");
                writer.newLine();
                writer.write("Date DAY/MONTH/YEAR: " + date);
                writer.newLine();
                writer.write("Cashier name: " + employeeName);
                writer.newLine();
                writer.write("Dine in or Take out: " + dineOrTake);
                writer.newLine();
                if(dineOrTake.equalsIgnoreCase("dn") ||  dineOrTake.equalsIgnoreCase("dine in") || dineOrTake.equalsIgnoreCase("dinein")) {
                    writer.write("Table number: " + tableNumber);
                    writer.newLine();
                }
                writer.write("Item quantity: " + quantity);
                writer.newLine();
                writer.write("Orders added: " + orderName);
                writer.newLine();
                writer.write("Individual Prices: " + priceTag);
                writer.newLine();
                writer.write("Discount: " + discount);
                writer.newLine();
                writer.write("Total: " + total);
                writer.newLine();
                if(discount.equalsIgnoreCase("y") || discount.equalsIgnoreCase("yes")){
                    writer.write("Discounted total: " + String.format("P%.2f", discountedTotal));
                    writer.newLine();
                }
                if(numPayment > effectiveTotal) {
                    writer.write("Paid amount: " + String.format("P%.2f", sufPayment));
                    writer.newLine();
                    writer.write("Change: " + String.format("P%.2f", sufficient));
                    writer.newLine();
                } else {
                    writer.write("Paid amount: " + numPayment);
                    writer.newLine();
                    writer.write("Change: " + change);
                    writer.newLine();
                    writer.write("Membership application: " + membership);
                    writer.newLine();
                    if(membership.equalsIgnoreCase("y") || membership.equalsIgnoreCase("yes")) {
                        writer.write("Customer email: " + email);
                        writer.newLine();
                        writer.write("Customer number: " + customerNumber);
                        writer.newLine();
                    }
                }
                writer.write("========== " + "RECEIPT NO. " + receiptNum + " ==========");
                writer.newLine();
                writer.close();

            }catch(Exception e){
                System.out.println(e.getMessage());
            }

            while(true) {
                System.out.print("Do you want to do another transaction? y/n: ");
                options = input.nextLine();

                if (options.equalsIgnoreCase("y") || options.equalsIgnoreCase("yes")) {
                    break;
                } else if (options.isEmpty()) {
                    System.out.println("-----------------------------------");
                    System.out.println("Please choose a valid option.");
                    System.out.println("This space cannot be empty");
                    System.out.println("-----------------------------------");
                    continue;
                } else if (options.equalsIgnoreCase("n") || options.equalsIgnoreCase("no")) {
                    break;
                } else {
                    System.out.println("-----------------------------------");
                    System.out.println("Please input a valid option.");
                    System.out.println("-----------------------------------");
                    continue;
                }
            }


               if(options.equalsIgnoreCase("y")){
                   System.out.println("-----------------------------------");
                   System.out.println("New Transaction In Progress!"); //Clears all the values for a new transaction
                   System.out.println("-----------------------------------");
                   orderName.clear();
                   priceTag.clear();
                   itemQuantity.clear();

                   quantity = 0; //resets the values of the numbers
                   total = 0;
                   numPayment = 0.0;
                   processedPayment = 0.0;

               } else if(options.equalsIgnoreCase("n")){
                   System.out.println("-----------------------------------");
                   System.out.println("THANK YOU FOR ORDERING AT MANG INASAL!");
                   System.out.println("-----------------------------------");
               }


        }while(options.equalsIgnoreCase("y"));

    }
}
