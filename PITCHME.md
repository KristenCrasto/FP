## Functional Programming

#### **NIC** Practical Programmer Series

---

### Practical Programmer Series

- Clean Code
- Code Complete
- Testable Code
- Code Reviewing
- Design Patterns
- **Functional Programming**

Note:
Inspiration: Great information out there for our profession that we never got taught.
Goal: Walk away from here with knowledge thats immediately applicable to your coding.

---

### Goals

- Understand the key concepts of FP |
- Understanding the difference between Programming Paradigms |
- Ability to transform non-functional code to functional |
- Have a FP "toolbox" to apply in a practical manner |
- Feel comfortable using FP in day-to-day scenarios |

---

### What is Functional Programming?

- The process of building software by composing **pure** functions. This means **avoiding** shared **state**, **mutable** data, and **side-effects**

```python
// imperative version
pacman = new pacman(0, 0)
while true
  if key = UP then pacman.y++
  elif key = DOWN then pacman.y--
  elif key = LEFT then pacman.x--
  elif key = RIGHT then pacman.x++
```

+++

```haskell
// functional version
let rec loop pacman =
  render(pacman)
  let x, y = switch(key)
    case UP: paxman.x, pacman.y + 1
    case DOWN: pacman.x, pacman.y - 1
    case LEFT: pacman.x - 1, pacman.y
    case RIGHT: pacman.x + 1, pacman.y
    loop(new pacman(x, y))
```

---

### Pure Functions

- A pure function **always returns the same result given the same parameters** and does not depend on the state of the system
- Only depends on the arguments passed in and doesn't modify variables out of its scope

```javascript
amount = 10;
function impureAdder(x){
  return amount + x;
}

function pureAdder(value, x){
  return value + x;
}
```

+++

```javascript
function impureCalculateTax(obj, tax){
  obj.cost *= tax;
  return obj.cost;
}

function pureCalculateTax(obj, tax){
  return obj.cost * tax;
}
```
<!-- @[1-8](relies on the current state)
@[10-17](modifies the scope) -->

---

### Immutable State

- An object's state **does not change** after it has been defined
- The basic strategy here is to create functions that take in a state and return a new state

```javascript
var xs = [1, 2, 3, 4, 5];

// pure
xs.slice(0, 3);
//=> [1, 2, 3]

xs.slice(0, 3);
//=> [1, 2, 3]

xs.slice(0, 3);
//=> [1, 2, 3]
```

+++

```javascript
var xs = [1, 2, 3, 4, 5];
// impure
xs.splice(0, 3);
//=> [1, 2, 3]

xs.splice(0, 3);
//=> [4, 5]

xs.splice(0, 3);
//=> []
```

Note:
- imagine using the keyword **final** for all variables
- find examples in other languages
---

### Side Effects

- A side effect is a change of system state or observable interaction with the outside world that occurs during the calculation of a result.

< insert example >

---

### First Class Functions

- Functions are treated the **same as any other data type** - they may be stored in arrays, passed around as function parameters, assigned to variables, etc

```javascript
var hi = function(name) {
  return 'Hi ' + name;
};

var greeting = function(name) {
  return hi(name);
};

hi;
// function(name) {
//  return 'Hi ' + name
// }

hi('jonas');
// "Hi jonas"
```
**REWRITE EXAMPLE IN OTHER LANGUAGE**

---
![Blocks](assets/image/stream.jpg)
---

#### Map

```java
List<String> alpha = Arrays.asList("a", "b", "c", "d");
List<String> upperCase = alpha.stream()
                        .map(String::toUpperCase)
                        .collect(Collectors.toList());
System.out.println(upperCase); //[A, B, C, D]
```

-iterate over every element in alpha and make it upper case

---

#### Filter

```Python
fib = [0,1,1,2,3,5,8,13,21,34,55]
result = filter(lambda x: x % 2, fib)
#[1, 1, 3, 5, 13, 21, 55]
```

-iterates through every element in the list and only returns those that satisfy the condition

---

#### Reduce

```javascript
var euros = [29.76, 41.85, 46.5];
var sum = euros.reduce( function(total, amount){
  return total + amount
});
sum // 118.11
```
-iterate over every element in alpha and apply the reducer

---

### List Comprehension

```Python
new_range  = [i * i for i in range(5) if i % 2 == 0]

# You can either use loops:
squares = []

for x in range(10):
    squares.append(x**2)

print squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# Or you can use list comprehensions to get the same result:
squares = [x**2 for x in range(10)]

print squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```
-Simply *result*  = [transform    iteration         filter     ]

---

### FP VS OOP

- Designed to solve different problems
  - Object-oriented languages are good when you have a fixed set of *operations* on *things*
  - Functional languages are good when you have a fixed set of *things*, and as your code evolves, you primarily add new operations on existing things.

+++

- Each have their own complications
  - Adding a new operation to an object-oriented program may require editing many class definitions to add a new method
  - Adding a new kind of thing to a functional program may require editing many functions to add a new case

But remember: OOP can co-exist with FP

---

### Benefits of Functional Programming

- Functional code keeps all state held on the stack which allows for easier debugging using the stack trace
- Easier to avoid repetitive code

---

### Kata

---

### Advanced Topics
- Technically mathematical
- writing what a program is supposed to do in a form of equations defining new values (note: not variables) as functions of previously defined values

---

### Higher Order Functions

```python
"""
Decorator Functions/ Higher Order functions
Take in a function as input and return another function as output
"""
#Implement Memoize
def memoize(fn, memory):
  def helper(*args):
    if args not in memory:
      print "Need to cache"
      memory[args] = fn(*args)
    return memory[args]
  return helper
```

---

### Generic Flow Selection

```python
def math_strategy(op):
  fns = {
    'add': lambda data: reduce(lambda x,y: x + y, data),
    'subtract': lambda data: reduce(lambda x,y: x - y, data),
    'multiply': lambda data: reduce(lambda x,y: x * y, data)
  }
  return fns.get(op)
```

---

### Currying

```python
def addTwo(x, y):
  return x + y

def addCurry(x):
  def add_to(y):
    return x + y
  return add_to

print addTwo(1, 1) #2
print addCurry(1)(1) #2
```

---

### Pipeline

```python
def pipeline(data, fns):
  return reduce(lambda data, fns: map(fns, data), fns, data)
```
-difference in java where your pipeline is the stream

---

### Resources

Java
- https://www.manning.com/books/java-8-in-action

Python
- https://maryrosecook.com/blog/post/a-practical-introduction-to-functional-programming

Javascript
- https://drboolean.gitbooks.io/mostly-adequate-guide-old/content/ch4.html#more-than-a-pun--special-sauce
- http://reactivex.io/learnrx/

---
