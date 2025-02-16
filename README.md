import java.util.Scanner;

public class Student {

static final int MAX_GRADES = 5;
static int studentCount = 0;
String name;
int[] grades;
int gradeCount;

    public Student(String name) {
        this.name = name;
        this.grades = new int[MAX_GRADES];
        this.gradeCount = 0;
        studentCount++;
    }

    public void addGrade(int grade) {
        if (gradeCount < MAX_GRADES) {
            grades[gradeCount] = grade;
            gradeCount++;
        } else {
            System.out.println("Cannot add more than " + MAX_GRADES + " grades for " + name);
        }
    }

    public double calculateAverage() {
        if (gradeCount == 0) {
            return 0.0;
        }
        int sum = 0;
        int i = 0;
        while (i < gradeCount) {
            sum += grades[i];
            i++;
        }
        return (double) sum / gradeCount;
    }

    public void displayInfo() {
        System.out.print("Student Name: " + name + "\nGrades: ");
        int i = 0;
        while (i < gradeCount) {
            System.out.print(grades[i] + " ");
            i++;
        }
        System.out.println("\nAverage Grade: " + calculateAverage());
    }

    public static int getStudentCount() {
        return studentCount;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter number of students: ");
        int numStudents = scanner.nextInt();
        scanner.nextLine();

        Student[] students = new Student[numStudents];

        int i = 0;
        while (i < numStudents) {
            System.out.print("Enter name for student " + (i + 1) + ": ");
            String name = scanner.nextLine();
            students[i] = new Student(name);
            
            int j = 0;
            while (j < MAX_GRADES) {
                System.out.print("Enter grade " + (j + 1) + " for " + name + ": ");
                int grade = scanner.nextInt();
                students[i].addGrade(grade);
                j++;
            }
            System.out.println("\n");
            scanner.nextLine();
            i++;
        }

        System.out.println("\nTotal students: " + Student.getStudentCount());

        i = 0;
        while (i < students.length) {
            students[i].displayInfo();
            System.out.println();
            i++;
        }

        scanner.close();
    }
}
