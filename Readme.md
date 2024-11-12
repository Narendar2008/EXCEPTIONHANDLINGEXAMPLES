### Common Java Exceptions and Errors

Here’s a list of common exceptions and errors, along with examples:

#### 1. `ArithmeticException`
Occurs when an invalid arithmetic operation is performed, such as division by zero.

```java
public class ArithmeticExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // Throws ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("ArithmeticException caught: " + e.getMessage());
        }
    }
}
```

#### 2. `ArrayIndexOutOfBoundsException`
Occurs when accessing an array element with an invalid index.

```java
public class ArrayIndexExample {
    public static void main(String[] args) {
        try {
            int[] arr = {1, 2, 3};
            int value = arr[5]; // Throws ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("ArrayIndexOutOfBoundsException caught: " + e.getMessage());
        }
    }
}
```

#### 3. `NullPointerException`
Occurs when attempting to use `null` as if it were an object.

```java
public class NullPointerExample {
    public static void main(String[] args) {
        try {
            String str = null;
            str.length(); // Throws NullPointerException
        } catch (NullPointerException e) {
            System.out.println("NullPointerException caught: " + e.getMessage());
        }
    }
}
```

#### 4. `NumberFormatException`
Occurs when attempting to convert a string into a numeric type, and the string is not properly formatted.

```java
public class NumberFormatExample {
    public static void main(String[] args) {
        try {
            int num = Integer.parseInt("abc"); // Throws NumberFormatException
        } catch (NumberFormatException e) {
            System.out.println("NumberFormatException caught: " + e.getMessage());
        }
    }
}
```

#### 5. `ClassCastException`
Occurs when an object is cast to a class it is not an instance of.

```java
public class ClassCastExample {
    public static void main(String[] args) {
        try {
            Object obj = "Hello";
            Integer num = (Integer) obj; // Throws ClassCastException
        } catch (ClassCastException e) {
            System.out.println("ClassCastException caught: " + e.getMessage());
        }
    }
}
```

#### 6. `IOException`
Occurs during input and output operations, typically when file operations fail.

```java
import java.io.*;

public class IOExceptionExample {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("nonexistent.txt"); // Throws IOException
        } catch (IOException e) {
            System.out.println("IOException caught: " + e.getMessage());
        }
    }
}
```

#### 7. `FileNotFoundException`
A subclass of `IOException`, occurs when a file is not found.

```java
import java.io.*;

public class FileNotFoundExceptionExample {
    public static void main(String[] args) {
        try {
            FileInputStream file = new FileInputStream("missingfile.txt"); // Throws FileNotFoundException
        } catch (FileNotFoundException e) {
            System.out.println("FileNotFoundException caught: " + e.getMessage());
        }
    }
}
```

#### 8. `OutOfMemoryError`
Occurs when the JVM runs out of memory.

```java
public class OutOfMemoryErrorExample {
    public static void main(String[] args) {
        try {
            int[] arr = new int[Integer.MAX_VALUE]; // Throws OutOfMemoryError
        } catch (OutOfMemoryError e) {
            System.out.println("OutOfMemoryError caught: " + e.getMessage());
        }
    }
}
```

#### 9. `StackOverflowError`
Occurs when there is an infinite recursion, causing the stack to overflow.

```java
public class StackOverflowExample {
    public static void main(String[] args) {
        try {
            recursiveMethod(); // Throws StackOverflowError
        } catch (StackOverflowError e) {
            System.out.println("StackOverflowError caught: " + e.getMessage());
        }
    }

    public static void recursiveMethod() {
        recursiveMethod(); // Infinite recursion
    }
}
```

#### 10. `IllegalArgumentException`
Thrown when a method receives an invalid argument.

```java
public class IllegalArgumentExample {
    public static void main(String[] args) {
        try {
            Thread.sleep(-100); // Throws IllegalArgumentException
        } catch (IllegalArgumentException | InterruptedException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```

### Advanced Exception Handling Concepts

1. **Custom Exceptions**: Sometimes, predefined exceptions do not cover specific use cases in your application. You can create custom exceptions by extending the `Exception` or `RuntimeException` class.
   
   ```java
   // Custom checked exception
   public class InvalidAgeException extends Exception {
       public InvalidAgeException(String message) {
           super(message);
       }
   }

   public class CustomExceptionExample {
       public static void main(String[] args) {
           try {
               validateAge(15); // Throws InvalidAgeException
           } catch (InvalidAgeException e) {
               System.out.println("Exception caught: " + e.getMessage());
           }
       }

       public static void validateAge(int age) throws InvalidAgeException {
           if (age < 18) {
               throw new InvalidAgeException("Age must be 18 or older.");
           }
       }
   }
   ```

2. **Multiple Catch Blocks**: You can handle multiple exceptions in a single `try` block with multiple `catch` blocks. Starting from Java 7, you can catch multiple exceptions in a single `catch` by separating them with a pipe (`|`).

   ```java
   public class MultipleCatchExample {
       public static void main(String[] args) {
           try {
               int arr[] = new int[5];
               arr[10] = 100; // ArrayIndexOutOfBoundsException
               int result = 10 / 0; // ArithmeticException
           } catch (ArrayIndexOutOfBoundsException | ArithmeticException e) {
               System.out.println("Exception caught: " + e.getMessage());
           }
       }
   }
   ```

