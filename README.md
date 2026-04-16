https://onecompiler.com/java/44kh65pgh
MCQ Q1 ANS.import java.util.*;

class Student {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // Required for HashMap key comparison
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (!(obj instanceof Student)) return false;
        Student s = (Student) obj;
        return id == s.id;
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}

class Course {
    String courseName;

    Course(String courseName) {
        this.courseName = courseName;
    }
}

public class Main {
    public static void main(String[] args) {

        // Key: Student, Value: List of Courses
        HashMap<Student, ArrayList<Course>> map = new HashMap<>();

        Student s1 = new Student(1, "Amit");
        Student s2 = new Student(2, "Riya");

        map.put(s1, new ArrayList<>());
        map.put(s2, new ArrayList<>());

        map.get(s1).add(new Course("Math"));
        map.get(s1).add(new Course("Science"));

        map.get(s2).add(new Course("English"));

        // Display data
        for (Student s : map.keySet()) {
            System.out.print(s.name + " enrolled in: ");
            for (Course c : map.get(s)) {
                System.out.print(c.courseName + " ");
            }
            System.out.println();
        }
    }
}
MCQ Q2 ANS.
class InvalidFeeException extends Exception {
    public InvalidFeeException(String message) {
        super(message);
    }
}

class Course {
    String name;
    double fee;

    Course(String name, double fee) throws InvalidFeeException {
        if (fee < 0) {
            throw new InvalidFeeException("Course fee cannot be negative!");
        }
        this.name = name;
        this.fee = fee;
    }

    void display() {
        System.out.println("Course: " + name + ", Fee: " + fee);
    }
}

public class Main {
    public static void main(String[] args) {

        try {
            Course c1 = new Course("Java Programming", -3000);
            c1.display();
        } catch (InvalidFeeException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }

        try {
            Course c2 = new Course("Python Programming", 5000);
            c2.display();
        } catch (InvalidFeeException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
MCQ Q3 ANS.
import java.util.*;

class EnrollmentSystem {

    // Thread-safe list
    private List<String> enrollments = Collections.synchronizedList(new ArrayList<>());

    public void addStudent(String studentName) {
        enrollments.add(studentName);
    }

    public void display() {
        synchronized (enrollments) {
            for (String s : enrollments) {
                System.out.println(s);
            }
        }
    }
}

class EnrollmentThread extends Thread {
    EnrollmentSystem system;
    String studentName;

    EnrollmentThread(EnrollmentSystem system, String studentName) {
        this.system = system;
        this.studentName = studentName;
    }

    public void run() {
        system.addStudent(studentName);
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {

        EnrollmentSystem system = new EnrollmentSystem();

        Thread t1 = new EnrollmentThread(system, "Amit");
        Thread t2 = new EnrollmentThread(system, "Riya");
        Thread t3 = new EnrollmentThread(system, "John");

        t1.start();
        t2.start();
        t3.start();

        t1.join();
        t2.join();
        t3.join();

        System.out.println("Enrolled Students:");
        system.display();
    }
}
MCQ Q4 ANS.
interface Course {
    double calculateFee();
}

class RegularCourse implements Course {
    double baseFee;

    RegularCourse(double baseFee) {
        this.baseFee = baseFee;
    }

    public double calculateFee() {
        return baseFee;
    }
}

class AdvancedCourse implements Course {
    double baseFee;

    AdvancedCourse(double baseFee) {
        this.baseFee = baseFee;
    }

    public double calculateFee() {
        return baseFee + 2000; // extra fee
    }
}

public class Main {
    public static void main(String[] args) {

        Course c1 = new RegularCourse(5000);
        Course c2 = new AdvancedCourse(5000);

        System.out.println("Regular Course Fee: " + c1.calculateFee());
        System.out.println("Advanced Course Fee: " + c2.calculateFee());
    }
}
