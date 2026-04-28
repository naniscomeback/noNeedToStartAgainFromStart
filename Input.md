## 1. Using Scanner (Most Common)
Scanner is the easiest way to read primitive types (like int, double) and strings.

Java
import java.util.Scanner;
```
public class Main {
    public static void main(String[] args) {
        // Create a Scanner object
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine(); // Reads a full line

        System.out.print("Enter your age: ");
        int age = scanner.nextInt();      // Reads an integer

        System.out.println("Hello " + name + ", you are " + age + " years old.");
        
        scanner.close(); // Good practice to close the scanner
    }
}
```
## 2. Using BufferedReader (Faster)
BufferedReader is faster than Scanner because it has a larger buffer and doesn't do regex parsing. It is preferred for handling large amounts of data.

```
Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException {
        // Wrap System.in in an InputStreamReader and then a BufferedReader
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

        System.out.print("Enter some text: ");
        String input = reader.readLine(); // Always reads as a String

        System.out.println("You typed: " + input);
    }
}
```
## 3. Using System.console() (For Passwords)
If you need to take sensitive input (like a password) where you don't want the text to appear on the screen as you type, use the Console class.

```
Java
import java.io.Console;

public class Main {
    public static void main(String[] args) {
        Console console = System.console();
        
        if (console != null) {
            char[] password = console.readPassword("Enter password: ");
            System.out.println("Password captured securely.");
        } else {
            System.out.println("Console is not available (e.g., in some IDEs).");
        }
    }
}
```


* **`Which one should We can choose?  `**
  
  * Use Scanner if you are writing a small tool, a school project, or need to easily convert input into numbers.

  * Use BufferedReader if you are doing competitive programming or need high-performance I/O.

  * Use System.console() if you are building a secure CLI application that handles passwords.
