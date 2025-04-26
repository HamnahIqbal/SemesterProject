//# SemesterProject
package cscorner;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
class Man {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public void login() {
        System.out.println(name + " has logged in successfully!");
    }
}
class User extends Man {
    private WorkoutPlan workoutPlan;
    public WorkoutPlan getWorkoutPlan() {
        return workoutPlan;
    }
    public void setWorkoutPlan(WorkoutPlan workoutPlan) {
        this.workoutPlan = workoutPlan;
    }
}
class Trainer extends Man{
    private List<User> clients = new ArrayList<>();
    public void addClient(User user) {
        clients.add(user);
        System.out.println(user.getName() + " has been added as a client.");
    }
}
class WorkoutPlan {
    private String planName;
    private List<WorkoutSession> sessions = new ArrayList<>();
    public String getPlanName() {
        return planName;
    }
    public void setPlanName(String planName) {
        this.planName = planName;
    }
    public List<WorkoutSession> getSessions() {
        return sessions;
    }
    public void addSession(WorkoutSession session) {
        sessions.add(session);
    }
}
class WorkoutSession {
    private String type;
    private int duration;
    private int caloriesBurned;
public String getType() {
        return type;
    }
    public void setType(String type) {
        this.type = type;
    }
    public int getDuration() {
        return duration;
    }
public void setDuration(int duration) {
        this.duration = duration;
    }
    public int getCaloriesBurned() {
        return caloriesBurned;
    }
 public void setCaloriesBurned(int caloriesBurned) {
        this.caloriesBurned = caloriesBurned;
    }
}
public class FitnessApp {
    private static final Scanner scanner = new Scanner(System.in);
 public static void main(String[] args) {
        boolean continueProgramme = true;
while (continueProgramme) {
            runFitnessApp();
            continueProgramme = askToContinue();
        }
 System.out.println("Thank you for using the Fitness App. Goodbye!");
        scanner.close();
    }
 private static void runFitnessApp() {
        User user = createUser();
        Trainer trainer = createTrainer();
 user.login();
        trainer.login();
 trainer.addClient(user);
 createAndDisplayWorkoutPlan(user);
    }
 private static User createUser() {
        System.out.print("Enter User Name: ");
        String userName = scanner.nextLine();
        User user = new User();
        user.setName(userName);
        return user;
    }
 private static Trainer createTrainer() {
        System.out.print("Enter Trainer Name: ");
        String trainerName = scanner.nextLine();
        Trainer trainer = new Trainer();
        trainer.setName(trainerName);
        return trainer;
    }
 private static void createAndDisplayWorkoutPlan(User user) {
        System.out.print("Enter Workout Plan Name: ");
        String workoutPlanName = scanner.nextLine();
        WorkoutPlan workoutPlan = new WorkoutPlan();
        workoutPlan.setPlanName(workoutPlanName);
        user.setWorkoutPlan(workoutPlan);
 int sessionCount = getValidIntInput("How many workout sessions to add? ");
for (int i = 0; i < sessionCount; i++) {
            WorkoutSession session = createWorkoutSession();
            workoutPlan.addSession(session);
        }
displayWorkoutPlan(workoutPlan);
    }
private static WorkoutSession createWorkoutSession() {
        WorkoutSession session = new WorkoutSession();
 System.out.print("Enter Session Type (e.g., Cardio, Strength): ");
        session.setType(scanner.nextLine());
        session.setDuration(getValidIntInput("Enter Session Duration (minutes): "));
        session.setCaloriesBurned(getValidIntInput("Enter Calories Burned in Session: "));
 return session;
    }
private static void displayWorkoutPlan(WorkoutPlan workoutPlan) {
        System.out.println("\nWorkout Plan: " + workoutPlan.getPlanName());
        for (WorkoutSession ws : workoutPlan.getSessions()) {
            System.out.println("Session Type: " + ws.getType());
            System.out.println("Duration: " + ws.getDuration() + " minutes");
            System.out.println("Calories Burned: " + ws.getCaloriesBurned());
            System.out.println();
        }
    }
    private static boolean askToContinue() {
        while (true) {
            System.out.print("Do you want to log in another user? (yes/no): ");
            String response = scanner.nextLine().toLowerCase();
            if (response.equals("yes")) {
                return true;
            } else if (response.equals("no")) {
                return false;
            } else {
                System.out.println("Invalid input. Please enter 'yes' or 'no'.");
            }
        }
    }
    private static int getValidIntInput(String prompt) {
        while (true) {
            try {
                System.out.print(prompt);
                return Integer.parseInt(scanner.nextLine());
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a valid number.");
            }
        }
    }
}
