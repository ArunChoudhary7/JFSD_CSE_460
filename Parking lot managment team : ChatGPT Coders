import java.util.*;
class Vehicle {
    String licensePlate;
    String type;
    public Vehicle(String licensePlate, String type) {
        this.licensePlate = licensePlate;
        this.type = type;
    }
}

class ParkingTicket {
    int ticketID;
    String licensePlate;
    int hoursParked;
    double cost;

    public ParkingTicket(int ticketID, String licensePlate, int hoursParked, double cost) {
        this.ticketID = ticketID;
        this.licensePlate = licensePlate;
        this.hoursParked = hoursParked;
        this.cost = cost;
    }
}

class ParkingSpot {
    int id;
    String type;
    boolean occupied;

    public ParkingSpot(int id, String type) {
        this.id = id;
        this.type = type;
        this.occupied = false;
    }
}
class ParkingLot {
    private static final int MAX_SPOTS = 15;
    private ParkingSpot[] spots;
    private List<ParkingTicket> tickets;
    private int availableSpots;
    private int ticketCount;
    private double totalRevenue;

    public ParkingLot() {
        spots = new ParkingSpot[MAX_SPOTS];
        tickets = new ArrayList<>();
        availableSpots = MAX_SPOTS;
        ticketCount = 0;
        totalRevenue = 0.0;

        for (int i = 0; i < MAX_SPOTS; i++) {
            String type;
            if (i % 4 == 0) type = "EV";
            else if (i % 4 == 1) type = "Motorcycle";
            else if (i % 4 == 2) type = "Truck";
            else type = "Regular";

            spots[i] = new ParkingSpot(i + 1, type);
        }
    }

    private double getParkingRate(String vehicleType) {
        switch (vehicleType) {
            case "EV":
                return 1.0;
            case "Motorcycle":
                return 0.5;
            case "Truck":
                return 3.0;
            default:
                return 2.0;
                }
    }

    public void displayAvailability() {
        System.out.println("Available Spots: " + availableSpots + "/" + MAX_SPOTS);
        for (ParkingSpot spot : spots) {
            System.out.println("Spot ID: " + spot.id + ", Type: " + spot.type + 
                               ", Occupied: " + (spot.occupied ? "Yes" : "No"));
        }
    }
public void parkVehicle(Vehicle vehicle, int hours) {
        for (ParkingSpot spot : spots) {
            if (!spot.occupied && spot.type.equals(vehicle.type)) {
                double cost = getParkingRate(vehicle.type) * hours;
                spot.occupied = true;
                tickets.add(new ParkingTicket(ticketCount + 1, vehicle.licensePlate, hours, cost));
                totalRevenue += cost;
                availableSpots--;
                System.out.printf("Vehicle parked at Spot ID: %d. Total Cost: $%.2f%n", spot.id, cost);
                return;
            }
        }
        System.out.println("No available spots for vehicle type: " + vehicle.type);
    }

public void removeVehicle(String licensePlate) {
        for (ParkingSpot spot : spots) {
            if (spot.occupied) {
                for (ParkingTicket ticket : tickets) {
                    if (ticket.licensePlate.equals(licensePlate)) {
                        spot.occupied = false;
                        availableSpots++;
                        totalRevenue -= ticket.cost;
                        System.out.printf("Vehicle with license plate %s removed from Spot ID: %d.%n" +
                                          "Total hours parked: %d. Total cost: $%.2f%n",
                                          licensePlate, spot.id, ticket.hoursParked, ticket.cost);
                        return;
                    }
                }
            }
        }
        System.out.println("Vehicle with license plate " + licensePlate + " not found in the parking lot.");
    }
public void viewAdminReport() {
        System.out.println("Admin Report:");
        for (ParkingTicket ticket : tickets) {
            System.out.printf("Ticket ID: %d, License Plate: %s, Hours Parked: %d, Cost: $%.2f%n",
                              ticket.ticketID, ticket.licensePlate, ticket.hoursParked, ticket.cost);
        }
        System.out.printf("Total Revenue: $%.2f%n", totalRevenue);
        System.out.println("Total Parked Vehicles: " + tickets.size());
        System.out.println("Available Spots: " + availableSpots);
        System.out.println("Occupied Spots: " + (MAX_SPOTS - availableSpots));
    }

    public void resetParkingLot() {
        for (ParkingSpot spot : spots) {
            spot.occupied = false;
        }
        availableSpots = MAX_SPOTS;
        tickets.clear();
        totalRevenue = 0.0;
        System.out.println("Parking lot reset successful.");
    }
public void displayUserParkingHistory(String licensePlate) {
        System.out.println("Parking History for License Plate: " + licensePlate);
        boolean found = false;
        for (ParkingTicket ticket : tickets) {
            if (ticket.licensePlate.equals(licensePlate)) {
                System.out.printf("Ticket ID: %d, Hours Parked: %d, Cost: $%.2f%n",
                                  ticket.ticketID, ticket.hoursParked, ticket.cost);
                found = true;
            }
        }
        if (!found) {
            System.out.println("No parking history found for this vehicle.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ParkingLot lot = new ParkingLot();
        int choice;

        do {
            System.out.println("\nSmart Parking Management System");
            System.out.println("1. Display Availability");
            System.out.println("2. Park Vehicle");
            System.out.println("3. Remove Vehicle");
            System.out.println("4. View Admin Report");
            System.out.println("5. Reset Parking Lot");
            System.out.println("6. View User Parking History");
            System.out.println("7. Exit");
            System.out.print("Enter choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); 

            switch (choice) {
                case 1:
                    lot.displayAvailability();
                    break;
                case 2: {
                    System.out.print("Enter vehicle license plate: ");
                    String licensePlate = scanner.nextLine();
                    System.out.print("Enter vehicle type (Regular/EV/Motorcycle/Truck): ");
                    String type = scanner.nextLine();
                    System.out.print("Enter number of hours to park: ");
                    int hours = scanner.nextInt();
                    scanner.nextLine();

                    Vehicle vehicle = new Vehicle(licensePlate, type);
                    lot.parkVehicle(vehicle, hours);
                    break;
                }
                case 3: {
                    System.out.print("Enter vehicle license plate to remove: ");
                    String licensePlate = scanner.nextLine();
                    lot.removeVehicle(licensePlate);
                    break;
                }
                case 4:
                    lot.viewAdminReport();
                    break;
                case 5:
                    lot.resetParkingLot();
                    break;
                case 6: {
                    System.out.print("Enter vehicle license plate to view history: ");
                    String licensePlate = scanner.nextLine();
                    lot.displayUserParkingHistory(licensePlate);
                    break;
                }
                case 7:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 7);

        scanner.close();
    }
}