3. **Throwing Exceptions in Methods**: The `throws` keyword in the method signature declares the exceptions that a method can throw, allowing the caller to handle them.

   ```java
   public class ThrowsExample {
       public static void main(String[] args) {
           try {
               readFile();
           } catch (IOException e) {
               System.out.println("IOException caught: " + e.getMessage());
           }
       }

       public static void readFile() throws IOException {
           FileReader file = new FileReader("nonexistent.txt"); // IOException
       }
   }
   ```

4. **Nested `try-catch` Blocks**: You can place `try-catch` blocks inside other `try-catch` blocks, which is helpful for handling exceptions in complex code structures.

   ```java
   public class NestedTryExample {
       public static void main(String[] args) {
           try {
               int arr[] = new int[3];
               try {
                   int result = arr[5] / 0; // Throws ArrayIndexOutOfBoundsException
               } catch (ArithmeticException e) {
                   System.out.println("ArithmeticException caught: " + e.getMessage());
               }
           } catch (ArrayIndexOutOfBoundsException e) {
               System.out.println("ArrayIndexOutOfBoundsException caught: " + e.getMessage());
           }
       }
   }
   ```

5. **Try-With-Resources**: Introduced in Java 7, `try-with-resources` is a feature that automatically closes resources like files or database connections after usage, even if an exception occurs.

   ```java
   import java.io.*;

   public class TryWithResourcesExample {
       public static void main(String[] args) {
           try (BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
               String line;
               while ((line = br.readLine()) != null) {
                   System.out.println(line);
               }
           } catch (IOException e) {
               System.out.println("IOException caught: " + e.getMessage());
           }
       }
   }
   ```


#### 11. `IllegalStateException`
Occurs when a method is invoked at an inappropriate time, often in an invalid object state.

```java
import java.util.ArrayList;
import java.util.Iterator;

public class IllegalStateExample {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("Item1");
        list.add("Item2");
        
        Iterator<String> iterator = list.iterator();
        iterator.next();
        iterator.remove(); // Valid remove

        iterator.remove(); // Throws IllegalStateException because next() was not called
    }
}
```

#### 12. `UnsupportedOperationException`
Occurs when a requested operation is not supported by the target.

```java
import java.util.*;

public class UnsupportedOperationExample {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("A", "B", "C");
        
        try {
            list.add("D"); // Throws UnsupportedOperationException
        } catch (UnsupportedOperationException e) {
            System.out.println("UnsupportedOperationException caught: " + e.getMessage());
        }
    }
}
```

#### 13. `IndexOutOfBoundsException`
Occurs when an invalid index is used for an array or list.

```java
import java.util.ArrayList;

public class IndexOutOfBoundsExample {
    public static void main(String[] args) {
        try {
            ArrayList<String> list = new ArrayList<>();
            list.add("Element");
            list.get(10); // Throws IndexOutOfBoundsException
        } catch (IndexOutOfBoundsException e) {
            System.out.println("IndexOutOfBoundsException caught: " + e.getMessage());
        }
    }
}
```

#### 14. `NoSuchElementException`
Occurs when attempting to access an element in an empty data structure.

```java
import java.util.*;

public class NoSuchElementExample {
    public static void main(String[] args) {
        try {
            ArrayList<String> list = new ArrayList<>();
            Iterator<String> iterator = list.iterator();
            iterator.next(); // Throws NoSuchElementException
        } catch (NoSuchElementException e) {
            System.out.println("NoSuchElementException caught: " + e.getMessage());
        }
    }
}
```

#### 15. `InterruptedException`
Occurs when a thread is interrupted while it is sleeping, waiting, or otherwise paused.

```java
public class InterruptedExample {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                System.out.println("InterruptedException caught: " + e.getMessage());
            }
        });

        thread.start();
        thread.interrupt(); // Causes InterruptedException
    }
}
```

#### 16. `ConcurrentModificationException`
Occurs when trying to modify a collection while iterating over it using an iterator.

```java
import java.util.ArrayList;
import java.util.Iterator;

public class ConcurrentModificationExample {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");

        try {
            for (String s : list) {
                if (s.equals("A")) {
                    list.remove(s); // Throws ConcurrentModificationException
                }
            }
        } catch (ConcurrentModificationException e) {
            System.out.println("ConcurrentModificationException caught: " + e.getMessage());
        }
    }
}
```

### Exception Chaining

Exception chaining is useful when one exception causes another exception. You can chain exceptions by passing one exception to the constructor of another.

```java
public class ExceptionChainingExample {
    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            System.out.println("Exception caught: " + e.getMessage());
            e.printStackTrace();
        }
    }

    public static void method1() throws Exception {
        try {
            int result = 10 / 0; // Throws ArithmeticException
        } catch (ArithmeticException e) {
            throw new Exception("Exception in method1", e); // Exception chaining
        }
    }
}
```

# **FinallyExample**
```java
import java.io.*;

public class FinallyExample {
    public static void main(String[] args) {
        BufferedReader reader = null;
        
        try {
            reader = new BufferedReader(new FileReader("test.txt"));
            System.out.println("File opened successfully.");
            String line = reader.readLine(); // Reading the first line
            System.out.println("Read line: " + line);
            
            // Simulating an exception
            int result = 10 / 0;
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("IOException occurred: " + e.getMessage());
        } catch (ArithmeticException e) {
            System.out.println("Arithmetic exception: " + e.getMessage());
        } finally {
            // Closing the file in finally block
            try {
                if (reader != null) {
                    reader.close();
                    System.out.println("File closed.");
                }
            } catch (IOException e) {
                System.out.println("Failed to close the file: " + e.getMessage());
            }
        }
    }
}

```
