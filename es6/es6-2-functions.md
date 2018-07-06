# JavaScript ES6 Functions

<a href="https://www.udacity.com/">
  <img src="https://s3-us-west-1.amazonaws.com/udacity-content/rebrand/svg/logo.min.svg" width="300" alt="Udacity logo">
</a>

[ES6 - JavaScript Improved course](https://www.udacity.com/course/es6-javascript-improved--ud356) lesson 2/4

Udacity Google Mobile Web Specialist Nanodegree program part 3 lesson 05

Udacity Grow with Google Scholarship challenge course lesson 07

Brendon Smith

[br3ndonland](https://github.com/br3ndonland)

## Table of Contents <!-- omit in toc -->

- [JavaScript Arrow Functions](#javascript-arrow-functions)
  - [2.01. Updates to Functions](#201-updates-to-functions)
  - [2.02. Arrow Functions](#202-arrow-functions)
  - [2.03. Using Arrow Functions](#203-using-arrow-functions)
  - [2.04. Quiz: Convert Function into an Arrow Function (2-1)](#204-quiz-convert-function-into-an-arrow-function-2-1)
  - [2.05. Arrow Functions Recap](#205-arrow-functions-recap)
- [JavaScript "this"](#javascript-this)
  - [2.06. Arrow Functions and the "this" Keyword](#206-arrow-functions-and-the-this-keyword)
  - [2.07. "this" and Regular Functions](#207-this-and-regular-functions)
  - [2.08. "this" and Arrow Functions](#208-this-and-arrow-functions)
  - [2.09. Default Function Parameters](#209-default-function-parameters)
  - [2.10. Defaults and Destructuring](#210-defaults-and-destructuring)
  - [2.11. Quiz: Using Default Function Parameters (2-2)](#211-quiz-using-default-function-parameters-2-2)
- [JavaScript Classes](#javascript-classes)
  - [2.12. Class Preview](#212-class-preview)
  - [2.13. JavaScript's Illusion of Classes](#213-javascripts-illusion-of-classes)
  - [2.14. JavaScript Classes](#214-javascript-classes)
  - [2.15. Convert a Function to a Class](#215-convert-a-function-to-a-class)
  - [2.16. Working with JavaScript Classes](#216-working-with-javascript-classes)
  - [2.17. Super and Extends](#217-super-and-extends)
  - [2.18. Extending Classes from ES5 to ES6](#218-extending-classes-from-es5-to-es6)
  - [2.19. Working with JavaScript Subclasses](#219-working-with-javascript-subclasses)
  - [2.20. Quiz: Building Classes and Subclasses (2-3)](#220-quiz-building-classes-and-subclasses-2-3)
  - [2.21. Lesson 2 Summary](#221-lesson-2-summary)
- [Feedback on JavaScript ES6 lesson 2/4](#feedback-on-javascript-es6-lesson-24)

## JavaScript Arrow Functions

### 2.01. Updates to Functions

> Functions are one of the primary data structures in JavaScript; they've been around *forever*.

### 2.02. Arrow Functions

#### Arrow functions

> ES6 introduces a new kind of function called the **arrow function**.
>
> Arrow functions are very similar to regular functions in behavior, but are quite different syntactically. The following code takes a list of names and converts each one to uppercase using a regular function:
>
> ```javascript
> const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) {
>   return name.toUpperCase();
> });
> ```
>
> The code below does the same thing except instead of passing a regular function to the `map()` method, it passes an arrow function. Notice the arrow in the arrow function (`=>`) in the code below:
>
> ```javascript
> const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
>   name => name.toUpperCase()
> );
> ```
>
> The only change to the code above is the code inside the `map()` method. It takes a regular function and changes it to use an arrow function.
>
> NOTE: Not sure how `map()` works? It's a method on the Array prototype. You pass a function to it, and it calls that function once on every element in the array. It then gathers the returned values from each function call and makes a new array with those results. For more info, check out [MDN's documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map).

#### Convert a function to an arrow function

```javascript
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) {
  return name.toUpperCase();
});
```

With the function above, there are only a few steps for converting the existing "normal" function into an arrow function:

- remove the `function` keyword
- remove the parentheses
- remove the opening and closing curly braces
- remove the `return` keyword
- remove the semicolon
- add an arrow (`=>`) between the parameter list and the function body

Converting a normal function into an arrow function:

```javascript
// es5
const upperizedNames = ['Farrin', 'Kagure', 'Asser']
  .map(function(name) {
    return name.toUpperCase();
  });

// es6
const upperizedNames = ['Farrin', 'Kagure', 'Asser']
  .map( name => name.toUpperCase() );
```

#### 2.02 Mini-Quiz Question

Take a look at the following code:

```javascript
const names = ['Afghanistan', 'Aruba', 'Bahamas', 'Chile', 'Fiji', 'Gabon',
                'Luxembourg', 'Nepal', 'Singapore', 'Uganda', 'Zimbabwe'];

const longNames = names.filter(function(name) {
  return name.length > 6;
});
```

Which of the following choices does the same thing, but replaces .filter()'s function with an arrow function?

- `const longNames = names.filter( function(name) => return name.length > 6; );`
- `const longNames = names.filter( return name.length > 6 );`
- `const longNames = names.filter( name => {names.length > 6} );`
- `const longNames = names.filter( name => name.length > 6 );`

<details>
  <summary><em>Solution</em></summary>

```javascript
const longNames = names.filter( name => name.length > 6 );
```

Got it on my first try by evaluating the checklist [above](#convert-a-function-to-an-arrow-function).

> This arrow function returns country names that are six characters or longer.

</details>

### 2.03. Using Arrow Functions

#### Intro

> **Regular functions can be either function declarations or function expressions, but arrow functions are *always* expressions.** In fact, their full name is "arrow function expressions", so they can only be used where an expression is valid. This includes being:
>
> - stored in a variable,
> - passed as an argument to a function,
> - and stored in an object's property.
>
> One confusing syntax is when an arrow function is stored in a variable.
>
> ```javascript
> const greet = name => `Hello ${name}!`;
> ```
>
> In the code above, the arrow function is stored in the greet variable and you'd call it like this:
>
> ```javascript
> greet('Asser');
> ```
>
> Returns: `Hello Asser!`

#### Parentheses and arrow function parameters

> You might have noticed the arrow function from the `greet()` function looks like this:
>
> ```javascript
> name => `Hello ${name}!`
> ```
>
> If you recall, the parameter list appears before the arrow function's arrow (i.e. `=>`). If there's only **one** parameter in the list, then you can write it just like the example above. But, if there are **two or more** items in the parameter list, or if there are **zero** items in the list, then you need to wrap the list in parentheses:
>
> ```javascript
> // empty parameter list requires parentheses
> const sayHi = () => console.log('Hello Udacity Student!');
> sayHi();
> ```
> Prints:
> ```text
> Hello Udacity Student!
> ```
>
> ```javascript
> // multiple parameters requires parentheses
> const orderIceCream = (flavor, cone) => console.log(`Here's your ${flavor} ice cream in a ${cone} cone.`);
> orderIceCream('chocolate', 'waffle');
> ```
> Prints:
> ```text
> Here's your chocolate ice cream in a waffle cone.
> ```

#### 2.03 Mini-Quiz Question 1 of 2

Which of the following choices have correctly formatted arrow functions?

```javascript
setTimeout(() => {
  console.log('starting the test');
  test.start();
}, 2000);
```

```javascript
setTimeout( _ => {
  console.log('starting the test');
  test.start();
}, 2000);
```

```javascript
const vowels = 'aeiou'.split('');
const bigVowels = vowels.map( (letter) => letter.toUpperCase() );
```

```javascript
const vowels = 'aeiou'.split('');
const bigVowels = vowels.map( letter => letter.toUpperCase() );
```

<details>
  <summary><em>Solution</em></summary>

> All four options are valid uses of arrow functions.

*[Additional notes from James Priest](https://github.com/james-priest/100-days-of-code-log-r2/blob/master/ES6-Functions.md#solution-1):*

> If there's no parameter to the function, you just use a pair of empty parentheses like option 1.
>
> Alternatively, some developers choose to use an underscore as their single parameter. The underscore never gets used, so it's `undefined` inside the function, but it's a common technique.
>
> The only difference between options 3 and 4 is the use of the parentheses around `letter`. Typically, if there's only one parameter, then no parentheses are used, but it's not wrong.

</details>

#### Concise and block body syntax

> All of the arrow functions we've been looking at have only had a single expression as the function body:
>
> ```javascript
> const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
>   name => name.toUpperCase()
> );
> ```
>
> This format of the function body is called the "**concise body syntax**". The concise syntax:
>
> - has no curly braces surrounding the function body
> - and automatically returns the expression.
>
> If you need more than just a single line of code in your arrow function's body, then you can use the "**block body syntax**".
>
> ```javascript
> const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map( name => {
>   name = name.toUpperCase();
>   return `${name} has ${name.length} characters in their name`;
> });
> ```
>
> Important things to keep in mind with the block syntax:
>
> - it uses curly braces to wrap the function body
> - and a return statement needs to be used to actually return something from the function.

#### 2.03 Mini-Quiz Question 2 of 2

Using your knowledge of how arrow functions work with automatic returns and curly braces, which of the following choices have correctly formatted arrow functions?

```javascript
const colors = ['red', 'blue', 'yellow', 'orange', 'black'];
const crazyColors = color.map( color => {
  const jumble = color.split('').reverse();
  return jumble.join('') + '!';
});
```

```javascript
const colors = ['red', 'blue', 'yellow', 'orange', 'black'];
const crazyColors = color.map( color => {
  color.split('').reverse().join('') + '!';
});
```

```javascript
const colors = ['red', 'blue', 'yellow', 'orange', 'black'];
const crazyColors = color.map( color => return color.split('').reverse().join('') + '!' );
```

```javascript
const colors = ['red', 'blue', 'yellow', 'orange', 'black'];
const crazyColors = color.map( color => color.split('').reverse().join('') + '!' );
```

<details>
  <summary><em>Solution</em></summary>

Again, I evaluated the checklist [above](#convert-a-function-to-an-arrow-function), along with the [new info](#concise-and-block-body-syntax).

> Options 1 and 4 both use correct syntax for arrow functions.

*[Additional notes from James Priest](https://github.com/james-priest/100-days-of-code-log-r2/blob/master/ES6-Functions.md#solution-2):*

> 1. Option 1 is correct. Because the arrow function uses curly braces, there has to be a `return` in there somewhere for something to actually be returned.
> 2. Option 2 is not correct because it has curly braces and no `return`. This function runs, but nothing gets returned to crazyColors.
> 3. Option 3 doesn't have curly braces. This means it needs to be in the concise syntax and automatically return the expression so it should not have a `return` keyword, so this one isn't correct.
> 4. Option 4 is correct. This is the most common way you'll see arrow functions written—as one-liners that automatically return.

</details>

#### Summary

> So arrow functions are awesome!
>
> - The syntax is a lot shorter,
> - it's easier to write and read short, single-line functions,
> - and they automatically return when using the concise body syntax!
>
> **WARNING:** Everything's not all ponies and rainbows though, and there are definitely times when you might not want to use an arrow function. So before you wipe from your memory how to write a traditional function, check out these implications:
>
> - there's a gotcha with the `this` keyword in arrow functions
>   - go to the next lesson to find out the details!
>
> - arrow functions are only _expressions_
>   - there's no such thing as an arrow function declaration

### 2.04. Quiz: Convert Function into an Arrow Function (2-1)

Convert the function passed to the `map()` method into an arrow function.

```javascript
/*
 - Programming Quiz: Convert Function into an Arrow Function (2-1)
 */

// convert to an arrow function
const squares = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(function(square) {
  return square - square;
});

console.log(...squares);
```

<details>
  <summary><em>Solution</em></summary>

I walked through the steps and example code [above](#convert-a-function-to-an-arrow-function) to get the solution:

- remove the `function` keyword
- remove the parentheses
- remove the opening and closing curly braces
- remove the `return` keyword
- remove the semicolon
- add an arrow (`=>`) between the parameter list and the function body

```javascript
// es5
const upperizedNames = ['Farrin', 'Kagure', 'Asser']
  .map(function(name) {
    return name.toUpperCase();
  });

// es6
const upperizedNames = ['Farrin', 'Kagure', 'Asser']
  .map( name => name.toUpperCase() );
```

Got it on my first try!

```javascript
// converted from normal to arrow function
const squares = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  .map( square => square - square );

console.log(...squares);
```

```text
1 4 9 16 25 36 49 64 81 100
```

> What Went Well
>
> - Your code should have a variable squares
> - The variable squares should be an array
> - Your code should replace the function expression with an arrow function
> - Your arrow function should have one parameter called square
> - Your arrow function should square each element in the squares array
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 2.05. Arrow Functions Recap

Arrow functions allow us to remove

- `function`
- `return`
- `{ }`

[(Back to top)](#top)

## JavaScript "this"

### 2.06. Arrow Functions and the "this" Keyword

- **Finally, the mystical "this"!**
- The value of "this" depends on how the function is called.
- In arrow functions, the value of "this" depends on where it's located in the code.

### 2.07. "this" and Regular Functions

#### Intro to `this`

> To get a handle on how `this` works differently with arrow functions, let's do a quick recap of how `this` works in a standard function. If you have a solid grasp of how `this` works already, feel free to jump over this section.
>
> The value of the `this` keyword is based completely on how its function (or method) is called. `this` could be any of the following:

##### 1. A new object

> If the function is called with `new`:
>
> ```javascript
> const mySundae = new Sundae('Chocolate', ['Sprinkles', 'Hot Fudge']);
> ```
>
> In the code above, the value of `this` inside the `Sundae` constructor function is a new object because it was called with `new`.

##### 2. A specified object

> If the function is invoked with `call`/`apply`:
>
> ```javascript
> const result = obj1.printName.call(obj2);
> ```
>
> In the code above, the value of `this` inside `printName()` will refer to `obj2` since the first parameter of `call()` is to explicitly set what `this` refers to.

##### 3. A context object

> If the function is a method of an object:
>
> ```javascript
> data.teleport();
> ```
>
> In the code above, the value of `this` inside `teleport()` will refer to `data`.

##### 4. The global object or undefined

> If the function is called with no context:
>
> ```javascript
> teleport();
> ```
>
> In the code above, the value of `this` inside `teleport()` is either the global object or, if in strict mode, it's `undefined`.

#### Tip

> TIP: `this` in JavaScript is a complicated topic. We just did a quick overview, but for an in-depth look at how `this` is determined, check out [this All Makes Sense Now!](https://github.com/getify/You-Dont-Know-JS/blob/master/this%20%26%20object%20prototypes/ch2.md) from Kyle Simpson's book series [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS/blob/master/README.md).

#### 2.07 Mini-Quiz Question 1 of 2

What is the value of `this` inside the `Train` constructor function below?

```javascript
const redTrain = new Train('red');
```

- the `window` object
- a new object
- `undefined`

<details>
  <summary><em>Solution</em></summary>

a new object

> Since the `new` keyword was used, the correct answer is a new object.

</details>

#### 2.07 Mini-Quiz Question 2 of 2

What is the value of `this` inside the `increaseSpeed()` function below?

```javascript
const redTrain = new Train('red');
redTrain.increaseSpeed(25);
```

- the `window` object
- a new object
- the `redTrain` object
- `undefined`

<details>
  <summary><em>Solution</em></summary>

the `redTrain` object

> Since the `increaseSpeed()` function is called from a context object (`redTrain`) that context object will be the value of `this` in the function.

</details>

### 2.08. "this" and Arrow Functions

I didn't follow 2.08 very well. I worked on it early in the morning and I wasn't really awake yet.

> With regular functions, the value of `this` is set based on _how the function is called_. With arrow functions, the value of `this` is based on the _function's surrounding context_. In other words, the value of `this` _inside_ an arrow function is the same as the value of `this` _outside_ the function.
>
> Let's check out an example with `this` in regular functions and then look at how arrow functions will work.
>
> ```javascript
> // constructor
> function IceCream() {
>   this.scoops = 0;
> }
>
> // adds scoop to ice cream
> IceCream.prototype.addScoop = function() {
>   setTimeout(function() {
>     this.scoops++;
>     console.log('scoop added!');
>   }, 500);
> };
>
> const dessert = new IceCream();
> dessert.addScoop();
> ```
>
> Prints:
>
> ```text
> scoop added!
> ```
> After running the code above, you'd _think_ that `dessert.scoops` would be 1 after half a millisecond. But, unfortunately, it's not:
>
> ```javascript
> console.log(dessert.scoops);
> ```
>
> Prints:
>
> ```text
> 0
> ```
>
> Can you tell why?
>
> The function passed to `setTimeout()` is called without `new`, without `call()`, without `apply()`, and without a context object. That means the value of `this` inside the function is the global object and **NOT** the `dessert` object. So what actually happened was that a new `scoops` variable was created (with a default value of `undefined`) and was then incremented (`undefined + 1` results in `NaN`):
>
> ```javascript
> console.log(scoops);
> ```
>
> Prints:
>
> ```text
> NaN
> ```
>
> One way around this is to use closure:
>
> ```javascript
> // constructor
> function IceCream() {
>   this.scoops = 0;
> }
>
> // adds scoop to ice cream
> IceCream.prototype.addScoop = function() {
>   const cone = this; // sets `this` to the `cone` variable
>   setTimeout(function() {
>     cone.scoops++; // references the `cone` variable
>     console.log('scoop added!');
>   }, 0.5);
> };
>
> const dessert = new IceCream();
> dessert.addScoop();
> ```
>
> The code above _will_ work because instead of using `this` inside the function, it sets the cone variable to this and then looks up the cone variable when the function is called. This works because it's using the value of the this outside the function. So if we check the number of scoops in our dessert right now, we'll see the correct value of `1`:
>
> ```javascript
> console.log(dessert.scoops);
> ```
>
> Prints:
>
> ```text
> 1
> ```
>
> Well that's exactly what arrow functions do, so let's replace the function passed to `setTimeout()` with an arrow function:
>
> ```javascript
> // constructor
> function IceCream() {
>   this.scoops = 0;
> }
>
> // adds scoop to ice cream
> IceCream.prototype.addScoop = function() {
>   setTimeout(() => { // an arrow function is passed to setTimeout
>     this.scoops++;
>     console.log('scoop added!');
>   }, 0.5);
> };
>
> const dessert = new IceCream();
> dessert.addScoop();
> ```
>
> Since arrow functions inherit their this value from the surrounding context, this code works!
>
> ```javascript
> console.log(dessert.scoops);
> ```
>
> > **Prints:**<br>
> > 1
>
> When `addScoop()` is called, the value of `this` _inside_ `addScoop()` refers to `dessert`. Since an arrow function is passed to `setTimeout()`, it's using its surrounding context to determine what `this` refers to inside itself. So since `this` _outside_ of the arrow function refers to `dessert`, the value of `this` _inside_ the arrow function will also refer to `dessert`.`
>
> Now what do you think would happen if we changed the `addScoop()` method to an arrow function?
>
> ```javascript
> // constructor
> function IceCream() {
>     this.scoops = 0;
> }
>
> // adds scoop to ice cream
> IceCream.prototype.addScoop = () => { // addScoop is now an arrow function
>   setTimeout(() => {
>     this.scoops++;
>     console.log('scoop added!');
>   }, 0.5);
> };
>
> const dessert = new IceCream();
> dessert.addScoop();
> ```
>
> Yeah, this doesn't work for the same reason - arrow functions inherit their `this` value from their surrounding context. Outside of the `addScoop()` method, the value of `this` is the global object. So if `addScoop()` is an arrow function, the value of `this` _inside_ `addScoop()` is the global object. Which then makes the value of `this` in the function passed to `setTimeout()` also set to the global object!

### 2.09. Default Function Parameters

#### Intro to default function parameters

> Take a look at this code:
>
> ```javascript
> function greet(name, greeting) {
>   name = (typeof name !== 'undefined') ?  name : 'Student';
>   greeting = (typeof greeting !== 'undefined') ?  greeting : 'Welcome';
>
>   return `${greeting} ${name}!`;
> }
>
> greet(); // Welcome Student!
> greet('James'); // Welcome James!
> greet('Richard', 'Howdy'); // Howdy Richard!
> ```
>
> Returns:
>
> ```text
> Welcome Student!
> Welcome James!
> Howdy Richard!
> ```
>
> What is all that horrible mess in the first two lines of the `greet()` function? All of that is there to provide default values for the function if the required arguments aren't provided. It's pretty ugly, though...
>
> Fortunately, ES6 has introduced a new way to create defaults. It's called **default function parameters**.

#### Default function parameters

> Default function parameters are quite easy to read since they're placed in the function's parameter list:
>
> ```javascript
> function greet(name = 'Student', greeting = 'Welcome') {
>   return `${greeting} ${name}!`;
> }
>
> greet(); // Welcome Student!
> greet('James'); // Welcome James!
> greet('Richard', 'Howdy'); // Howdy Richard!
> ```
>
> Returns:
>
> ```text
> Welcome Student!
> Welcome James!
> Howdy Richard!
> ```
>
> Wow, that's a lot less code, so much cleaner, and significantly easier to read!
>
> To create a default parameter, you add an equal sign and then whatever you want the parameter to default to if an argument is not provided. In the code above, both parameters have default values of strings, but they can be any JavaScript type!

#### 2.09 Mini-Quiz Question

Take a look at the following code:

```javascript
function shippingLabel(name, address) {
  name = (typeof name !== 'undefined') ? name : 'Richard';
  address = (typeof address !== 'undefined') ?  address : 'Mountain View';
  return `To: ${name} In: ${address}`;
}
```

Which of the following choices is the correct way to write the `shippingLabel()` function using default function parameters?

```javascript
function shippingLabel(name = '', address = '') {
  return `To ${name} In: ${address}`;
}
```

```javascript
function shippingLabel(name, address) {
  name = name || 'Richard';
  address = address || 'Mountain View';
  return `To: ${name} In: ${address}`;
}
```

```javascript
function shippingLabel(name, address) {
  return `To: ${name} In: ${address}`;
}
```

```javascript
function shippingLabel(name = 'Richard', address = 'Mountain View') {
  return `To: ${name} In: ${address}`;
}
```

<details>
  <summary><em>Solution</em></summary>

> Option 4 uses default function parameters correctly by setting the defaults directly to the parameters.

```javascript
function shippingLabel(name = 'Richard', address = 'Mountain View') {
  return `To: ${name} In: ${address}`;
}
```

</details>

### 2.10. Defaults and Destructuring

#### Defaults and destructuring arrays

> You can combine default function parameters with destructuring to create some pretty powerful functions!
>
> ```javascript
> function createGrid([width = 5, height = 5]) {
>   return `Generates a ${width} x ${height} grid`;
> }
>
> createGrid([]); // Generates a 5 x 5 grid
> createGrid([2]); // Generates a 2 x 5 grid
> createGrid([2, 3]); // Generates a 2 x 3 grid
> createGrid([undefined, 3]); // Generates a 5 x 3 grid
> ```
>
> Returns:
>
> ```text
> Generates a 5 x 5 grid
> Generates a 2 x 5 grid
> Generates a 2 x 3 grid
> Generates a 5 x 3 grid
> ```
>
> The `createGrid()` function expects an array to be passed to it. It uses destructuring to set the first item in the array to the `width` and the second item to be the `height`. If the array is empty or if it has only one item in it, then the default parameters kick in and give the missing parameters a default value of `5`.
>
> There is a problem with this though, the following code will not work:
>
> ```javascript
> createGrid(); // throws an error
> ```
>
> ```text
> Uncaught TypeError:** Cannot read property 'Symbol(Symbol.iterator)' of undefined
> ```
>
> This throws an error because `createGrid()` expects an array to be passed in that it will then destructure. Since the function was called without passing an array, it breaks. But, we can use default function parameters for this!
>
> ```javascript
> function createGrid([width = 5, height = 5] = []) {
>   return `Generates a ${width} x ${height} grid`;
> }
> ```
>
> See that new `= []` in the function's parameter? If `createGrid()` is called without any argument then it will use this default empty array. And since the array is empty, there's nothing to destructure into `width` and `height`, so their default values will apply! So by adding `= []` to give the entire parameter a default, the following code will now work:
>
> ```javascript
> createGrid(); // Generates a 5 x 5 grid
> ```
>
> Returns:
>
> ```text
> Generates a 5 x 5 grid
> ```

#### 2.10 Mini-Quiz Question 1 of 2

Take a look at the following code:

```javascript
function houseDescriptor([houseColor = 'green', shutterColors = ['red']]) {
  return `I've a ${houseColor} house w/ ${shutterColors.join(' and ')} shutters`;
}
```

Which of the following choices will run without throwing an error?

- `houseDescriptor('red', ['white', 'gray', 'pink']);`
- `houseDescriptor(['green', ['white', 'gray', 'pink']]);`
- `houseDescriptor(['blue', 'purple']);`
- `houseDescriptor(['green]);`

<details>
  <summary><em>Solution</em></summary>

> Options 2 and 4 are the only choices that will run correctly without throwing an error.

*[Additional notes from James Priest](https://github.com/james-priest/100-days-of-code-log-r2/blob/master/ES6-Functions.md#solution-7):*

> - Since `houseDescriptor` is expecting only a single argument (an array) to be passed in, Option 1 has to be incorrect since it's calling the function with two arguments.
> - Option 2 is correct.
> - Option 3 does call the function with a single array argument, but the second item in the list is a string and `.join()` is not a method of strings, so the code throws an error.
> - Option 4 is correct.

</details>

#### Defaults and destructuring objects

> Just like array destructuring with array defaults, a function can have an object be a default parameter and use object destructuring:
>
> ```javascript
> function createSundae({scoops = 1, toppings = ['Hot Fudge']}) {
>   const scoopText = scoops === 1 ? 'scoop' : 'scoops';
>   return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
> }
>
> createSundae({});
> // Your sundae has 1 scoop with Hot Fudge toppings.
> createSundae({scoops: 2});
> // Your sundae has 2 scoops with Hot Fudge toppings.
> createSundae({scoops: 2, toppings: ['Sprinkles']});
> // Your sundae has 2 scoops with Sprinkles toppings.
> createSundae({toppings: ['Cookie Dough']});
> // Your sundae has 1 scoop with Cookie Dough toppings.
> ```
>
> Returns:
>
> ```text
> Your sundae has 1 scoop with Hot Fudge toppings.
> Your sundae has 2 scoops with Hot Fudge toppings.
> Your sundae has 2 scoops with Sprinkles toppings.
> Your sundae has 1 scoop with Cookie Dough toppings.
> ```
>
> Just like the array example before, if you try calling the function without any arguments it won't work:
>
> ```javascript
> createSundae(); // throws an error
> ```
>
> ```text
> Uncaught TypeError: Cannot match against 'undefined' or 'null'.
> ```
>
> We can prevent this issue by providing a default object to the function:
>
> ```javascript
> function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) {
>   const scoopText = scoops === 1 ? 'scoop' : 'scoops';
>   return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
> }
> ```
>
> By adding an empty object as the default parameter in case no arguments are provided, calling the function without any arguments now works.
>
> ```javascript
> createSundae(); // Your sundae has 1 scoop with Hot Fudge toppings.
> ```
>
> Returns:
>
> ```text
> Your sundae has 1 scoop with Hot Fudge toppings.
> ```

#### 2.10 Mini-Quiz Question 2 of 2

Take a look at the following code:

```javascript
function houseDescriptor({houseColor = 'green', shutterColors = ['red']} = {}) {
  return `I have a ${houseColor} house with ${shutterColors.join(' and ')} shutters`;
}
```

Which of the following choices will run without throwing an error?

- `houseDescriptor({houseColor: 'red', shutterColors: ['white', 'gray', 'pink']});`
- `houseDescriptor({houseColor: 'red'});`
- `houseDescriptor();`
- `houseDescriptor({shutterColors: ['orange', 'blue']});`
- `houseDescriptor({});`

<details>
  <summary><em>Solution</em></summary>

> Actually, every single one of these function calls will work correctly!

*[Additional notes from James Priest](https://github.com/james-priest/100-days-of-code-log-r2/blob/master/ES6-Functions.md#solution-8):*

> The only option that would NOT work is:
>
> - houseDescriptor({houseColor: 'red', shutterColors: 'white'});<br>
>   Uncaught TypeError: `.join` is not a function of String. The function is expecting an array as the `shutterColors` property.

</details>

#### Array defaults vs. object defaults

> Default function parameters are a simple addition, but it makes our lives so much easier! One benefit of object defaults over array defaults is how they handle skipped options. Check this out:
>
> ```javascript
> function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) { }
> ```
>
> With the `createSundae()` function using object defaults with destructuring, if you want to use the default value for `scoops` but change the `toppings`, then all you need to do is pass in an object with `toppings`:
>
> ```javascript
> createSundae({toppings: ['Hot Fudge', 'Sprinkles', 'Caramel']});
> ```
>
> Compare the above example with the same function that uses array defaults with destructuring.
>
> ```javascript
> function createSundae([scoops = 1, toppings = ['Hot Fudge']] = []) { }
> ```
>
> With this function setup, if you want to use the default number of scoops but change the toppings, you'd have to call your function a little...oddly:
>
> ```javascript
> createSundae([undefined, ['Hot Fudge', 'Sprinkles', 'Caramel']]);
> ```
>
> Since arrays are positionally based, we have to pass `undefined` to "skip" over the first argument (and accept the default) to get to the second argument.
>
> **Unless you've got a strong reason to use array defaults with array destructuring, we recommend going with object defaults with object destructuring!**

### 2.11. Quiz: Using Default Function Parameters (2-2)

Create a `buildHouse()` function that accepts an object as a default parameter. The object should set the following properties to these default values:

- `floors = 1`
- `color = 'red'`
- `walls = 'brick'`

The function should return the following if no arguments or any empty object is passed to the function.

```text
Your house has 1 floor(s) with red brick walls.
```

Code:

```javascript
/*
 - Programming Quiz: Using Default Function Parameters (2-2)
 */

// your code goes here

// tests
console.log(buildHouse());
console.log(buildHouse({}));
console.log(buildHouse({floors: 3, color: 'yellow'}));
```

Output:

```text
Your house has 1 floor(s) with red brick walls.
Your house has 1 floor(s) with red brick walls.
Your house has 3 floor(s) with yellow brick walls.
```

<details>
  <summary><em>Solution</em></summary>

You basically have to tell the function two things:

1. What it should contain
2. What the output should be

The sample code from the tests helps suggest the function formatting.

```javascript
// function
function buildHouse({floors = 1, color = 'red', walls = 'brick'} = {}) {
  return `Your house has ${floors} floor(s) with ${color} ${walls} walls.`;
}

// tests
console.log(buildHouse());
console.log(buildHouse({}));
console.log(buildHouse({floors: 3, color: 'yellow'}));
```

```text
Your house has 1 floor(s) with red brick walls.
Your house has 1 floor(s) with red brick walls.
Your house has 3 floor(s) with yellow brick walls.
```

> What Went Well
>
> - Your code should have a function `buildHouse()`
> - Your `buildHouse()` function should have one parameter
> - Your `buildHouse()` function should accept an object and an empty object as a default parameter
> - Your `buildHouse()` function should set the `floors`, `color`, and `walls` properties to default values
> - Your `buildHouse()` function should produce the correct output when no arguments or any empty object is passed to it
> - Your `buildHouse()` function should produce the correct output when a valid object is passed to it
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

[(Back to top)](#top)

## JavaScript Classes

### 2.12. Class Preview

#### Class Preview

> Here's a quick peek of what a JavaScript class looks like:
>
> ```javascript
> class Dessert {
>   constructor(calories = 250) {
>     this.calories = calories;
>   }
> }
>
> class IceCream extends Dessert {
>   constructor(flavor, calories, toppings = []) {
>     super(calories);
>     this.flavor = flavor;
>     this.toppings = toppings;
>   }
>   addTopping(topping) {
>     this.toppings.push(topping);
>   }
> }
> ```
>
> Notice the new `class` keyword right in front of `Dessert` and `IceCream`, or the new `extends` keyword in `class IceCream extends Dessert`? What about the call to `super()` inside the IceCream's `constructor()` method.
>
> There are a bunch of new keywords and syntax to play with when creating JavaScript classes. But, before we jump into the specifics of how to write JavaScript classes, we want to point out a rather confusing part about JavaScript compared with class-based languages.

### 2.13. JavaScript's Illusion of Classes

- In other languages, we use functions to create classes and provide inheritance.
- **JavaScript is not a class-based language. The classes are just a mirage over prototypal inheritance.**
- In JavaScript, we use functions to create objects.
- JavaScript links objects together by "prototypal inheritance."

### 2.14. JavaScript Classes

#### ES5 "Class" Recap

> Since ES6 classes are just a mirage and hide the fact that prototypal inheritance is actually going on under the hood, let's quickly look at how to create a "class" with ES5 code:
>
> ```javascript
> function Plane(numEngines) {
>   this.numEngines = numEngines;
>   this.enginesActive = false;
> }
>
> // methods "inherited" by all instances
> Plane.prototype.startEngines = function () {
>   console.log('starting engines...');
>   this.enginesActive = true;
> };
>
> const richardsPlane = new Plane(1);
> richardsPlane.startEngines();
>
> const jamesPlane = new Plane(4);
> jamesPlane.startEngines();
> ```
>
> In the code above, the `Plane` function is a constructor function that will create new Plane objects. The data for a specific Plane object is passed to the `Plane` function and is set on the object. Methods that are "inherited" by each Plane object are placed on the `Plane.prototype` object. Then `richardsPlane` is created with one engine while `jamesPlane` is created with 4 engines. Both objects, however, use the same `startEngines` method to activate their respective engines.
>
> Things to note:
>
> - the constructor function is called with the `new` keyword
> - the constructor function, by convention, starts with a capital letter
> - the constructor function controls the setting of data on the objects that will be created
> - "inherited" methods are placed on the constructor function's prototype object
>
> Keep these in mind as we look at how ES6 classes work because, remember, ES6 classes set up all of this for you under the hood.

#### ES6 Classes

> Here's what that same Plane class would look like if it were written using the new class syntax:
>
> ```javascript
> class Plane {
>   constructor(numEngines) {
>     this.numEngines = numEngines;
>     this.enginesActive = false;
>   }
>
>   startEngines() {
>     console.log('starting engines…');
>     this.enginesActive = true;
>   }
> }
> ```

### 2.15. Convert a Function to a Class

> Let's convert this function into a class.
>
> ```javascript
> // ES5 Syntax
> function Plane(numEngines) {
>   this.numEngines = numEngines;
>   this.enginesActive = false;
> }
>
> Plane.prototype.startEngines = function () {
>   console.log('starting engines...');
>   this.enginesActive = true;
> }
>
> var richardsPlane = new Plane(1);
> richardsPlane.startEngines();
>
> var jamesPlane = new Plane(4);
> jamesPlane.startEngines();
> ```
>
> Everything inside the constructor function is now placed inside a method with the name constructor.
>
> ```javascript
> // ES6 Syntax
> class Plane {
>   constructor(numEngines) {
>     this.numEngines = numEngines;
>     this.enginesActive = false;
>   }
> }
> ```
>
> This constructor method will automatically run when a new object is constructed from this class. If any data is needed to create the object then it needs to be included here.
>
> So this takes care of creating an object. Now the methods that all objects inherit are placed inside the class.
>
> ```javascript
> // ES6 Syntax
> class Plane {
>   constructor(numEngines) {
>     this.numEngines = numEngines;
>     this.enginesActive = false;
>   }
>
>   startEngines() {
>     console.log('starting engines...');
>     this.enginesActive = true;
>   }
> }
> ```
>
> `startEngines()` exists on the prototype explicitly in the pre-class way of writing it. Now it appears inside the class but the functionality is exactly the same.
>
> Also it looks like `startEngines()` and this `constructor()` method are the same kind of method but the constructor method is not on the prototype. It's a new special method that exists in a class and is used to initialize new objects.
>
> To drive this home, the functionality of these two is exactly the same. The class syntax is just a nicer way of writing it. In fact, we create new objects in exactly the
> same way with this new class syntax.
>
> ```javascript
> // ES6 Syntax
> class Plane {
>   constructor(numEngines) {
>     this.numEngines = numEngines;
>     this.enginesActive = false;
>   }
>
>   startEngines() {
>     console.log('starting engines...');
>     this.enginesActive = true;
>   }
> }
>
> var richardsPlane = new Plane(1);
> richardsPlane.startEngines();
>
> var jamesPlane = new Plane(1);
> jamesPlane.startEngines();
> ```
>
> If you already understand prototypal inheritance then you already have a good understanding of how `class` and class methods work.

### 2.16. Working with JavaScript Classes

#### Class is just a function

> Just to prove that there isn't anything special about `class`, check out this code:
>
> ```javascript
> class Plane {
>   constructor(numEngines) {
>     this.numEngines = numEngines;
>     this.enginesActive = false;
>   }
>
>   startEngines() {
>     console.log('starting engines…');
>     this.enginesActive = true;
>   }
> }
>
> typeof Plane; // function
> ```
>
> Returns:
>
> ```text
> function
> ```
>
>
> That's right—it's just a function! There isn't even a new type added to JavaScript.
>
>
> ⚠️ Where Are All The Commas? ⚠️
>
> Did you notice that there aren't any commas between the method definitions in the Class? Commas are not used to separate properties or methods in a Class. If you add them, you'll get a `SyntaxError` of `unexpected token ,`

#### 2.16 Mini-Quiz Question

Take a look at the following code:

```javascript
class Animal {
  constructor(name = 'Sprinkles', energy = 100) {
    this.name = name;
    this.energy = energy;
  }

  eat(food) {
    this.energy += food / 3;
  }
}
```

Which of the following are true?

- the `eat()` method ends up `onAnimal.prototype`
- `typeof Animal === 'class'`
- `typeof Animal === 'function'`

<details>
  <summary><em>Solution</em></summary>

> Options 1 and 3 are both true. Methods that appear in the class definition are placed on that class's prototype object and a class is just a function.

</details>

#### Static methods

> To add a static method, the keyword `static` is placed in front of the method name. Look at the `badWeather()` method in the code below.
>
> ```javascript
> class Plane {
>   constructor(numEngines) {
>     this.numEngines = numEngines;
>     this.enginesActive = false;
>   }
>
>   static badWeather(planes) {
>     for (plane of planes) {
>       plane.enginesActive = false;
>     }
>   }
>
>   startEngines() {
>     console.log('starting engines…');
>     this.enginesActive = true;
>   }
> }
> ```
>
> See how `badWeather()` has the word `static` in front of it while `startEngines()` doesn't? That makes `badWeather()` a method that's accessed directly on the `Plane` class, so you can call it like this:
>
> ```javascript
> Plane.badWeather([plane1, plane2, plane3]);
> ```
>
> **NOTE:** A little hazy on how constructor functions, class methods, or prototypal inheritance works? We've got a course on it! Check out [Object Oriented JavaScript](https://www.udacity.com/course/object-oriented-javascript--ud015).

#### Benefits of classes

> 1. Less setup
>     - There's a lot less code that you need to write to create a function
> 2. Clearly defined constructor function
>     - Inside the class definition, you can clearly specify the constructor function.
> 3. Everything's contained
>     - All code that's needed for the class is contained in the class declaration. Instead of having the constructor function in one place, then adding methods to the prototype one-by-one, you can do everything all at once!

#### Things to look out for when using classes

> 1. `class` is not magic
>     - The `class` keyword brings with it a lot of mental constructs from other, class-based languages. It doesn't magically add this functionality to JavaScript classes.
> 2. `class` is a mirage over prototypal inheritance
>     - We've said this many times before, but under the hood, a JavaScript class just uses prototypal inheritance.
> 3. Using classes requires the use of `new`
>     - When creating a new instance of a JavaScript class, the `new` keyword **must be used**
>
> For example,
>
> ```javascript
> class Toy {
>   // some class code
> }
>
> const myToy1 = Toy(); // throws an error
> ```
>
> ```text
> Uncaught TypeError: Class constructor Toy cannot be invoked without 'new'
> ```
>
> ```javascript
> const myToy2 = new Toy(); // this works!
> ```

### 2.17. Super and Extends

> Now that we've looked at creating classes in JavaScript. Let's use the new `super` and `extends` keywords to extend a class.
>
> ```javascript
> // ES6 --------------------------------------
> class Tree {
>   constructor(size = '10', leaves = {
>       spring: 'green',
>       summer: 'green',
>       fall: 'orange',
>       winter: null}) {
>     this.size = size;
>     this.leaves = leaves;
>     this.leafColor = null;
>   }
>
>   changeSeason(season) {
>     this.leafColor = this.leaves[season];
>     if (season === 'spring') {
>       this.size += 1;
>     }
>   }
> }
>
> class Maple extends Tree {
>   constructor(syrupQty = 15, size, leaves) {
>     super(size, leaves);
>     this.syrupQty = syrupQty;
>   }
>
>   changeSeason(season) {
>     super.changeSeason(season);
>     if (season === 'spring') {
>       this.syrupQty += 1;
>     }
>   }
>
>   gatherSyrup() {
>     this.syrupQty -= 3;
>   }
> }
>
> const myMaple = new Maple(15, 5);
> myMaple.changeSeason('fall');
> myMaple.gatherSyrup();
> myMaple.changeSeason('spring');
> ```
>
> Both `Tree` and `Maple` are JavaScript classes. The `Maple` class is a "subclass" of `Tree` and uses the `extends` keyword to set itself as a "subclass".
>
> To get from the "subclass" to the parent class, the `super` keyword is used. Did you notice that `super` was used in two different ways? In `Maple`'s constructor method, `super` is used as a function. In `Maple`'s `changeSeason()` method, `super` is used as an object!

#### Compared to ES5 subclasses

> Let's see this same functionality, but written in ES5 code:
>
> ```javascript
> // ES5 --------------------------------------
> function Tree() {
>   this.size = size || 10;
>   this.leaves = leaves || {
>     spring: 'green', summer: 'green', fall: 'orange', winter: null
>   };
>   this.leafColor;
> }
>
> Tree.prototype.changeSeason = function(season) {
>   this.leafColor = this.leaves[season];
>   if (season === 'spring') {
>     this.size += 1;
>   }
> }
>
> function Maple (syrupQty, size, leaves) {
>   Tree.call(this, size, leaves);
>   this.syrupQty = syrupQty || 15;
> }
>
> Maple.prototype = Object.create(Tree.prototype);
> Maple.prototype.constructor = Maple;
>
> Maple.prototype.changeSeason = function(season) {
>   Tree.prototype.changeSeason.call(this, season);
>   if (season === 'spring') {
>     this.syrupQty += 1;
>   }
> }
>
> Maple.prototype.gatherSyrup = function() {
>   this.syrupQty -= 3;
> }
>
> const myMaple = new Maple(15, 5);
> myMaple.changeSeason('fall');
> myMaple.gatherSyrup();
> myMaple.changeSeason('spring');
> ```
>
> Both this code and the class-style code above achieve the same functionality.

### 2.18. Extending Classes from ES5 to ES6

> Let's hide the inner workings of these classes to compare how they're constructed.
>
> ```javascript
> // ES5 --------------------------------------
> function Tree(size, leaves) {...}
> Tree.prototype.changeSeason = function (season) {...}
>
> function Maple(syrupQty, size, barkColor, leaves) {...}
> Maple.prototype = Object.create(Tree.prototype);
> Maple.prototype.constructor = Maple;
>
> Maple.prototype.changeSeason = function (season) {...}
> Maple.prototype.gatherSyrup = function () {...}
>
> // ES6 --------------------------------------
> class Tree {
>   constructor(size = '10', leaves = {...}) {...}
>   changeSeason(season) {...}
> }
>
> class Maple extends Tree {
>   constructor(syrupQty = 15, size, leaves) {...}
>   changeSeason(season) {...}
>   gatherSyrup() {...}
> }
> ```
>
> Remember that there's a new special method called the `constructor()` that's run whenever the class is called. It's doing the same thing as the `Tree` constructor in _ES5_.
>
> Also remember that a method inside of a class definition (`changeSeason`) is the same as adding that method to the prototype. That takes care of the base class which looks pretty similar to before.
>
> The bigger difference comes when extending the base class with a subclass. With the older ES5 code we'd have to:
>
> 1. Create another constructor function
> 2. Then set the function's prototype to the base class' prototype
> 3. Since we've overwritten the original prototype object, we need to set/reset the connection between the constructor property and the original constructor function.
>
> Then we're back to the normal routine of adding methods to the prototype object.
>
> Now compare all of the code it took to get these two functions connected and prototype linked in ES5 to the class code of ES6.
>
> It's just another class definition but it uses the extends keyword to connect the `Maple` class to the base class `Tree`.
>
> Significantly nicer right? It's also a lot easier to call the base class from the subclass.
>
> The es6 code uses the new `super` keyword while you have to use `.call` in the es5 code and pass `this` as the first argument.
>
> Also, calling a prototype method also takes a lot less code in the new class format too.

### 2.19. Working with JavaScript Subclasses

> Like most of the new additions, there's a lot less setup code and it's a lot cleaner syntax to create a subclass using `class`, `super`, and `extends`.
>
> Just remember that, under the hood, the same connections are made between functions and prototypes.

#### `super` must be called before `this`

> In a subclass constructor function, before `this` can be used, a call to the super class must be made.
>
> ```javascript
> class Apple {}
> class GrannySmith extends Apple {
>   constructor(tartnessLevel, energy) {
>     this.tartnessLevel = tartnessLevel; // `this` before `super` throws an error!
>     super(energy);
>   }
> }
> ```

#### 2.19 Mini-Quiz Question 1 of 2

Take a look at the following code:

```javascript
class Toy {}
class Dragon extends Toy {}
const dragon1 = new Dragon();
```

Given the code above, is the following statement true or false?

```javascript
dragon1 instanceof Toy;
```

<details>
  <summary><em>Solution</em></summary>

Got it on my first try.

> The `dragon1` variable is an object created by the `Dragon` class, and since the `Dragon` class extends the `Toy` class, `dragon1` is also considered an instance of `Toy`.

</details>

#### 2.19 Mini-Quiz Question 2 of 2

Let's say that a `Toy` class exists and that a `Dragon` class extends the `Toy` class.

What is the correct way to create a `Toy` object from inside the `Dragon` class's `constructor` method?

- `super();`
- `super.call(this)`
- `parent();`
- `Toy();`

<details>
  <summary><em>Solution</em></summary>

Got it on my first try again.

> Option 1 is the correct way to call the super class from within the subclass's constructor function.

</details>

### 2.20. Quiz: Building Classes and Subclasses (2-3)

Quiz

Create a `Bicycle` subclass that extends the `Vehicle` class. The `Bicycle` subclass should override `Vehicle`'s constructor function by changing the default values for `wheels` from `4` to `2` and `horn` from `'beep beep'` to `'honk honk'`.

```javascript
/*
 - Programming Quiz: Building Classes and Subclasses (2-3)
 */

class Vehicle {
  constructor(color = 'blue', wheels = 4, horn = 'beep beep') {
    this.color = color;
    this.wheels = wheels;
    this.horn = horn;
  }

  honkHorn() {
    console.log(this.horn);
  }
}

// your code goes here

/- tests
const myVehicle = new Vehicle();
myVehicle.honkHorn(); // beep beep
const myBike = new Bicycle();
myBike.honkHorn(); // honk honk
*/
```

Output:

```text
beep beep
honk honk
```

<details>
  <summary><em>Solution</em></summary>

```javascript
/*
 - Programming Quiz: Building Classes and Subclasses (2-3)
 */

class Vehicle {
  constructor(color = 'blue', wheels = 4, horn = 'beep beep') {
    this.color = color;
    this.wheels = wheels;
    this.horn = horn;
  }

  honkHorn() {
    console.log(this.horn);
  }
}

// your code goes here
class Bicycle extends Vehicle {
  constructor(color, wheels = 2, horn = 'honk honk') {
    super(color, wheels, horn);
    this.horn = horn;
  }
  honkHorn() {
    super.honkHorn();
  }
}

// tests
const myVehicle = new Vehicle();
myVehicle.honkHorn(); // beep beep
const myBike = new Bicycle();
myBike.honkHorn(); // honk honk
```

> What Went Well
>
> - Your code should have a class Vehicle
> - Your code should have a class Bicycle
> - Your class Bicycle should be a subclass of the class Vehicle
> - Your class Bicycle should have a constructor
> - Your Bicycle's constructor should set default values for color, wheels, and horn
> - Your Bicycle's constructor should override Vehicle's constructor as specified in the directions
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 2.21. Lesson 2 Summary

## Feedback on JavaScript ES6 lesson 2/4

Very helpful! Thank you!

[Next lesson](es6-3-built-ins.md)

[Previous lesson](es6-1-syntax.md)

[(Back to top)](#top)