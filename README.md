java
import java.util.ArrayList;
import java.util.List;
import java.util.Random;
import java.util.Scanner;

class Plant {
    private int id;
    private String name;
    private String description;
    private long timeToHarvest;

    public Plant(int id, String name, String description, long timeToHarvest) {
        this.id = id;
        this.name = name;
        this.description = description;
        this.timeToHarvest = timeToHarvest;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getDescription() {
        return description;
    }

    public long getTimeToHarvest() {
        return timeToHarvest;
    }
}

public class VegetableShop {
    private List<Plant> seedlings;
    private Random random;

    public VegetableShop() {
        seedlings = new ArrayList<>();
        random = new Random();
    }

    public void addPlant(Plant plant) {
        seedlings.add(plant);
    }

    public void viewSeedlings() {
        for (Plant plant : seedlings) {
            System.out.println("id: " + plant.getId());
            System.out.println("name: " + plant.getName());
            System.out.println("description: " + plant.getDescription());
            long timeToHarvestMinutes = plant.getTimeToHarvest();
            long days = timeToHarvestMinutes / (24 * 60);
            long hours = (timeToHarvestMinutes % (24 * 60)) / 60;
            long minutes = (timeToHarvestMinutes % (24 * 60)) % 60;
            System.out.println("time to harvest: " + days + " days, " + hours + " hours, " + minutes + " minutes");
            System.out.println("-----------------------------------------");
        }
    }

    public static void main(String[] args) {
        VegetableShop shop = new VegetableShop();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. view seedlings");
            System.out.println("2. add plant");
            System.out.println("3. exit");
            System.out.print("enter choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    shop.viewSeedlings();
                    break;
                case 2:
                    System.out.print("enter id: ");
                    int id = scanner.nextInt();
                    scanner.nextLine();
                    System.out.print("enter name: ");
                    String name = scanner.nextLine();
                    System.out.print("enter description: ");
                    String description = scanner.nextLine();
                    
                    // Генерация случайного времени созревания от 0 до 15 секунд
                    long timeToHarvest = random.nextInt(16); // от 0 до 15
                    Plant plant = new Plant(id, name, description, timeToHarvest);
                    shop.addPlant(plant);
                    System.out.println("plant added successfully!");
                    break;
                case 3:
                    System.out.println("exiting...");
                    System.exit(0);
                    break;
                default:
                    System.out.println("invalid choice! please try again.");
            }
        }
    }
}
