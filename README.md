import java.util.Scanner;
import java.util.Random;

class TrafficLightController {

    String roadName;
    int vehicles;
    int greenTime;
    String density;

    void analyzeTraffic(int vehicles) {
        this.vehicles = vehicles;

        if (vehicles <= 10) {
            density = "LOW";
            greenTime = 30;
        } else if (vehicles <= 30) {
            density = "MEDIUM";
            greenTime = 45;
        } else {
            density = "HIGH";
            greenTime = 60;
        }
    }

    void displayAnalysis() {
        System.out.println("\n====== TRAFFIC ANALYSIS ======");
        System.out.println("Road Name       : " + roadName);
        System.out.println("Vehicle Count   : " + vehicles);
        System.out.println("Traffic Density : " + density);
        System.out.println("Green Time      : "
                           + greenTime + " seconds");
    }

    void manageSignal() {
        System.out.println("\n====== SIGNAL MANAGEMENT ======");
        System.out.println("Road: " + roadName);
        System.out.println("Signal: GREEN");
        System.out.println("Green Time: " + greenTime + " seconds");
        System.out.println("Signal: YELLOW");
        System.out.println("Signal: RED");
    }
}

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        Random random = new Random();

        System.out.println("======================================");
        System.out.println("       SMART TRAFFIC MANAGEMENT");
        System.out.println("======================================");

        System.out.print("Enter number of roads: ");
        int n = sc.nextInt();
        sc.nextLine();

        if (n <= 0) {
            System.out.println("Invalid number of roads!");
            sc.close();
            return;
        }

        TrafficLightController[] roads =
                new TrafficLightController[n];

        for (int i = 0; i < n; i++) {

            roads[i] = new TrafficLightController();

            System.out.println("\n---------- ROAD " + (i + 1)
                               + " ----------");

            System.out.print("Enter road name: ");
            roads[i].roadName = sc.nextLine();

            System.out.println("1. Manual Traffic Data");
            System.out.println("2. Real-Time Simulation");
            System.out.print("Choose option: ");
            int option = sc.nextInt();

            if (option == 1) {
                System.out.print("Enter number of vehicles: ");
                roads[i].vehicles = sc.nextInt();

                if (roads[i].vehicles < 0) {
                    System.out.println("Invalid vehicle count!");
                    sc.close();
                    return;
                }

            } else if (option == 2) {
                roads[i].vehicles = random.nextInt(51);
                System.out.println("Simulated Vehicles: "
                                   + roads[i].vehicles);

            } else {
                System.out.println("Invalid option!");
                sc.close();
                return;
            }

            sc.nextLine();

            roads[i].analyzeTraffic(roads[i].vehicles);
            roads[i].displayAnalysis();
        }

        for (int i = 0; i < n; i++) {
            roads[i].manageSignal();
        }

        System.out.println("\n======================================");
        System.out.println("Traffic Management Completed!");
        System.out.println("======================================");

        sc.close();
    }
}
