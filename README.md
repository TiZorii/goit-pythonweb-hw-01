# Topic 1: Homework

It's time to put theory into practice. The homework consists of two tasks.

For both tasks, you must apply typing. Instead of using the `print` operator, use logging at the INFO level. Use the `black` formatter for code formatting.

---

## Technical Description of the Tasks

### Task 1: Factory Pattern

The following code represents a simple system for creating vehicles. We have two classes: `Car` and `Motorcycle`. Each class has a method `start_engine()` that simulates starting the engine of the respective vehicle. Currently, to create a new vehicle, we instantiate the appropriate class with the specified make and model.

```python
class Car:
    def __init__(self, make, model):
        self.make = make
        self.model = model

    def start_engine(self):
        print(f"{self.make} {self.model}: Engine started")

class Motorcycle:
    def __init__(self, make, model):
        self.make = make
        self.model = model

    def start_engine(self):
        print(f"{self.make} {self.model}: Engine started")

# Usage
vehicle1 = Car("Toyota", "Corolla")
vehicle1.start_engine()

vehicle2 = Motorcycle("Harley-Davidson", "Sportster")
vehicle2.start_engine()
```
### Next Steps: Creating Region-Specific Vehicles

The next step is to create vehicles that account for regional specifications, such as US Spec for the United States or EU Spec for Europe.

#### Task Objective

Implement the Factory pattern to enable the creation of vehicles with different regional specifications without modifying the main vehicle classes.

#### Steps for Task 1

1. Create an abstract base class `Vehicle` with the method `start_engine()`.
2. Update the `Car` and `Motorcycle` classes to inherit from `Vehicle`.
3. Create an abstract class `VehicleFactory` with methods `create_car()` and `create_motorcycle()`.
4. Implement two factory classes: `USVehicleFactory` and `EUVehicleFactory`. These factories should create cars and motorcycles with region-specific identifiers, e.g., `Ford Mustang (US Spec)` for the United States.
5. Update the initial code to use the factories for vehicle creation.

#### Expected Outcome

A codebase that allows the easy creation of vehicles for different regions using the corresponding factories.

---

### Task 2: Refactoring to Adhere to SOLID Principles

You are provided with a simplified library management program that allows users to add new books, remove books, and display all books in the library. The user interacts with the program through the command line using the commands `add`, `remove`, `show`, and `exit`.

```python
class Library:
    def __init__(self):
        self.books = []

    def add_book(self, title, author, year):
        book = {
            "title": title,
            "author": author,
            "year": year
        }
        self.books.append(book)

    def remove_book(self, title):
        for book in self.books:
            if book["title"] == title:
                self.books.remove(book)
                break

    def show_books(self):
        for book in self.books:
            print(f'Title: {book["title"]}, Author: {book["author"]}, Year: {book["year"]}')

def main():
    library = Library()
    
    while True:
        command = input("Enter command (add, remove, show, exit): ").strip().lower()
        
        if command == "add":
            title = input("Enter book title: ").strip()
            author = input("Enter book author: ").strip()
            year = input("Enter book year: ").strip()
            library.add_book(title, author, year)
        elif command == "remove":
            title = input("Enter book title to remove: ").strip()
            library.remove_book(title)
        elif command == "show":
            library.show_books()
        elif command == "exit":
            break
        else:
            print("Invalid command. Please try again.")

if __name__ == "__main__":
    main()
```
### Your Task: Refactor the Code to Follow SOLID Principles

#### Steps to Complete Task 2:

1. **Single Responsibility Principle (SRP)**:  
   Create a `Book` class to handle the storage of book information.

2. **Open/Closed Principle (OCP)**:  
   Design the `Library` class to allow for extension with new functionality without modifying its existing code.

3. **Liskov Substitution Principle (LSP)**:  
   Ensure that any class inheriting from the `LibraryInterface` can replace the `Library` class without breaking the program's functionality.

4. **Interface Segregation Principle (ISP)**:  
   Use the `LibraryInterface` to clearly define the methods required for working with the library.

5. **Dependency Inversion Principle (DIP)**:  
   Ensure that high-level classes, such as `LibraryManager`, depend on abstractions (interfaces) rather than concrete implementations.

#### Refactored Code:

```python
from abc import ABC, abstractmethod

class Book:
    pass

class LibraryInterface(ABC):
    pass

class Library(LibraryInterface):
    pass

class LibraryManager:
    pass

def main():
    library = Library()
    manager = LibraryManager(library)

    while True:
        command = input("Enter command (add, remove, show, exit): ").strip().lower()

        match command:
            case "add":
                title = input("Enter book title: ").strip()
                author = input("Enter book author: ").strip()
                year = input("Enter book year: ").strip()
                manager.add_book(title, author, year)
            case "remove":
                title = input("Enter book title to remove: ").strip()
                manager.remove_book(title)
            case "show":
                manager.show_books()
            case "exit":
                break
            case _:
                print("Invalid command. Please try again.")

if __name__ == "__main__":
    main()
```
