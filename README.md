# Scope

## Learning Goals

- Explain scope in Java.

## Introduction

We have seen several examples where new curly brace blocks can be defined, and
every time a new set of matching `{` and `}` is created, it defines a new
**scope**. This means that the variables that are defined inside that scope are
only known to that scope.

## Scope Walkthrough

Let's look at the following example code:

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class Main {  // <-- first scope

  public static int add(int x, int y) {  // <-- second scope
    int sum;    // method level variable
    sum = x + y;
    return sum;
  }  // <-- end of second scope

  public static void printMenu() {  // <-- third scope
    System.out.println("What operation would you like to perform?");
    System.out.println("0. Exit");
    System.out.println("1. Add.");
  }  // <-- end of third scope

  public static void main(String[] args) {  // <-- fourth scope
    Scanner scanner = new Scanner(System.in);

    int choice = 0;

    do {  // <-- fifth scope
      // Prompt the user to select a menu item
      printMenu();

      try {  // <-- sixth scope
        choice = scanner.nextInt();

        if (choice == 0) {  // <-- seventh scope
          System.out.println("Goodbye!");
        }  // <-- end of seventh scope
        else if (choice == 1) {  // <-- eighth scope
          System.out.println("Let's add 2 and 5!");
          int result = add(2, 5);
          System.out.println("The sum is " + result);
        } // <-- end of eighth scope
        else {  // <-- ninth scope
          System.out.println("Sorry that wasn't an option.");
        }  // <-- end of ninth scope

      }  // <-- end of sixth scope
      catch (InputMismatchException exception) {  // <-- tenth scope
        System.out.println("Invalid input");
      }  // <-- end of tenth scope
    } while (choice != 0);  // <-- end of fifth scope
  }  // <-- end of fourth scope
}  // <-- end of first scope
```

As we discussed before, curly brace "blocks" can be contained inside each other
like Russian dolls, which is the case here:

- The first scope is the top level scope, which means nothing can be defined
  outside it for our program.
- The second scope is inside the first scope, which means the second scope has
  access to all the variables defined in the first scope.
  - Notice the method level variable, `sum`. The `sum` variable is only
    accessible within the method, `add`, inside this second scope. We cannot
    access it from the first scope.
- The third scope is inside the first scope and a peer to the second scope. This
  means they cannot see each other's variables, but it can access any variables
  defined in the first scope.
- The fourth scope is inside the first scope and a peer to the second and third
  scopes.
- The fifth scope is inside the fourth scope, which means the fifth scope has
  access to all the variables defined in the fourth scope, including the ones
  defined in the first scope.
  - Notice that the `scanner` is defined in the `main()` method. The fifth scope
    takes us into the `do-while` loop and still can access the `scanner`
    variable. This is because the `do-while` loop's scope has access to the
    variables within the `main()` method's scope.
- The sixth scope is inside the fifth scope, which means the sixth scope has
  access to all the variables defined in the fifth scope.
  - This includes the `scanner` variable still since the fifth scope has access
    to the scope where the `scanner` was declared.
- The seventh, eighth, and ninth scopes are all inside the sixth scope and are
  peers to one another. This means they cannot see each other's variables. A
  scope can only see its variables and the variables of all the scopes inside
  it.
  - Notice each conditional block has its own scope. The `result` variable
    within the `else if` block is not accessible from the `if` or the `else`
    block since it is only in scope of the `else if` block.
- The tenth scope is inside the fifth scope and is a peer with the sixth scope.
  - Notice that the `try` and the `catch` block are also individual scopes.

In the example above, the variables are only accessible inside the scope it is
defined in and the other scopes inside it. As we saw with the `scanner` and
`choice` variables, we can access those from the inner scopes. The variables are
**local** to the scope they are defined in. This is why we can call them **local
variables**.

## Conclusion

As we have seen, every time we have a new set of curly braces `{ }`, we are
opening up a new scope. When we do this, it means that the variables that are
defined inside that method, loop, or conditional are only known to that scope
and any inner scopes.
