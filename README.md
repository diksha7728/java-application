import java.util.*;

public class CourseManagementSystem {

    static class Course {
        private static int idCounter = 1;
        private int id;
        private String courseName;
        private double fee;
        private String instructor;

        public Course(String courseName, double fee, String instructor) {
            this.id = idCounter++;
            this.courseName = courseName;
            this.fee = fee;
            this.instructor = instructor;
        }

        // Getters and Setters
        public int getId() {
            return id;
        }

        public String getCourseName() {
            return courseName;
        }

        public void setCourseName(String courseName) {
            this.courseName = courseName;
        }

        public double getFee() {
            return fee;
        }

        public void setFee(double fee) {
            this.fee = fee;
        }

        public String getInstructor() {
            return instructor;
        }

        public void setInstructor(String instructor) {
            this.instructor = instructor;
        }

        @Override
        public String toString() {
            return "Course{" +
                    "id=" + id +
                    ", courseName='" + courseName + '\'' +
                    ", fee=" + fee +
                    ", instructor='" + instructor + '\'' +
                    '}';
        }
    }

    private static List<Course> courses = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\nCourse Management System");
            System.out.println("1. Add Course");
            System.out.println("2. View All Courses");
            System.out.println("3. Update Course Details");
            System.out.println("4. Delete Course");
            System.out.println("5. Retrieve Courses by Instructor");
            System.out.println("6. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    addCourse(scanner);
                    break;
                case 2:
                    viewAllCourses();
                    break;
                case 3:
                    updateCourse(scanner);
                    break;
                case 4:
                    deleteCourse(scanner);
                    break;
                case 5:
                    retrieveByInstructor(scanner);
                    break;
                case 6:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice.");
            }
        } while (choice != 6);
    }

    private static void addCourse(Scanner scanner) {
        System.out.print("Enter Course Name: ");
        String name = scanner.next();
        System.out.print("Enter Course Fee: ");
        double fee = scanner.nextDouble();
        System.out.print("Enter Instructor Name: ");
        String instructor = scanner.next();
        Course course = new Course(name, fee, instructor);
        courses.add(course);
        System.out.println("Course added successfully!");
    }

    private static void viewAllCourses() {
        if (courses.isEmpty()) {
            System.out.println("No courses found.");
        } else {
            System.out.println("----------------------------------");
            System.out.println("ID\tName\t\tFee\tInstructor");
            System.out.println("----------------------------------");
            for (Course course : courses) {
                System.out.println(course.getId() + "\t" + course.getCourseName() + "\t" + course.getFee() + "\t" + course.getInstructor());
            }
        }
    }

    private static void updateCourse(Scanner scanner) {
        System.out.print("Enter Course ID to update: ");
        int id = scanner.nextInt();
        for (Course course : courses) {
            if (course.getId() == id) {
                System.out.print("Enter new Course Name: ");
                String newName = scanner.next();
                System.out.print("Enter new Course Fee: ");
                double newFee = scanner.nextDouble();
                System.out.print("Enter new Instructor Name: ");
                String newInstructor = scanner.next();
                course.setCourseName(newName);
                course.setFee(newFee);
                course.setInstructor(newInstructor);
                System.out.println("Course updated successfully!");
                return;
            }
        }
        System.out.println("Course not found.");
    }

    private static void deleteCourse(Scanner scanner) {
        System.out.print("Enter Course ID to delete: ");
        int id = scanner.nextInt();
        courses.removeIf(course -> course.getId() == id);
        System.out.println("Course deleted successfully!");
    }

    private static void retrieveByInstructor(Scanner scanner) {
        System.out.print("Enter Instructor Name: ");
        String instructorName = scanner.next();
        List<Course> instructorCourses = new ArrayList<>();
        for (Course course : courses) {
            if (course.getInstructor().equalsIgnoreCase(instructorName)) {
                instructorCourses.add(course);
            }
        }
        if (instructorCourses.isEmpty()) {
            System.out.println("No courses found for the given instructor.");
        } else {
            System.out.println("Courses taught by " + instructorName + ":");
            for (Course course : instructorCourses) {
                System.out.println(course);
            }
        }
    }
}
