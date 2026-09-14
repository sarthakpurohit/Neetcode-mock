1 - Classes And Objects

0 Intro to Classes
Imagine you're a game developer creating a superhero game. You start by defining individual heroes:

hero_1_name = "Iron Man"
hero_1_power = "repulsor beams"
hero_1_health = 100
hero_1_speed = 80

hero_2_name = "Spider Man"
hero_2_power = "web slinging"
hero_2_health = 90
hero_2_speed = 95
This approach has a few problems:

Repetition: You have to define each hero individually.
Messy code: It's hard to keep track of all the hero attributes and their values.
Scalability: What if you need to create 50 different heroes? Your code would become unmanageable very quickly.
Classes
A class is a blueprint for creating objects. Here's the basic syntax for defining a class in Python:

class SuperHero:
    def __init__(self, name: str, power: str, health: int, speed: int):
        self.name = name
        self.power = power
        self.health = health
        self.speed = speed
In Python, a class is defined with the keyword word class followed by the name of the class and a colon. The __init__ method is a special method that belongs to the class. It creates an object and initializes it's attributes.

Notice that the __init__ method has an argument self. This is required. The self variable allows us to add attributes to our object. It also prevents name conflicts, since name and self.name are different variables.

Challenge
Please see the starter code on the right and complete the following tasks:

Define a class named Pet.
Define a method for initialization: def __init__(self, name, species)
Inside the __init__ method, initialize two attributes:
self.name: assigned the value of the name parameter
self.species: assigned the value of the species parameter

What is the self argument?
In Python, self represents the instance of the class. It's used to access variables and methods associated with the class. When you create an object from a class, Python automatically passes the object as the first argument to the __init__ method. You can name this argument anything you like, but self is the convention.

Don't worry if this doesn't make sense right now. We'll cover it in more detail in the upcoming lessons.


How to name classes in Python?
Class names in Python use PascalCase convention, meaning each word starts with a capital letter and there are no underscores between words (e.g., SuperHero, IronMan, SpiderMan).

Starter Code:





# Do not modify below this line
my_pet = Pet("Fluffy", "cat")
print(f"My pet is a {my_pet.species} named {my_pet.name}")


Solution:
class Pet:
    def __init__(self, name: str, species: str):
        self.name = name
        self.species = species


# Do not modify below this line
my_pet = Pet("Fluffy", "cat")
print(f"My pet is a {my_pet.species} named {my_pet.name}")


1 What are Objects?
An object is an instance of a class. It's a specific item created using the blueprint defined by the class.

Creating Objects
We have seen the class definition for a SuperHero before.

class SuperHero:
    def __init__(self, name: str, power: str, health: int, speed: int):
        self.name = name
        self.power = power
        self.health = health
        self.speed = speed
We can create an object by calling the class and passing in the required arguments.

# Creating superhero objects
iron_man = SuperHero("Iron Man", "repulsor beams", 100, 80)
spider_man = SuperHero("Spider Man", "web slinging", 90, 95)
When we write iron_man = SuperHero("Iron Man", "repulsor beams", 100, 80), we're telling Python:

Create a new object variable called iron_man
Use the SuperHero class to create it
Set its name attribute to "Iron Man"
Set its power attribute to "repulsor beams"
Set its health attribute to 100
Set its speed attribute to 80
Challenge
You have given the code for a Pet class. When run, this code produces an error:

NameError: name 'whiskers' is not defined
To fix this error and get the expected output, complete the following task:

Create a pet with a name of Whiskers, which is a cat with hunger level 6 and energy level 8.
Note: The name of the variable should be whiskers (no uppercase).
Expected Output:

Whiskers (cat) - Hunger: 6, Energy: 8

Hint
Object creation: pet_name = Pet("Name", "species", hunger_value, energy_value)

The importance of parameter order
When creating a new superhero object, the order of values must match the __init__ method:

def __init__(self, name, power, health, speed)
Example:

Correct order
correct_hero = SuperHero("Captain America", "super strength", 110, 85)
Incorrect order
incorrect_hero = SuperHero(100, "Hulk", 75, "gamma radiation")
In the incorrect example, the order of attributes is mismatched. Be careful, Python won't give us any errors for this incorrect order, which means we need to be careful when creating our objects!

Starter Code:
class Pet:
    def __init__(self, name: str, species: str, hunger: int, energy: int):
        self.name = name
        self.species = species
        self.hunger = hunger
        self.energy = energy

# Don't modify the above code

# TODO: Create a pet named "Whiskers" that is a species of 'cat' with hunger level 6 and energy level 8


