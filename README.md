import java.util.Scanner;

public class Main {

    // Constants
    private static final int MAX_PRODUCTS = 50;
    private static final int MAX_CUSTOMERS = 30;
    private static final String ADMIN_USERNAME = "HatBazar";
    private static final String ADMIN_PASSWORD = "munsi69";

    // Arrays to hold products and customers
    private static Product[] products = new Product[MAX_PRODUCTS];
    private static Customer[] customers = new Customer[MAX_CUSTOMERS];
    private static int productCount = 0;
    private static int customerCount = 0;

    public static void main(String[] args) {
        authenticateAdmin();  // Authenticate admin before accessing the system

        Scanner sc = new Scanner(System.in);
        int choice;

        System.out.println("\n\t\tSuper Shop Management System");

        do {
            System.out.println("\n\tMenu\n\t=========================");
            System.out.println("1. Add Product\t\t2. Search Product");
            System.out.println("3. List Products\t4. Add Customer");
            System.out.println("5. Search Customer\t6. List Customers");
            System.out.println("7. Generate Bill\t8. Exit");
            System.out.print("\nEnter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    addProduct();
                    break;
                case 2:
                    searchProduct();
                    break;
                case 3:
                    listProducts();
                    break;
                case 4:
                    addCustomer();
                    break;
                case 5:
                    searchCustomer();
                    break;
                case 6:
                    listCustomers();
                    break;
                case 7:
                    generateBill();
                    break;
                case 8:
                    System.out.println("\n\t\tTHANK YOU!");
                    // You can add the saveData function if needed
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice!\n");
            }
        } while (choice != 8);
    }

    // Function to authenticate admin
    private static void authenticateAdmin() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter Admin Username: ");
        String username = sc.nextLine();
        System.out.print("Enter Admin Password: ");
        String password = sc.nextLine();

        if (!username.equals(ADMIN_USERNAME) || !password.equals(ADMIN_PASSWORD)) {
            System.out.println("Incorrect username or password. Exiting...");
            System.exit(1);
        }
    }

    // Function to add a product
    private static void addProduct() {
        if (productCount < MAX_PRODUCTS) {
            Scanner sc = new Scanner(System.in);
            System.out.print("Enter product name: ");
            String name = sc.nextLine();
            System.out.print("Enter product price: ");
            float price = sc.nextFloat();
            System.out.print("Enter product quantity: ");
            int quantity = sc.nextInt();

            products[productCount] = new Product(productCount + 1, name, price, quantity);
            productCount++;
            System.out.println("Product added successfully.\n");
        } else {
            System.out.println("Maximum product limit reached!\n");
        }
    }

    // Function to search for a product
    private static void searchProduct() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter product ID: ");
        int searchId = sc.nextInt();
        boolean found = false;

        for (int i = 0; i < productCount; i++) {
            if (products[i].getId() == searchId) {
                System.out.println("\n\tProduct Information");
                System.out.printf("ID: %d\tName: %s\nPrice: %.2f\tQuantity: %d\n",
                        products[i].getId(), products[i].getName(), products[i].getPrice(), products[i].getQuantity());
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Product not found.\n");
        }
    }

    // Function to list all products
    private static void listProducts() {
        System.out.println("\n\t\tProduct List\n");
        System.out.println("ID\tName\t\t\tPrice\t\tQuantity");

        for (int i = 0; i < productCount; i++) {
            System.out.printf("%d\t%s\t\t%.2f\t\t%d\n",
                    products[i].getId(), products[i].getName(), products[i].getPrice(), products[i].getQuantity());
        }
    }

    // Function to add a customer
    private static void addCustomer() {
        if (customerCount < MAX_CUSTOMERS) {
            Scanner sc = new Scanner(System.in);
            System.out.print("Enter Customer's name: ");
            String name = sc.nextLine();
            System.out.print("Enter Customer's address: ");
            String address = sc.nextLine();
            System.out.print("Enter Customer's mobile number: ");
            String mobile = sc.nextLine();

            customers[customerCount] = new Customer(customerCount + 1, name, address, mobile);
            customerCount++;
            System.out.println("Customer added successfully.\n");
        } else {
            System.out.println("Maximum customer limit reached!\n");
        }
    }

    // Function to search for a customer
    private static void searchCustomer() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter Customer ID: ");
        int searchId = sc.nextInt();
        boolean found = false;

        for (int i = 0; i < customerCount; i++) {
            if (customers[i].getId() == searchId) {
                System.out.println("\n\tCustomer Information");
                System.out.printf("ID: %d\tName: %s\nAddress: %s\nMobile: %s\n",
                        customers[i].getId(), customers[i].getName(), customers[i].getAddress(), customers[i].getMobile());
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Customer not found.\n");
        }
    }

    // Function to list all customers
    private static void listCustomers() {
        System.out.println("\n\t\tCustomer List\n");
        System.out.println("ID\tName\t\t\tAddress\t\t\tMobile");

        for (int i = 0; i < customerCount; i++) {
            System.out.printf("%d\t%s\t\t%s\t\t%s\n",
                    customers[i].getId(), customers[i].getName(), customers[i].getAddress(), customers[i].getMobile());
        }
    }

    // Function to generate bill
    private static void generateBill() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter product ID to sell: ");
        int productId = sc.nextInt();
        System.out.print("Enter customer ID: ");
        int customerId = sc.nextInt();
        System.out.print("Enter quantity: ");
        int quantity = sc.nextInt();

        boolean foundProduct = false;
        boolean foundCustomer = false;
        float totalCost = 0;

        // Check if the product exists and if there is enough quantity
        for (int i = 0; i < productCount; i++) {
            if (products[i].getId() == productId) {
                foundProduct = true;
                if (products[i].getQuantity() >= quantity) {
                    totalCost = products[i].getPrice() * quantity;
                    System.out.println("\n\t\tBill");
                    System.out.println("Customer Name: " + customers[customerId - 1].getName());
                    System.out.println("Customer Mobile: " + customers[customerId - 1].getMobile());
                    System.out.println("Product Name: " + products[i].getName());
                    System.out.println("Quantity: " + quantity);
                    System.out.println("Total Cost: " + totalCost);
                } else {
                    System.out.println("Insufficient quantity available for the product.\n");
                }
                break;
            }
        }

        // Check if customer exists
        for (int i = 0; i < customerCount; i++) {
            if (customers[i].getId() == customerId) {
                foundCustomer = true;
                break;
            }
        }

        if (!foundProduct) {
            System.out.println("Product not found.\n");
        }
        if (!foundCustomer) {
            System.out.println("Customer not found.\n");
        }
    }

    // Product class
    static class Product {
        private int id;
        private String name;
        private float price;
        private int quantity;

        public Product(int id, String name, float price, int quantity) {
            this.id = id;
            this.name = name;
            this.price = price;
            this.quantity = quantity;
        }

        public int getId() {
            return id;
        }

        public String getName() {
            return name;
        }

        public float getPrice() {
            return price;
        }

        public int getQuantity() {
            return quantity;
        }
    }

    // Customer class
    static class Customer {
        private int id;
        private String name;
        private String address;
        private String mobile;

        public Customer(int id, String name, String address, String mobile) {
            this.id = id;
            this.name = name;
            this.address = address;
            this.mobile = mobile;
        }

        public int getId() {
            return id;
        }

        public String getName() {
            return name;
        }

        public String getAddress() {
            return address;
        }

        public String getMobile() {
            return mobile;
        }
    }
}
