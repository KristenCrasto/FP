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
<!-- ```
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo();
```

@[1-3](Which one would you use to get the Active Account?)

+++

##### Variable Names

```
moneyAmount vs money
customerInfo vs customer
theMessage vs message
accountData vs account
```

@[1-4](Don't make variables compete for attention)

---

#### Avoid Mental Mapping

```python
for i in range(34):
  s += (t[i]*4)/5;
```

@[2](Clearly everyone knows why we multiply times 4 and divide by 5)

+++

#### Searchable Names

```python
real_days_per_ideal_day = 4
work_days_per_week = 5
number_of_tasks = len(task_estimates)
sum = 0
for i in range(number_of_tasks):
  real_days = task_estimates[i] * real_days_per_ideal_day
  real_weeks = (real_days / work_days_per_week)
  sum += real_weeks
```
@[1-8](How about now?)
@[4](Although this name is great, it shadows a built in function)
@[3, 5](Why acces via array? Why not For In?)

---

#### Good naming can replace comments

```python
# Check to see if the employee is elegibile for bonus
if (employee.flag and employee.rating >= 4 and employee.years > 5)

if (employee.isEligibleForBonus())
```

Note:
- is / has Function Names
---

### Functions

- Functons should be small, the smaller the better |
- A function should only do one thing |
- One level of abstraction |
- Less arguments are better |
- Impure Sandwhich -> No side effects* |

---

#### Building Blocks

![Blocks](assets/image/blocks.jpeg)

Note:
- Level Of Astraction
- Composing
- Small

---

#### Code Examples

```java
public void Checkout()
{
  Price CurrentPrice = new Price();
  foreach(var product in CurrentShoppingCart)
    CurrentPrice.Add(product.Price);
  foreach(var coupon in CurrentDiscounts)
    CurrentPrice.Discount(coupon.Price);

  var billingInfo = BillingRepository.get(BillingId);
  if (billingInfo.CheckIfStillValid() == False)
  {
    DisplayError("Invalid Billing Information")
    return;
  }

  var paymentResult = PaymentGateway.Charge(billingInfo, CurrentPrice);
  if (paymentResult.Success == false)
  {
    DisplayError("Payment Processing Error");
    return;
  }
  DisplayMessage("Thank you for your order");
}
```
@[3-7](We first Calculate our Price by summing product prices and subtracting discount prices)
@[9-14](We then confirm if the billing info is valid)
@[16-23](Finally we charge the billingInfo card the currentPrice)
@[1-24](Think we can use our magic refactoring wand?)

+++

```java
public void Checkout()
{
  UpdateCurrentTotalPrice()
  ChargeCustomer()
  DisplayResult()
}

private void UpdateCurrentTotalPrice()
{
  Price CurrentPrice = new Price()
  SumShoppingCartProductsToCurrentPrice(CurrentPrice);
  ApplyShoppingCartDiscountsToCurrentPrice(CurrentPrice);
}

private void SumShoppingCartProductsToCurrentPrice()
{
  foreach(var product in CurrentShoppingCart)
    CurrentPrice.Add(product.Price);
}

// etc ...
```

@[1-6](High Level Abstraction)
@[8-13](Mid Level Abstraction)
@[15-19](Detail Level)

---

#### Impure Sandwich

![Sandwich](assets/image/cookie_sandwich.png)

Fun Fact: I love ice cream sandwiches

+++

```python
# Simplified version of making a reservation at a restaurant
def makeReservation(quantity, date, restaurantId):
	restaurant = Restaurant.getRestaurant(restaurantId) # ORM
	reservationsOnDate = filter(lambda reservation: reservation.date == date, restaurant.reservations)
	available_seats = restaurant.capacity - len(reservationsOnDate)
	if available_seats >= quantity:
		return Restaurant.reserve(data, quanitity) # Returns a reservation String from db call
	else:
		return None # Client Handles None
```

@[2-9](Code is easy to read, seems straighfoward what we are doing)
@[3](Here is our culprit, making we are mixing a database call with our business logic)
@[4-6](This is our business logic)
@[7](More of this impure **Hogwash**!)

+++

```python
# Impure Function Call
def getRestaurant(restaurantId):
	restaurant = Restaurant.getRestaurant(restaurant)


# Business Logic
@_.curry
def canMakeReservation(quantity, date, restaurant):
	reservationsOnDate = filter(lambda reservation: reservation.date == date, restaurant.reservations)
	available_seats = restaurant.capacity - len(reservationsOnDate)
	if available_seats >= quantity:
		return Some(Reservation(quantity, date)) # Creates a reservation object
	else:
		return None

#Impure Function Call
def reserve(reservation):
	return Restaurant.reserve(reservation)

# Yummy Impure Sandwhich
def makeReservation(quantity, date, restaurantId):
	return _.compose(
			getRestaurant(restaurantId),
			canMakeReservation(quantity, date),
			lambda reservation: reserve(reservation) if reservation else None # Does your language have Options?
		)
```
@[1-3](First Impure DB Call)
@[6-14](Business Logic Pure Function)
@[16-18](Second Impure DB Call)
@[20-26](We build our impure sandwhich via compose)
@[25](**Note** This Janky Ternary Operation, Does your language support Option?)

---

![Comic Style Guide](assets/image/styleGuide.png)

---

### Code Readability

- Nested Code sucks |
- Looping |
- Formatting Code |
- Broken Windows |

---

#### Nested Code

![Graph](assets/image/nestedIf.jpg)

---

#### Looping
##### Shameless Functional Programming Plug

```javascript
// Artists with popularity <= 3 percentage of given playlist
func getHipsterArtists(playlist) {
	const maxPopularity = 3
	let artists = []
	// Get All the artists from a playlist and filter only unpopular artists
	for(let songIndex = 0; songIndex < playlist.length; songIndex++) {
		const artistsCount = playlist[songIndex].artists.length
	    for (let artistIndex = 0; artistIndex  < artistsCount; artistIndex++) {
	        if playlist[songIndex][artistIndex].popularity <= 3 {
	        	artists.append(playlist[songIndex][artistIndex].name)
	        }
	}
	return artists
}

//Functional with ES6
const getHipsterArtists = (playlist) => {
	const maxPopularity = 3
	return playlist.
		flatMap(song => song.artists).
		filter(artists => artists.popularity <= maxPopularity).
		map(artists => artists.name)
}
```
@[2-13](Imperative Programming, you have to read deep in the code to see exactly whats happening)
@[15-22](Functional Programming, concise and clean, generally no need for comments)
@[2-13](This is a small example, but have you seen double/triple for loops with maybe 3 or 4 if statements inside?)

---

#### Formatting Code

- Horizontal - Line Length |
- Vertical - File Size |
- Indentation |
- Consistency |
- Style Guide & Linter |

---

#### Broken Windows

+++

![Windows](https://image.slidesharecdn.com/designingviolenceoutofschools-110919110142-phpapp01/95/cpted-designing-violence-out-of-schools-27-728.jpg?cb=1335528522)

---

### Refactoring

- Types of Requirements |
- Refactoring |
- Technical Debt |
- Code Smells |

---

#### Types of Requirements

- Functional |
- Operational |
- Developmental |

Note:
- Functional: Use cases, features
- Operational: Performance, SLA
- Developmental: Developers QOL
- Raise hand if you have had a refactoring sprint or investment to just improve code readability


---

#### Refactoring

![Stickmen](http://deus.co.uk/images/refactoring.png)

---

#### Why Refactor

+++

>By continuously improving the design of code, we make it easier and easier to work with.

---

#### What Is Refactoring

+++

> Code Refactoring is the process of clarifying and simplifying the design of existing code, without changing its behavior.

---


#### When

- Brittle Code |
- Turn around times on Functional Requirements increased |
- Debugging takes longer |
- Onboarding New Joiners takes longer |
- Code Smells |

---

#### Technical Debt

+++

> The implied cost of additional rework caused by choosing an easy solution now instead of using a better approach that would take longer

+++

![Technical_Debt](https://www.jeremymorgan.com/images/code-smell-2.jpg)

---

#### Code Smells

+++

> A code smell is a surface indication that usually corresponds to a deeper problem in the system

---

#### Code Smell Categories

- Bloaters |
- Object orientation Abusers |
- Change Preventers |
- Dispensables |
- Couplers |

Note:
- Gargantuan Porpotion
- Incorrect Application of OO
- Makes change so expensive you dont want to do it
- Pointless/uneeded
- Excessive Coupling

---

# Kata

Note:
- Naming: clear and concise
- Functions: level of abstraction, one thing, small
- Code smells: are there any?
- Refactor: where would you refactor

---

### How to write unmaintanable code

- Use horrible naming for variables and functions |
- Don't break up your functions into abstract levels |
- Make your code look like a maze |
- Compete to see who has the most technical debt |

---

![Image-Relative](http://giant.gfycat.com/BothLongAstrangiacoral.gif)

---

## Thank you!
### Be sure to check out the rest of our classes! -->