# Don't modify the following code
print(f"{whiskers.name} ({whiskers.species}) - Hunger: {whiskers.hunger}, Energy: {whiskers.energy}") 


Solution:
class Pet:
    def __init__(self, name: str, species: str, hunger: int, energy: int):
        self.name = name
        self.species = species
        self.hunger = hunger
        self.energy = energy

whiskers = Pet("Whiskers", "cat", 6, 8)

print(f"{whiskers.name} ({whiskers.species}) - Hunger: {whiskers.hunger}, Energy: {whiskers.energy}")


2 Object Attributes
Attributes are the properties that define or belong to an object. In our superhero example, we have the following attributes for a superhero: name, power, health, and speed.

Accessing Attributes
To access an object's attributes, we use dot notation: object_name.attribute_name. Let's create a superhero and access its attributes:

class SuperHero:
    def __init__(self, name: str, power: str, health: int, speed: int):
        self.name = name
        self.power = power
        self.health = health
        self.speed = speed

iron_man = SuperHero("Iron Man", "repulsor beams", 100, 80)

print(iron_man.name)    # Iron Man
print(iron_man.power)   # repulsor beams
Modifying Attributes
We can also modify an attribute's value using the same dot notation:

iron_man.health = 90
iron_man.power = "advanced repulsor technology"

print(iron_man.health)  # 90
print(iron_man.power)   # advanced repulsor technology
Attribute Types
While Python won't give us any errors when changing the data type of an attribute, we should avoid doing so to avoid unexpected behavior.

iron_man.name = 42       # Allowed but bad practice
iron_man.health = "full" # Allowed but bad practice
Challenge
You are given a Pet class and an object from that class whiskers.

Print the attributes of whiskers with the formatting below.
Decrease the hunger attribute by 3, and increase the energy attribute by 2.
Print the attributes of whiskers again with the formatting below.
Expected Output:

Initial Attributes: Whiskers (cat) - Hunger: 6, Energy: 8
Modified Attributes: Whiskers (cat) - Hunger: 3, Energy: 10

Hints
Access: pet_object.attribute
Modify: pet_object.attribute = new_value or pet_object.attribute += value
Print: f"Attributes: {pet_object.name} ({pet_object.species}) - Hunger: {pet_object.hunger}, Energy: {pet_object.energy}"

Starter Code:
class Pet:
    def __init__(self, name: str, species: str, hunger: int, energy: int):
        self.name = name
        self.species = species
        self.hunger = hunger
        self.energy = energy

whiskers = Pet("Whiskers", "cat", 6, 8)

# TODO: Print Whiskers' initial attributes

# TODO: Modify Whiskers' attributes:
#  - Decrease hunger by 3
#  - Increase energy by 2

# TODO: Print Whiskers' modified attributes


Solution:
class Pet:
    def __init__(self, name: str, species: str, hunger: int, energy: int):
        self.name = name
        self.species = species
        self.hunger = hunger
        self.energy = energy

whiskers = Pet("Whiskers", "cat", 6, 8)

# Print Whiskers' initial attributes
print(f"Initial Attributes: {whiskers.name} ({whiskers.species}) - Hunger: {whiskers.hunger}, Energy: {whiskers.energy}")

# Modify Whiskers' attributes
whiskers.hunger -= 3
whiskers.energy += 2

# Print Whiskers' modified attributes
print(f"Modified Attributes: {whiskers.name} ({whiskers.species}) - Hunger: {whiskers.hunger}, Energy: {whiskers.energy}")


3 Object Methods
Methods are functions that belong to a class or object. They define the behavior of the class or object.

Defining methods in a class
Let's update our SuperHero class to include two methods, use_power() and take_damage(amount):

class SuperHero:
    def __init__(self, name, power, health, speed):
        self.name = name
        self.power = power
        self.health = health
        self.speed = speed

    def use_power(self):
        print(f"{self.name} uses {self.power}!")

    def take_damage(self, amount):
        self.health -= amount
        print(f"{self.name} takes {amount} damage. Health is now {self.health}.")
We can create an object of the SuperHero class and call the methods on it:

iron_man = SuperHero("Iron Man", "super strength", 100, 90)

iron_man.use_power()     # Output: Iron Man uses super strength!
iron_man.take_damage(20) # Output: Iron Man takes 20 damage. Health is now 80.
Let's break down what's happening in this code:

