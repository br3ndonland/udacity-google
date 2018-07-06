# JavaScript ES6 Syntax

<a href="https://www.udacity.com/">
  <img src="https://s3-us-west-1.amazonaws.com/udacity-content/rebrand/svg/logo.min.svg" width="300" alt="Udacity logo">
</a>

[ES6 - JavaScript Improved course](https://www.udacity.com/course/es6-javascript-improved--ud356) lesson 1/4

Udacity Google Mobile Web Specialist Nanodegree program part 3 lesson 04

Udacity Grow with Google Scholarship challenge course lesson 06

Brendon Smith

[br3ndonland](https://github.com/br3ndonland)

## Table of Contents <!-- omit in toc -->

- [Lesson plan](#lesson-plan)
- [Lesson Part 1: Declaring Variables](#lesson-part-1-declaring-variables)
  - [1.01. Harmony, ES6, ES2015](#101-harmony-es6-es2015)
  - [1.02. Let and Const](#102-let-and-const)
  - [1.03. Quiz: Using Let and Const (1-1)](#103-quiz-using-let-and-const-1-1)
  - [1.04. Template Literals](#104-template-literals)
  - [1.05. Quiz: Build an HTML Fragment (1-2)](#105-quiz-build-an-html-fragment-1-2)
  - [1.06. Destructuring](#106-destructuring)
  - [1.07. Quiz: Destructuring Arrays (1-3)](#107-quiz-destructuring-arrays-1-3)
  - [1.08. Object Literal Shorthand](#108-object-literal-shorthand)
  - [1.09. Lesson 1 Checkup](#109-lesson-1-checkup)
- [Lesson Part 2: Iteration](#lesson-part-2-iteration)
  - [1.10. Iteration](#110-iteration)
  - [1.11. Family of For Loops](#111-family-of-for-loops)
  - [1.12. For...of Loop](#112-forof-loop)
  - [1.13. Quiz: Writing a For...of Loop (1-4)](#113-quiz-writing-a-forof-loop-1-4)
  - [1.14. Spread... Operator](#114-spread-operator)
  - [1.15. ...Rest Parameter](#115-rest-parameter)
  - [1.16. Quiz: Using the Rest Parameter (1-5)](#116-quiz-using-the-rest-parameter-1-5)
  - [1.17. Lesson 1 Summary](#117-lesson-1-summary)
- [Feedback on JavaScript ES6 lesson 1/4](#feedback-on-javascript-es6-lesson-14)

## Lesson plan

1. Syntax
2. Functions
3. Built-Ins
4. Developer-Fu

## Lesson Part 1: Declaring Variables

### 1.01. Harmony, ES6, ES2015

> Welcome to the course on ES6! We're glad you're here! 👋
>
> This course is all about the new changes brought to the JavaScript programming language. We're expecting that you've worked with JavaScript for a couple of years and have an intermediate level of experience with the language.
>
> If you're new to the JavaScript language or would like a refresher, check out our [Intro to JavaScript course](https://www.udacity.com/course/intro-to-javascript--ud803).
>
> Follow us!
>
> - @parkesrjames
> - @richardkalehoff

ES6 brings some much-needed modernization to JavaScript. This is the biggest update to JavaScript ever.

These lessons are part of the free [ES6 - JavaScript Improved course](https://www.udacity.com/course/es6-javascript-improved--ud356).

The [ES6 spec](https://www.ecma-international.org/ecma-262/6.0/) came out in June 2015.

### 1.02. Let and Const

#### Intro

`let` and `const` are new keywords added to JavaScript.

> There are now two new ways to declare variables in JavaScript: let and const.
>
> Up until now, the only way to declare a variable in JavaScript was to use the keyword var. To understand why let and const were added, it’s probably best to look at an example of when using var can get us into trouble.
>
> Take a look at the following code.
>
> **Question 1 of 3**
>
> What do you expect to be the output from running `getClothing(false)`?

```javascript
function getClothing(isCold) {
  if (isCold) {
    var freezing = 'Grab a jacket!';
  } else {
    var hot = 'It’s a shorts kind of day.';
    console.log(freezing);
  }
}
```

Answer: `undefined`. Got this on the first try.

#### Hoisting

> Hoisting is a result of how JavaScript is interpreted by your browser. Essentially, before any JavaScript code is executed, all variables are "hoisted", which means they're raised to the top of the function scope. So at run-time, the getClothing() function actually looks more like this:

<img src="img/udacity-google-06-0201.png" alt="JavaScript hoisting" width="400px">

#### let and const

> Variables declared with `let` and `const` eliminate this specific issue of hoisting because they’re **scoped to the block, not to the function.** Previously, when you used `var`, variables were either scoped globally or locally to an entire function scope.
>
> If a variable is declared using `let` or `const` inside a block of code (denoted by curly braces `{ }`), then the variable is stuck in what is known as the **temporal dead zone** until the variable’s declaration is processed. This behavior prevents variables from being accessed only until after they’ve been declared.
>
> **Question 2 of 3**
>
> What do you expect to be the output from running `getClothing(false)`?

```javascript
function getClothing(isCold) {
  if (isCold) {
    const freezing = 'Grab a jacket!';
  } else {
    const hot = 'It’s a shorts kind of day.';
    console.log(freezing);
  }
}
```

Answer: `ReferenceError: freezing is not defined`.

> Because freezing is not declared inside the else statement, the function scope, or the global scope, a ReferenceError is thrown.

#### Rules for using let and const

> `let` and `const` also have some other interesting properties.
>
> - Variables declared with `let` can be reassigned, but can’t be redeclared in the same scope.
> - Variables declared with `const` must be assigned an initial value, but can’t be redeclared in the same scope, and can’t be reassigned.
>
> **Question 3 of 3**
>
> What do you expect to be output from running the following code?

```javascript
let instructor = 'James';
instructor = 'Richard';
console.log(instructor);
```

Answer: Richard. Got it on the first try.

> This is the correct way to use `let`. Use `let` to declare variables when you plan on changing the value of a variable later in your code.

#### Use cases

> The big question is when should you use `let` and `const`? The general rule of thumb is as follows:
>
> - use `let` when you plan to reassign new values to a variable, and
> - use `const` when you don’t plan on reassigning new values to a variable.
>
> Since `const` is the strictest way to declare a variable, we suggest that you always declare variables with `const` because it'll make your code easier to reason about since you know the identifiers won't change throughout the lifetime of your program. If you find that you need to update a variable or change it, then go back and switch it from `const` to `let`.
>
> That’s pretty straightforward, right? But what about `var`?

#### What about var

> **Is there any reason to use `var` anymore? Not really.**
>
> There are some arguments that can be made for using `var` in situations where you want to globally define variables, but this is often considered bad practice and should be avoided. From now on, we suggest ditching `var` in place of using `let` and `const`.

### 1.03. Quiz: Using Let and Const (1-1)

Quiz

Replace `var` with `let` or `const`

```javascript
/*
 - Programming Quiz: Using Let and Const (1-1)
 */

var CHARACTER_LIMIT = 255;
var posts = [
  "#DeepLearning transforms everything from self-driving cars to language translations. AND it's our new Nanodegree!",
  "Within your first week of the VR Developer Nanodegree Program, you'll make your own virtual reality app",
  "I just finished @udacity's Front-End Web Developer Nanodegree. Check it out!"
];

// prints posts to the console
function displayPosts() {
  for (var i = 0; i < posts.length; i++) {
    console.log(posts[i].slice(0, CHARACTER_LIMIT));
  }
}

displayPosts();
```

<details>
  <summary><em>Solution</em></summary>

```javascript
/*
 - Programming Quiz: Using Let and Const (1-1)
 */

const CHARACTER_LIMIT = 255;
const posts = [
  "#DeepLearning transforms everything from self-driving cars to language translations. AND it's our new Nanodegree!",
  "Within your first week of the VR Developer Nanodegree Program, you'll make your own virtual reality app",
  "I just finished @udacity's Front-End Web Developer Nanodegree. Check it out!"
];

// prints posts to the console
function displayPosts() {
  for (let i = 0; i < posts.length; i++) {
    console.log(posts[i].slice(0, CHARACTER_LIMIT));
  }
}

displayPosts();
```

> What Went Well
>
> - Your code should have a variable i
> - Your code should have a variable posts
> - Your code should have a variable CHARACTER_LIMIT
> - Your variable i should be declared using let
> - Your variable posts should be declared using const
> - Your variable CHARACTER_LIMIT should be declared using const
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 1.04. Template Literals

#### Intro to template literals

> Prior to ES6, the old way to concatenate strings together was by using the string concatenation operator ( + ).
>
> ```javascript
> const student = {
>   name: 'Richard Kalehoff',
>   guardian: 'Mr. Kalehoff'
> };
>
> const teacher = {
>   name: 'Mrs. Wilson',
>   room: 'N231'
> }
>
> let message = student.name + ' please see ' + teacher.name + ' in ' + teacher.room + ' to pick up your report card.';
> ```
>
> Returns:
>
> ```text
> Richard Kalehoff please see Mrs. Wilson in N231 to pick up your report card.
> ```
>
> This works alright, but it gets more complicated when you need to build multi-line strings.
>
> ```javascript
> let note = teacher.name + ',\n\n' +
>   'Please excuse ' + student.name + '.\n' +
>   'He is recovering from the flu.\n\n' +
>   'Thank you,\n' +
>   student.guardian;
> ```
>
> Returns:
>
> ```text
> Mrs. Wilson,
>
> Please excuse Richard Kalehoff.
> He is recovering from the flu.
>
> Thank you,
> Mr. Kalehoff
> ```
> However, that’s changed with the introduction of **template literals** (previously referred to as "template strings" in development releases of ES6).
>
> *NOTE:* As an alternative to using the string concatenation operator ( + ), you can use the `concat()` method, but both options are rather clunky for simulating true string interpolation.

#### Template Literals

> **Template literals** are essentially string literals that include embedded expressions.
>
> Denoted with backticks instead of single quotes or double quotes, template literals can contain placeholders which are represented using backticks. This makes it much easier to build strings.
>
> Here's the previous example using template literals.
>
> ```javascript
> const student = {
>   name: 'Richard Kalehoff',
>   guardian: 'Mr. Kalehoff'
> };
>
> const teacher = {
>   name: 'Mrs. Wilson',
>   room: 'N231'
> }
>
> let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`;
> console.log(message);
> ```
>
> Returns:
>
> ```text
> Richard Kalehoff please see Mrs. Wilson in N231 to pick up your report card.
> ```
>
> By using template literals, you can drop the quotes along with the string concatenation operator. Also, you can reference the object's properties inside expressions.

Template literals are similar to [Python new style string formatting](https://pyformat.info/), so they made sense to me.

Here's the code from above in Python for comparison:

```python
student = {
  "name": "Richard Kalehoff",
  "guardian": "Mr. Kalehoff"
  }

teacher = {
  "name": "Mrs. Wilson",
  "room": "N231"
  }

message = ('{} please see {} in {} to pick up your report card.'
           .format(student['name'], teacher['name'], teacher['room']))
print(message)

```

The JSON is read by Python as a dictionary. Note that it is no longer necessary to `import json` or parse the JSON with `json.loads(student)`.

#### Quiz

>Change the `greeting` string below to use a template literal. Also, feel free to swap in your name for the placeholder.

```javascript
/*
 - Instructions: Change the `greeting` string to use a template literal.
 */

const myName = '[NAME]';
const greeting = 'Hello, my name is ' + myName;
console.log(greeting);
```

<details>
  <summary><em>Solution</em></summary>

```javascript
const myName = '[NAME]';
const greeting = `Hello, my name is ${myName}`;
console.log(greeting);
```

> What Went Well
>
> - Your code should have a variable myName
> - Your code should have a variable greeting
> - Your code should have a template literal greeting
> - Your template literal should match the original greeting string
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

> ...but what about the multi-line example from before?
>
> ```javascript
> var note = teacher.name + ',\n\n' +
>   'Please excuse ' + student.name + '.\n' +
>   'He is recovering from the flu.\n\n' +
>   'Thank you,\n' +
>   student.guardian;
> ```
>
> Becomes:
>
> ```javascript
> var note = `${teacher.name},
>
>   Please excuse ${student.name}.
>   He is recovering from the flu.
>
>   Thank you,
>   ${student.guardian}`;
> ```
> Here’s where template literals really shine. In the animation above, the quotes and string concatenation operator have been dropped, as well as the newline characters ( \n ). That's because template literals also preserve newlines as part of the string!
>
> TIP: Embedded expressions inside template literals can do more than just reference variables. You can perform operations, call functions and use loops inside embedded expressions!

### 1.05. Quiz: Build an HTML Fragment (1-2)

Quiz

> Modify the createAnimalTradingCardHTML() function to use a template literal for cardHTML.

```javascript
/*
 - Programming Quiz: Build an HTML Fragment (1-2)
 */

const cheetah = {
    name: 'Cheetah',
    scientificName: 'Acinonyx jubatus',
    lifespan: '10-12 years',
    speed: '68-75 mph',
    diet: 'carnivore',
    summary: 'Fastest mammal on land, the cheetah can reach speeds of 60 or perhaps even 70 miles (97 or 113 kilometers) an hour over short distances. It usually chases its prey at only about half that speed, however. After a chase, a cheetah needs half an hour to catch its breath before it can eat.',
    fact: 'Cheetahs have “tear marks” that run from the inside corners of their eyes down to the outside edges of their mouth.'
};

// creates an animal trading card
function createAnimalTradingCardHTML(animal) {
    const cardHTML = '<div class="card">' +
        '<h3 class="name">' + animal.name + '</h3>' +
        '<img src="' + animal.name + '.jpg" alt="' + animal.name +'" class="picture">' +
        '<div class="description">' +
            '<p class="fact">' + animal.fact + '</p>' +
            '<ul class="details">' +
                '<li><span class="bold">Scientific Name</span>: ' + animal.scientificName + '</li>' +
                '<li><span class="bold">Average Lifespan</span>: ' + animal.lifespan + '</li>' +
                '<li><span class="bold">Average Speed</span>: ' + animal.speed + '</li>' +
                '<li><span class="bold">Diet</span>: ' + animal.diet + '</li>' +
            '</ul>' +
            '<p class="brief">' + animal.summary + '</p>' +
        '</div>' +
    '</div>';

    return cardHTML;
}

console.log(createAnimalTradingCardHTML(cheetah));

```

<details>
  <summary><em>Solution</em></summary>

```javascript
/*
 - Programming Quiz: Build an HTML Fragment (1-2)
 */

const cheetah = {
    name: 'Cheetah',
    scientificName: 'Acinonyx jubatus',
    lifespan: '10-12 years',
    speed: '68-75 mph',
    diet: 'carnivore',
    summary: 'Fastest mammal on land, the cheetah can reach speeds of 60 or perhaps even 70 miles (97 or 113 kilometers) an hour over short distances. It usually chases its prey at only about half that speed, however. After a chase, a cheetah needs half an hour to catch its breath before it can eat.',
    fact: 'Cheetahs have “tear marks” that run from the inside corners of their eyes down to the outside edges of their mouth.'
};

// creates an animal trading card
function createAnimalTradingCardHTML(animal) {
    const cardHTML = `<div class="card">
        <h3 class="name">${animal.name}</h3>
        <img src="${animal.name}.jpg" alt="${animal.name}" class="picture">
        <div class="description">
            <p class="fact">${animal.fact}</p>
            <ul class="details">
                <li><span class="bold">Scientific Name</span>: ${animal.scientificName}</li>
                <li><span class="bold">Average Lifespan</span>: ${animal.lifespan}</li>
                <li><span class="bold">Average Speed</span>: ${animal.speed}</li>
                <li><span class="bold">Diet</span>: ${animal.diet}</li>
            </ul>
            <p class="brief">${animal.summary}</p>
        </div>
    </div>`;

    return cardHTML;
}

console.log(createAnimalTradingCardHTML(cheetah));
```

> What Went Well
>
> - Your code should have an object cheetah
> - Your code should have a function createAnimalTradingCardHTML()
> - The createAnimalTradingCardHTML function should have a variable cardHTML
> - The cardHTML variable should be a template literal
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 1.06. Destructuring

#### Intro to destructuring

> In ES6, you can extract data from arrays and objects into distinct variables using **destructuring**.
>
> This probably sounds like something you’ve done before, for example, look at the two code snippets below that extract data using pre-ES6 techniques:
>
> ```javascript
> const point = [10, 25, -34];
>
> const x = point[0];
> const y = point[1];
> const z = point[2];
>
> console.log(x, y, z);
> ```
>
> Prints: `10 25 -34`
>
> The example above shows extracting values from an array.
>
> ```javascript
> const gemstone = {
>   type: 'quartz',
>   color: 'rose',
>   carat: 21.29
> };
>
> const type = gemstone.type;
> const color = gemstone.color;
> const carat = gemstone.carat;
>
> console.log(type, color, carat);
> ```
>
> Prints: `quartz rose 21.29`
>
> And this example shows extracting values from an object.
>
> Both are pretty straightforward, however, neither of these examples are actually using destructuring.
>
> So what exactly is **destructuring**?

#### Destructuring

> **Destructuring** borrows inspiration from languages like [Perl](https://en.wikipedia.org/wiki/Perl) and [Python](https://en.wikipedia.org/wiki/Python_%28programming_language%29) by allowing you to specify the elements you want to extract from an array or object *on the left side of an assignment*. It sounds a little weird, but you can actually achieve the same result as before, but with much less code; and it's still easy to understand.
>
> Let’s take a look at both examples rewritten using destructuring.

##### Destructuring values from an array

> ```javascript
> const point = [10, 25, -34];
>
> const [x, y, z] = point;
>
> console.log(x, y, z);
> ```
>
> Prints: `10 25 -34`
>
> In this example, the brackets `[ ]` represent the array being destructured and `x`, `y`, and `z` represent the variables where you want to store the values from the array. Notice how you don’t have to specify the indexes for where to extract the values from because the indexes are implied.
>
> TIP: You can also ignore values when destructuring arrays. For example, const [x, , z] = point; ignores the y coordinate and discards it.
>
> **Question 1 of 2**
>
> What do you expect to be the value of `second` after running the following code?
> ```javascript
> let positions = ['Gabrielle', 'Jarrod', 'Kate', 'Fernando', 'Mike', 'Walter'];
> let [first, second, third] = positions;
> ```

Answer: Jarrod. Got it on the first try.

> The variables first, second, and third get populated with the first 3 values in the positions array while the remaining values are ignored.

##### Destructuring values from an object

> ```javascript
> const gemstone = {
>   type: 'quartz',
>   color: 'rose',
>   carat: 21.29
> };
>
> const {type, color, carat} = gemstone;
>
> console.log(type, color, carat);
> ```
>
> Prints: `quartz rose 21.29`
>
> In this example, the curly braces `{ }` represent the object being destructured and `type`, `color`, and `carat` represent the variables where you want to store the properties from the object. Notice how you don’t have to specify the property from where to extract the values. Because `gemstone` has a property named `type`, the value is automatically stored in the `type` variable. Similarly, `gemstone` has a `color` property, so the value of `color` automatically gets stored in the `color` variable. And it's the same with `carat`.
>
> TIP: You can also specify the values you want to select when destructuring an object. For example, `let {color} = gemstone;` will only select the `color` property from the `gemstone` object.
>
> **Question 2 of 2**
>
> What do you expect to be returned from calling `getArea()`?
>
> ```javascript
> const circle = {
>   radius: 10,
>   color: 'orange',
>   getArea: function() {
>     return Math.PI - this.radius - this.radius;
>   },
>   getCircumference: function() {
>     return 2 - Math.PI - this.radius;
>   }
> };
>
> let {radius, getArea, getCircumference} = circle;
> ```

Answer: NaN. Got it on my second try.

> Correct! Calling `getArea()` will return `NaN`. When you destructure the object and store the `getArea()` method into the `getArea` variable, it no longer has access to `this` in the `circle` object which results in an area that is `NaN`.

### 1.07. Quiz: Destructuring Arrays (1-3)

Use array destructuring to pull out the three colors from the array of things and store them into the variables one, two, and three.

```javascript
/*
 - Programming Quiz: Destructuring Arrays (1-3)
 *
 - Use destructuring to initialize the variables `one`, `two`, and `three`
 - with the colors from the `things` array.
 */

const things = ['red', 'basketball', 'paperclip', 'green', 'computer', 'earth', 'udacity', 'blue', 'dogs'];

const one = things;
const two = '';
const three = '';

const colors = `List of Colors
1. ${one}
2. ${two}
3. ${three}`;

console.log(colors);
```

<details>
  <summary><em>Solution</em></summary>

First attempt

Found that the arrays are zero indexed like Python.

```javascript
const things = ['red', 'basketball', 'paperclip', 'green', 'computer', 'earth', 'udacity', 'blue', 'dogs'];

const one = things[0];
const two = things[3];
const three = things[7];

const colors = `List of Colors
1. ${one}
2. ${two}
3. ${three}`;

console.log(colors);
```

```text
List of Colors
1. red
2. green
3. blue
```

> What Went Well
>
> - Your code should have a variable things
> - Your code should set variable one correctly
> - Your code should set variable two correctly
> - Your code should set variable three correctly
>
> What Went Wrong
>
> - Your code doesn't seem to be using array destructuring to access the colors
>
> Feedback
>
> Not everything is correct yet, but you're close!

Solution

The solution produces the same answer, but using commas to skip items in the array instead of slicing. It was a little weird that they taught us the slicing method in [6.06. Destructuring](#606-destructuring), and not the comma method, but expected us to use the comma method here.

```javascript
const things = ['red', 'basketball', 'paperclip', 'green', 'computer', 'earth', 'udacity', 'blue', 'dogs'];

const [one,,, two,,,, three] = things;

const colors = `List of Colors
1. ${one}
2. ${two}
3. ${three}`;

console.log(colors);
```

```text
List of Colors
1. red
2. green
3. blue
```

> What Went Well
>
> - Your code should have a variable things
> - Your code should set variable one correctly
> - Your code should set variable two correctly
> - Your code should set variable three correctly
> - Your code should use destructuring
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 1.08. Object Literal Shorthand

#### Intro to object literal shorthand

> A recurring trend in ES6 is to remove unnecessary repetition in your code. By removing unnecessary repetition, your code becomes easier to read and more concise. This trend continues with the introduction of new shorthand ways for initializing objects and adding methods to objects.
>
> Let’s see what those look like.

#### Object literal shorthand

> You’ve probably written code where an object is being initialized using the same property names as the variable names being assigned to them.
>
> But just in case you haven’t, here’s an example.
>
> ```javascript
> let type = 'quartz';
> let color = 'rose';
> let carat = 21.29;
>
> const gemstone = {
>   type: type,
>   color: color,
>   carat: carat
> };
>
> console.log(gemstone);
> ```
>
> Prints: `Object {type: "quartz", color: "rose", carat: 21.29}`
>
> Do you see the repetition? Doesn't `type: type`, `color: color`, and `carat: carat` seem redundant?
>
> The good news is that you can remove those duplicate variables names from object properties *if* the properties have the same name as the variables being assigned to them.
>
> Check it out!
>
> ```javascript
> let type = 'quartz';
> let color = 'rose';
> let carat = 21.29;
>
> let gemstone = { type, color, carat };
> ```
>
> Speaking of shorthand, there’s also a shorthand way to add methods to objects.
>
> To see how that looks, let’s start by adding a `calculateWorth()` method to our `gemstone` object. The `calculateWorth()` method will tell us how much our gemstone costs based on its `type`, `color`, and `carat`.
>
> ```javascript
> let type = 'quartz';
> let color = 'rose';
> let carat = 21.29;
>
> const gemstone = {
>   type,
>   color,
>   carat,
>   calculateWorth: function() {
>     // will calculate worth of gemstone based on type, color, and carat
>   }
> };
> ```
>
> In this example, an anonymous function is being assigned to the property `calculateWorth`, but is the **function** keyword really needed? In ES6, it’s not!

#### Shorthand method names

> Since you only need to reference the gemstone’s `calculateWorth` property in order to call the function, having the function keyword is redundant, so it can be dropped.
>
> ```javascript
> let gemstone = {
>   type,
>   color,
>   carat,
>   calculateWorth() { ... }
> };
> ```

### 1.09. Lesson 1 Checkup

We're about halfway through the lesson.

Declaring variables:

- `let` & `const`
- template literals
- destructuring
- object literal shorthand

[(Back to top)](#top)

## Lesson Part 2: Iteration

### 1.10. Iteration

Iteration will be an important concept for the rest of the lesson.

James and Richard explained it with a `for` loop.

- The variable `i` is typically used to iterate because "iterator" starts with an i.

  ```javascript
  const years = ['1999', '2001', '2013', '2016'];

  for (let i = 0; i < years.length; i++) {
    console.log(years[i]);
  }
  ```

- ES6 features a new **iterable protocol** that allows JavaScript objects to **define their iteration behavior**.
- The new **for... of loop** iterates over iterable objects.

### 1.11. Family of For Loops

#### Intro to loops

> The **for...of loop** is the most recent addition to the family of for loops in JavaScript.
>
> It combines the strengths of its siblings, the **for loop** and the **for...in loop**, to loop over any type of data that is **iterable** (meaning it follows the [iterable protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols) which we'll look at in lesson 3). By default, this includes the data types String, Array, Map, and Set—notably absent from this list is the `Object` data type (i.e. `{}`). Objects are not iterable, by default.
>
> Before we look at the for...of loop, let’s first take a quick look at the other for loops to see where they have weaknesses.

#### The for loop

> The for loop is obviously the most common type of loop there is, so this should be a quick refresher.
>
> ```javascript
> const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
>
> for (let i = 0; i < digits.length; i++) {
>   console.log(digits[i]);
> }
> ```
>
> Prints:
>
> ```text
> 0
> 1
> 2
> 3
> 4
> 5
> 6
> 7
> 8
> 9
> ```
>
> Really the biggest downside of a for loop is having to keep track of the **counter** and **exit condition**.
>
> In this example, we’re using the variable `i` as a counter to keep track of the loop and to access values in the array. We’re also using `digits.length` to determine the exit condition for the loop. If you just glance at this code, it can sometimes be confusing exactly what’s happening; especially for beginners.
>
> While for loops certainly have an advantage when looping through arrays, some data is not structured like an array, so a for loop isn’t always an option.

#### The for...in loop

> The for...in loop improves upon the weaknesses of the for loop by **eliminating the counting logic and exit condition**.
>
> ```javascript
> const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
>
> for (const index in digits) {
>   console.log(digits[index]);
> }
> ```
>
> Prints:
>
> ```text
> 0
> 1
> 2
> 3
> 4
> 5
> 6
> 7
> 8
> 9
> ```
>
> But, you still have to deal with the issue of using an **index** to access the values of the array, and that stinks; it almost makes it more confusing than before.
>
> Also, the for...in loop can get you into big trouble when you need to add an extra method to an array (or another object). Because for...in loops loop over all enumerable properties, this means if you add any additional properties to the array's prototype, then those properties will also appear in the loop.
>
> ```javascript
> Array.prototype.decimalfy = function() {
>   for (let i = 0; i < this.length; i++) {
>     this[i] = this[i].toFixed(2);
>   }
> };
>
> const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
>
> for (const index in digits) {
>   console.log(digits[index]);
> }
> ```
>
> Prints:
>
> ```text
> 0
> 1
> 2
> 3
> 4
> 5
> 6
> 7
> 8
> 9
> function() {
>  for (let i = 0; i < this.length; i++) {
>   this[i] = this[i].toFixed(2);
>  }
> }
> ```
>
> Gross! This is why for...in loops are discouraged when looping over arrays.
>
> NOTE: The **forEach loop** is another type of for loop in JavaScript. However, `forEach()` is actually an array method, so it can only be used exclusively with arrays. There is also no way to stop or break a forEach loop. If you need that type of behavior in your loop, you’ll have to use a basic for loop.

### 1.12. For...of Loop

#### Intro to for of loops

> Finally, we have the mighty for...of loop.

#### For...of loop

##### Description

> The **for...of loop** is used to loop over any type of data that is iterable.
>
> You write a **for...of loop** almost exactly like you would write a for...in loop, except you swap out `in` with `of` and you can **drop the index**.
>
> ```javascript
> const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
>
> for (const digit of digits) {
>   console.log(digit);
> }
> ```
>
> Prints:
>
> ```text
> 0
> 1
> 2
> 3
> 4
> 5
> 6
> 7
> 8
> 9
> ```
>
> **This makes the for...of loop the most concise version of all the for loops.**
>
> TIP: It’s good practice to use plural names for objects that are collections of values. That way, when you loop over the collection, you can use the singular version of the name when referencing individual values in the collection. For example, `for (const button of buttons) {...}`.

##### Comparison of loops

```javascript
// comparison of javascript loops

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

// for loop
for (let i = 0; i < digits.length; i++) {
  console.log(digits[i]);
}

// for...in  loop
for (let index in digits) {
  console.log(digits[index]);
}

// for...of loop
for (let digits of digit) {
  console.log(digit);
}
```

Equivalent loop in Python:

```python
digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
for digit in digits:
  print(digit)
```

##### Additional benefits of for...of loops

> But wait, there’s more! The for...of loop also has some additional benefits that fix the weaknesses of the for and for...in loops.
>
> You can **stop or break a for...of loop at any time**.
>
> ```javascript
> const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
>
> for (const digit of digits) {
>   if (digit % 2 === 0) {
>     continue;
>   }
>   console.log(digit);
> }
> ```
>
> Prints:
>
> ```text
> 1
> 3
> 5
> 7
> 9
> ```
>
> And you don’t have to worry about adding new properties to objects. **The for...of loop will only loop over the values in the object.**
>
> ```javascript
> Array.prototype.decimalfy = function() {
>   for (i = 0; i < this.length; i++) {
>     this[i] = this[i].toFixed(2);
>   }
> };
>
> const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
>
> for (const digit of digits) {
>   console.log(digit);
> }
> ```
>
> Prints:
>
> ```text
> 0
> 1
> 2
> 3
> 4
> 5
> 6
> 7
> 8
> 9
> ```

### 1.13. Quiz: Writing a For...of Loop (1-4)

Write a for...of loop that:

- loops through each day in the days array
- capitalizes the first letter of the day
- and prints the day out to the console

Your code should log the following to the console:

```text
Sunday
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
```

```javascript
/*
 - Programming Quiz: Writing a For...of Loop (1-4)
 */

const days = ['sunday', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday'];

// your code goes here

```

<details>
  <summary><em>Solution</em></summary>

First attempt

Got the days to print on my first try:

```javascript
const days = ['sunday', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday'];

// your code goes here
for (const day of days) {
    console.log(day);
}
```

```text
sunday
monday
tuesday
wednesday
thursday
friday
saturday
```

Next, I need to capitalize the first letter of each day. In Python, this would be something like `letter.upper()`.

This didn't work:

```javascript
const days = ['sunday', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday'];

// your code goes here
for (const day of days) {
    day.upper();
    console.log(day);
}
```

I needed some reformatting:

```javascript
const days = ['sunday', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday'];

// your code goes here
for(let day of days) {
    let word = day[0].toUpperCase() + day.substr(1);
    console.log(word);
}
```

```text
Sunday
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
```

> What Went Well
>
> - Your code should have a variable days
> - Your variable days should be an array
> - Your variable days should contain the days of the week
> - Your for...of loop should loop through the days array
> - Your for...of loop should print each day capitalized to the console
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 1.14. Spread... Operator

#### Intro to spread operator

> Time to switch gears for a moment and check out the spread operator!

#### Spread operator

> The **spread operator**, written with three consecutive dots ( `...` ), is new in ES6 and gives you the ability to expand, or *spread*, [iterable objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators#Iterators) into multiple elements.
>
> Let’s take a look at a few examples to see how it works.
>
> ```javascript
> const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"];
> console.log(...books);
> ```
>
> Prints:
>
> ```text
> Don Quixote The Hobbit Alice in Wonderland Tale of Two Cities
> ```
>
> ```javascript
> const primes = new Set([2, 3, 5, 7, 11, 13, 17, 19, 23, 29]);
> console.log(...primes);
> ```
>
> Prints:
>
> ```text
> 2 3 5 7 11 13 17 19 23 29
> ```
>
> If you look at the output from the examples, notice that both the array and set have been expanded into their individual elements. So how is this useful?
>
> NOTE: Sets are a new built-in object in ES6 that we’ll cover in more detail in a future lesson.

#### Combining arrays with concat

> One example of when the spread operator can be useful is when combining arrays.
>
> If you’ve ever needed to combine multiple arrays, prior to the spread operator, you were forced to use the array’s `concat()` method.
>
> ```javascript
> const fruits = ["apples", "bananas", "pears"];
> const vegetables = ["corn", "potatoes", "carrots"];
> const produce = fruits.concat(vegetables);
> console.log(produce);
> ```
>
> Prints:
>
> ```text
> ["apples", "bananas", "pears", "corn", "potatoes", "carrots"]
> ```
>
> This isn’t terrible, but wouldn’t it be nice if there was a shorthand way to write this code?
>
> For example, something like...
>
> ⚠️ Upcoming `const` Warning ⚠️
>
> If you're following along by copy/pasting the code, then you've already declared the `produce` variable with the `const` keyword. The following code will try to redeclare *and- reassign the variable, so depending on how you're running the code, it might throw an error.
>
> Remember that variables declared with `const` cannot be redeclared or reassigned in the same scope.
>
> ```javascript
> const produce = [fruits, vegetables];
> console.log(produce);
> ```
>
> Prints:
>
> ```text
> [Array[3], Array[3]]
> ```
>
> Unfortunately, that doesn’t work.
>
> Instead of combining both arrays, this code actually adds the `fruits` array at the first index and the `vegetables` array at the second index of the `produce` array.
>
> How about trying the spread operator?

#### Mini-Quiz

```javascript
/*
 - Instructions: Use the spread operator to combine the `fruits` and `vegetables` arrays into the `produce` array.
 */

const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];

const produce = [];

console.log(produce);
```

<details>
  <summary><em>Solution</em></summary>

Got it on the first try! Was trying out Pomodoros with @Bree on Slack. Completed 1.14 in one 25 minute Pomodoro.

```javascript
const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];

const produce = [...fruits, ...vegetables];

console.log(produce);
```

```text
[ 'apples', 'bananas', 'pears', 'corn', 'potatoes', 'carrots' ]
```

> What Went Well
>
> - Your code should have a variable fruits
> - Your code should have a variable vegetables
> - Your code should have a variable produce
> - Your variable produce should be an array
> - Your variable produce should contain the values from the fruits array
> - Your variable produce should contain the values from the vegetables array
> - Your code should use spread operator to combine the fruits and vegetables arrays into the produce array
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 1.15. ...Rest Parameter

#### Intro to rest parameter

> If you can use the spread operator to *spread* an array into multiple elements, then certainly there should be a way to bundle multiple elements back into an array, right?
>
> In fact, there is! It’s called the **rest parameter**, and it’s another new addition in ES6.

#### Rest parameter

> The rest parameter, also written with three consecutive dots ( `...` ), allows you to represent an indefinite number of elements as an array. This can be helpful in a couple of different situations.
>
> One situation is when assigning the values of an array to variables. For example,
>
> ```javascript
> const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
> const [total, subtotal, tax, ...items] = order;
> console.log(total, subtotal, tax, items);
> ```
>
> Prints:
>
> ```text
> 20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]
> ```
>
> This code takes the values of the `order` array and assigns them to individual variables using **destructuring**. `total`, `subtotal`, and `tax` are assigned the first three values in the array, however, `items` is where you want to pay the most attention.
>
> By using the rest parameter, **`items` is assigned the rest of the values in the array** (as an array).
>
> ```javascript
> // spread
> const myPackage = ['cheese', 'eggs', 'milk', 'bread'];
> console.log(...myPackage);
> ```
>
> Prints:
>
> ```text
> cheese eggs milk bread
> ```
>
> ```javascript
> // rest
> printPackageContents('cheese', 'eggs', 'milk', 'bread');
>
> function printPackageContents(...items) {
>   for (const item of items) {
>     console.log(item);
>   }
> }
> ```
>
> You can **think of the rest parameter like the opposite of the spread operator**; if the spread operator is like unboxing all of the contents of a package, then the rest parameter is like taking all the contents and putting them back into the package.

#### Variadic functions

> Another use case for the rest parameter is when you’re working with variadic functions. Variadic functions are functions that take an indefinite number of arguments.
>
> For example, let’s say we have a function called `sum()` which calculates the sum of an indefinite amount of numbers. How might the `sum()` function be called during execution?
>
> ```javascript
> sum(1, 2);
> sum(10, 36, 7, 84, 90, 110);
> sum(-23, 3000, 575000);
> ```
>
> There’s literally an endless number of ways the `sum()` function could be called. Regardless of the amount of numbers passed to the function, it should always return the total sum of the numbers.

#### Using the arguments object

> In previous versions of JavaScript, this type of function would be handled using the [arguments object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments). The **arguments object** is an array-like object that is available as a local variable inside all functions. It contains a value for each argument being passed to the function starting at 0 for the first argument, 1 for the second argument, and so on.
>
> If we look at the implementation of our `sum()` function, then you’ll see how the arguments object could be used to handle the variable amount of numbers being passed to it.
>
> ```javascript
> function sum() {
>   let total = 0;
>   for(const argument of arguments) {
>     total += argument;
>   }
>   return total;
> }
> ```
>
> Now this works fine, but it does have its issues:
>
> 1. If you look at the definition for the `sum()` function, it doesn’t have any parameters.
>     - This is misleading because we know the `sum()` function can handle an indefinite amount of arguments.
> 2. It can be hard to understand.
>     - If you’ve never used the arguments object before, then you would most likely look at this code and wonder where the arguments object is even coming from. Did it appear out of thin air? It certainly looks that way.

#### Using the rest parameter

> Fortunately, with the addition of the rest parameter, you can rewrite the `sum()` function to read more clearly.
>
> ```javascript
> function sum(...nums) {
>   let total = 0;
>   for(const num of nums) {
>     total += num;
>   }
>   return total;
> }
> ```
>
> This version of the `sum()` function is both **more concise** and is **easier to read**. Also, notice the for...in loop has been replaced with the new **for...of loop**.

### 1.16. Quiz: Using the Rest Parameter (1-5)

Directions:

Use the rest parameter to create an `average()` function that calculates the average of an *unlimited- amount of numbers.

TIP: Make sure to test your code with different values. For example,

- `average(2, 6)` should return `4`
- `average(2, 3, 3, 5, 7, 10)` should return `5`
- `average(7, 1432, 12, 13, 100)` should return `312.8`
- `average()` should return `0`

```javascript
/*
 - Programming Quiz: Using the Rest Parameter (1-5)
 */

// your code goes here

function average() {

}

console.log(average(2, 6));
console.log(average(2, 3, 3, 5, 7, 10));
console.log(average(7, 1432, 12, 13, 100));
console.log(average());
```

<details>
  <summary><em>Solution</em></summary>

First attempt:

```javascript
function average(...nums) {
  let total = 0;
  for(const num of nums) {
    total += num;
    total / nums;
  }
  return total;
}

console.log(average(2, 6));
console.log(average(2, 3, 3, 5, 7, 10));
console.log(average(7, 1432, 12, 13, 100));
console.log(average());
```

Just printed the total:

```text
8
30
1564
0
```

I iterated several more times, but wasn't sure how to calculate or display the average:

```javascript
function average(...nums) {
  let total = 0;
  let avg = 0;
  for(const num of nums) {
    avg = (total += num) / nums;
  }
  return avg;
}

console.log(average(2, 6));
console.log(average(2, 3, 3, 5, 7, 10));
console.log(average(7, 1432, 12, 13, 100));
console.log(average());
```

```text
NaN
NaN
NaN
0
```

> What Went Well
>
> - Your code should have a function average()
> - Your average() function should have one parameter
> - Your average() function should use the rest parameter
>
> What Went Wrong
>
> - Your average() function doesn't calculate average correctly
>
> Feedback
>
> Not everything is correct yet, but you're close!

I checked [James Priest's work](https://github.com/james-priest/100-days-of-code-log-r2/blob/master/ES6-Syntax.md#solution-8) for help at this point. I was on the right track, but just needed a few modifications to the syntax:

```javascript
function average(...nums) {
  let total = 0;
  for (const num of nums) {
    total += num;
  }
  if (nums.length > 0) {
    return total / nums.length;
  }
  return 0;
}

console.log(average(2, 6));
console.log(average(2, 3, 3, 5, 7, 10));
console.log(average(7, 1432, 12, 13, 100));
console.log(average());
```

```text
4
5
312.8
0
```

> What Went Well
>
> - Your code should have a function `average()`
> - Your `average()` function should have one parameter
> - Your `average()` function should use the rest parameter
> - Your `average()` function should calculate the average of an indefinite amount of numbers
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 1.17. Lesson 1 Summary

## Feedback on JavaScript ES6 lesson 1/4

Very helpful! The documentation was great, and I understood everything well. Definitely glad I'm learning JavaScript after ES6 is available! So much better.

[Next lesson](es6-02-functions.md)

[(Back to top)](#top)