The use_power() method:
Takes no parameters (except self, which we'll explain in a future lesson).
Prints a message saying the superhero is using their power.
The take_damage(amount) method:
Takes a parameter amount and subtracts it from the object's health.
Prints a message about the damage taken and the object's new health.
Methods are called on an object using dot notation, like iron_man.use_power(). If a method takes parameters, they are passed in the same way as function arguments e.g. iron_man.take_damage(20).

Challenge
Please see the starter code of the Pet class and complete the following in the feed method:

Decrease the pet's hunger by 1
Print the string 'Fluffy has been fed.'.
Print the current hunger level of my_pet, in this format: 'Fluffy's hunger level: X'
And then call the feed method three times on my_pet.

After completing the task your code should give the following expected output.

Expected Output
Fluffy has been fed.
Fluffy's hunger level: 4
Fluffy has been fed.
Fluffy's hunger level: 3
Fluffy has been fed.
Fluffy's hunger level: 2

Method vs Function
Methods are just functions that are defined inside a class. A function defined outside of a class is not a method.

Starter Code:
class Pet:
    def __init__(self, name: str):
        self.name = name
        self.hunger = 5

    def feed(self):
        # TODO: Implement this method
        # It should decrease the pet's hunger by 1
        # and print a message about feeding the pet
        pass

# Create a pet
my_pet = Pet("Fluffy")

# TODO: Feed the pet three times


Solution:
class Pet:
    def __init__(self, name: str):
        self.name = name
        self.hunger = 5
    
    def feed(self):
        self.hunger -= 1
        print(f"{self.name} has been fed.")
        print(f"{self.name}'s hunger level: {self.hunger}")

# Create a pet
my_pet = Pet("Fluffy")

# Feed the pet three times
my_pet.feed()
my_pet.feed()
my_pet.feed()


4 Self Parameter
When we create a superhero or call a method, how does Python know which superhero we're talking about? This is where self comes in!

self is how Python refers to the specific object being created or acted upon. It allows each superhero to have their own set of attributes and use their own powers.

In some other languages, this is used instead of self.
Let's look at our SuperHero class again:

class SuperHero:
    def __init__(self, name, power, health, speed):
        self.name = name
        self.power = power
        self.health = health
        self.speed = speed

    def use_power(self):
        print(f"{self.name} uses {self.power}!")
Notice how self is the first parameter in all our methods, including __init__. This is a Python convention and is required for methods to work.

How self works in method calls
To better understand how self works, it can be helpful to think of it this way:

spider_man = SuperHero("Spider-Man", "web-slinging", 100, 90)

spider_man.use_power() # SuperHero.use_power(spider_man)
self inside use_power() refers to spider_man
Challenge:
You are given a Superhero class with a power_boost method that is not working correctly. When you run this code, you'll encounter the following error:

TypeError: power_boost() takes 1 positional argument but 2 were given
Your task is to identify the issue and fix it and get the expected output.

Expected Output
Iron Man's strength increased to 100!

Hints
Think about the role of self in class methods.
Consider how instance attributes are accessed within a method.

Starter Code:
class SuperHero:
    def __init__(self, name: str, power: str, strength: int):
        self.name = name
        self.power = power
        self.strength = strength
    
    def power_boost(self) -> None:
        self.strength += strength_increase
        print(f"{self.name}'s strength increased to {self.strength}!")



# Don't modify the following code
ironman = SuperHero("Iron Man", "Repulsor Beams", 85)

ironman.power_boost(15)

Solution:
class SuperHero:
    def __init__(self, name: str, power: str, strength: int):
        self.name = name
        self.power = power
        self.strength = strength
    
    def power_boost(self, strength_increase: int) -> None:
        self.strength += strength_increase
        print(f"{self.name}'s strength increased to {self.strength}!")



# Don't modify the following code
ironman = SuperHero("Iron Man", "Repulsor Beams", 85)

ironman.power_boost(15)



5 Init Method

6 Docstrings

7 Implement Superhero Class

8 Add Superhero Abilities


2 - Encapsulation

9 Public Attribute and Method

10 Protected Attribute and Method

11 Private Attribute and Method

12 Getter and Setter Methods

13 Property and Setter Decorator

14 Hide Hero Details

15 Hide Details Using Decorators



3 - Class Attributes

16 Class Attributes

17 Class vs Instance Attributes

18 Class Methods

19 Static Methods

20 Implement Power Calculation System



4 - Inheritance

21 Inheritance Basics

22 Method Overriding

23 Super Function

24 Multiple Inheritance

25 Diamond Problem and Method Resolution Order

26 Implement Superhero Game



5 - Polymorphism

27 Polymorphism with Inheritance

28 Method Overloading

29 Duck Typing

30 Implement Polymorphic Battle System

31 Implement Area calculator


6 - Abstraction

32 Abstraction

33 Abstract Method and Class

34 Interface

35 Implement Abstract Superpower

36 Implement Hero Roles