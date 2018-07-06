# JavaScript Built-Ins

<a href="https://www.udacity.com/">
  <img src="https://s3-us-west-1.amazonaws.com/udacity-content/rebrand/svg/logo.min.svg" width="300" alt="Udacity logo">
</a>

[ES6 - JavaScript Improved course](https://www.udacity.com/course/es6-javascript-improved--ud356) lesson 3/4

Udacity Google Mobile Web Specialist Nanodegree program part 3 lesson 06

Udacity Grow with Google Scholarship challenge course lesson 08

Brendon Smith

[br3ndonland](https://github.com/br3ndonland)

## Table of Contents <!-- omit in toc -->

- [Symbols](#symbols)
  - [3.01. New Built-ins](#301-new-built-ins)
  - [3.02. Symbols Intro](#302-symbols-intro)
  - [3.03. Symbols](#303-symbols)
  - [3.04. Iteration & Iterable Protocols](#304-iteration--iterable-protocols)
- [Sets](#sets)
  - [3.05. Sets](#305-sets)
  - [3.06. Modifying Sets](#306-modifying-sets)
  - [3.07. Working with Sets](#307-working-with-sets)
  - [3.08. Sets & Iterators](#308-sets--iterators)
  - [3.09. Quiz: Using Sets](#309-quiz-using-sets)
  - [3.10. WeakSets](#310-weaksets)
  - [3.11. Quiz: Working With WeakSets](#311-quiz-working-with-weaksets)
- [Maps](#maps)
  - [3.12. Maps](#312-maps)
  - [3.13. Creating & Modifying Maps](#313-creating--modifying-maps)
  - [3.14. Working with Maps](#314-working-with-maps)
  - [3.15. Looping Through Maps](#315-looping-through-maps)
  - [3.16. WeakMaps](#316-weakmaps)
- [Promises](#promises)
  - [3.17. Promises Intro](#317-promises-intro)
  - [3.18. Promises](#318-promises)
  - [3.19. More Promises](#319-more-promises)
- [Proxies](#proxies)
  - [3.20. Proxies Intro](#320-proxies-intro)
  - [3.21. Proxies](#321-proxies)
  - [3.22. Proxies vs. ES5 Getter/Setter](#322-proxies-vs-es5-gettersetter)
  - [3.23. Proxies Recap](#323-proxies-recap)
- [Generators](#generators)
  - [3.24. Generators](#324-generators)
  - [3.25. Generators & Iterators](#325-generators--iterators)
  - [3.26. Sending Data into/out of a Generator](#326-sending-data-intoout-of-a-generator)
  - [3.27. Lesson 3 Summary](#327-lesson-3-summary)
- [Feedback on JavaScript ES6 lesson 3/4](#feedback-on-javascript-es6-lesson-34)

## Symbols

### 3.01. New Built-ins

### 3.02. Symbols Intro

- Symbols are a new "primitive data type" for JavaScript. A symbol is used to uniquely identify properties within an object.
- Previous primitive data types were:
  - numbers
  - strings
  - booleans
  - null
  - undefined

### 3.03. Symbols

> A **symbol** is a unique and immutable data type that is often used to identify object properties.
>
> To create a symbol, you write `Symbol()` with an optional string as its **description**.
>
> ```javascript
> const sym1 = Symbol('apple');
> console.log(sym1);
> ```
>
> ```text
> Symbol(apple)
> ```
>
> This will create a unique symbol and store it in `sym1`. The description `"apple"` is just a way to describe the symbol, but it **can’t** be used to access the symbol itself.
>
> And just to show you how this works, if you compare two symbols with the same description…
>
> ```javascript
> const sym2 = Symbol('banana');
> const sym3 = Symbol('banana');
> console.log(sym2 === sym3);
> ```
>
> ```text
> false
> ```
>
> ...then the result is `false` because the description is _only_ used to describe the symbol. It’s not used as part of the symbol itself. Each time, a new symbol is created, regardless of the description.
>
> Still, this can be hard to wrap your head around, so let’s use the example from the previous section to see how symbols can be useful. Here’s the code to represent the bowl from the example.
>
> ```javascript
> const bowl = {
>   'apple': { color: 'red', weight: 136.078 },
>   'banana': { color: 'yellow', weight: 183.15 },
>   'orange': { color: 'orange', weight: 170.097 }
> };
> ```
>
> The bowl contains fruit which are objects that are properties of the bowl. But, we run into a problem when the second banana gets added.
>
> ```javascript
> const bowl = {
>   'apple': { color: 'red', weight: 136.078 },
>   'banana': { color: 'yellow', weight: 183.151 },
>   'orange': { color: 'orange', weight: 170.097 },
>   'banana': { color: 'yellow', weight: 176.845 }
> };
> console.log(bowl);
> ```
>
> ```text
> Object {apple: Object, banana: Object, orange: Object}
> ```
>
> Instead of adding another banana to the bowl, our previous banana is overwritten by the new banana being added to the bowl. To fix this problem, we can use symbols.
>
> ```javascript
> const bowl = {
>   [Symbol('apple')]: { color: 'red', weight: 136.078 },
>   [Symbol('banana')]: { color: 'yellow', weight: 183.15 },
>   [Symbol('orange')]: { color: 'orange', weight: 170.097 },
>   [Symbol('banana')]: { color: 'yellow', weight: 176.845 }
> };
> console.log(bowl);
> ```
>
> ```text
> Object {Symbol(apple): Object, Symbol(banana): Object, Symbol(orange): Object, Symbol(banana): Object}
> ```
>
> By changing the bowl’s properties to use symbols, each property is a unique Symbol and the first banana doesn’t get overwritten by the second banana.

### 3.04. Iteration & Iterable Protocols

> Before you move on, let’s spend some time looking at two new protocols in ES6:
>
> - the iterable protocol
> - the iterator protocol
>
> These protocols aren’t built-ins, but they will help you understand the new concept of iteration in ES6, as well as show you a use case for symbols.

#### The Iterable Protocol

> The **iterable protocol** is used for defining and customizing the iteration behavior of objects. What that really means is you now have the _flexibility_ in ES6 to specify a way for iterating through values in an object. For some objects, they already come built-in with this behavior. For example, strings and arrays are examples of built-in iterables.
>
> ```javascript
> const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
> for (const digit of digits) {
>   console.log(digit);
> }
> ```
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
> **If you recall from earlier lesson 1, any object that is iterable can use the new `for..of` loop.** Later in this lesson, you’ll also learn about Sets and Maps which are other examples of built-in iterables.

##### How the iterable protocol works

> In order for an object to be iterable, it must implement the **iterable interface**. If you come from a language like Java or C, then you’re probably familiar with interfaces, but for those of you who aren’t, that basically means that in order for an object to be iterable it must contain a default iterator method. This method will define how the object should be iterated.
>
> The **iterator method**, which is available via the constant `[Symbol.iterator]`, is a zero arguments function that returns an iterator object. An iterator object is an object that conforms to the iterator protocol.

#### The Iterator Protocol

> The **iterator protocol** is used to define a standard way that an object produces a sequence of values. What that really means is you now have a process for defining how an object will iterate. This is done through implementing the `.next()` method.

##### How the iterator protocol works

> An object becomes an iterator when it implements the `.next()` method. The `.next()` method is a zero arguments function that returns an object with two properties:
>
> 1. `value`: the data representing the next value in the sequence of values within the object
> 2. `done`: a boolean representing if the iterator is done going through the sequence of values
>     - If done is true, then the iterator has reached the end of its sequence of values.
>     - If done is false, then the iterator is able to produce another value in its sequence of values.
>
> Here’s the example from earlier, but instead we are using the array’s default iterator to step through each value in the array.
>
> ```javascript
> const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
> const arrayIterator = digits[Symbol.iterator]();
>
> console.log(arrayIterator.next());
> console.log(arrayIterator.next());
> console.log(arrayIterator.next());
> ```
>
> ```text
> Object {value: 0, done: false}
> Object {value: 1, done: false}
> Object {value: 2, done: false}
> ```

## Sets

### 3.05. Sets

#### A Set in Mathematics

> If you think back to mathematics, a set is a collection of distinct items. For example, `{2, 4, 5, 6}` is a set because each number is unique and appears only once. However, `{1, 1, 2, 4}` is not a set because it _contains duplicate entries_ (the 1 is in there more than once!).
>
> In JavaScript, we can already represent something similar to a mathematical set using an array.
>
> ```javascript
> const nums = [2, 4, 5, 6];
> ```
>
> However, arrays _do no enforce items to be unique_. If we try to add another `2` to `nums`, JavaScript won't complain and will add it without any issue.
>
> ```javascript
> nums.push(2);
> console.log(nums);
> ```
>
> ```text
> [2, 4, 5, 6, 2]
> ```
>
> …and now `nums` is no longer a set in the mathematical sense.

#### Sets in JS

> In ES6, there’s a new built-in object that behaves like a mathematical set and works similarly to an array. This new object is conveniently called a "Set". The biggest differences between a set and an array are:
>
> - Sets are **not indexed-based** - you do not refer to items in a set based on their position in the set
> - items in a Set **can’t be accessed individually**
>
> **Basically, a Set is an object that lets you store unique items.** You can add items to a Set, remove items from a Set, and loop over a Set. These items can be either primitive values or objects.

#### How to Create a Set

> There’s a couple of different ways to create a Set. The first way, is pretty straightforward:
>
> ```javascript
> const games = new Set();
> console.log(games);
> ```
>
> ```text
> Set {}
> ```
>
> This creates an empty Set `games` with no items.
>
> If you want to create a Set from a list of values, you use an array:
>
> ```javascript
> const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
> console.log(games);
> ```
>
> ```text
> Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'}
> ```
>
> Notice the example above automatically removes the duplicate entry `"Super Mario Bros."` when the Set is created. Pretty neat!

#### 3.05 Mini-Quiz Question

Select the collections below that represent a Set in JavaScript.

- `{1, 'Basketball', true, false, '1'}`
- `{}`
- `{1, 1, 1, 1}`
- `{false, '0', 0, 'Soccer', 3.14, 25, 0}`
- `{'Gymnastics', 'Swimming', 2}`

<details>
  <summary><em>Solution</em></summary>

First try. Sets make a lot of sense. Thank you ES6!

- `{1, 'Basketball', true, false, '1'}`
- `{}`
- `{'Gymnastics', 'Swimming', 2}`

> Nice work! The choices you've selected represent sets since all their items are unique.

</details>

### 3.06. Modifying Sets

> After you’ve created a Set, you’ll probably want to add and delete items from the Set. So how do you that? You use the appropriately named, `.add()` and `.delete()` methods:
>
> ```javascript
>
> const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
>
> games.add('Banjo-Tooie');
> games.add('Age of Empires');
> games.delete('Super Mario Bros.');
>
> console.log(games);
> ```
>
> ```text
> Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Age of Empires'}
> ```
>
> On the other hand, if you want to delete all the items from a Set, you can use the `.clear()` method.
>
> ```javascript
> games.clear()
> console.log(games);
> ```
>
> ```text
> Set {}
> ```
>
> **TIP:** If you attempt to `.add()` a duplicate item to a Set, you won’t receive an error, but the item will not be added to the Set. Also, if you try to `.delete() an item that is not in a Set, you won’t receive an error, and the Set will remain unchanged.
>
>`.add()` returns the `Set` if an item is successfully added. On the other hand, `.delete()` returns a Boolean (`true` or `false`) depending on successful deletion.

### 3.07. Working with Sets

#### Checking The Length

> Once you’ve constructed your Set, there are a couple of different properties and methods you can use to work with Sets.
>
> Use the `.size` property to return the number of items in a Set:
>
> ```javascript
> const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']);
> console.log(months.size);
> ```
>
> ```text
> 12
> ```
>
> Remember, Sets can’t be accessed by their index like an array, so you use the `.size` property instead of `.length` property to get the size of the Set.

#### Checking If An Item Exists

> Use the `.has()` method to check if an item exists in a Set. If the item is in the Set, then `.has()` will return `true`. If the item doesn’t exist in the Set, then `.has()` will return `false`.
>
> ```javascript
> console.log(months.has('September'));
> ```
>
> ```text
> true
> ```

#### Retrieving All Values

> Finally, use the `.values()` method to return the values in a Set. The return value of the `.values()` method is a `SetIterator` object.
>
> ```javascript
> console.log(months.values());
> ```
>
> ```text
> SetIterator {'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'}
> ```
>
> More on the `SetIterator` object in a second!
>
> **TIP:** The `.keys()` method will behave the exact same way as the `.values()` method by returning the values of a Set within a new Iterator Object. The `.keys()` method is an alias for the .values() method for similarity with maps. You’ll see the `.keys()` method later in this lesson during the Maps section.

### 3.08. Sets & Iterators

#### Intro

> The last step to working with Sets is looping over them.
>
> If you remember back to our discussion on the new *iterable and iterator protocols* in ES6, then you’ll recall that Sets are built-in iterables. This means two things in terms of looping:
>
> 1. You can use the Set’s default iterator to step through each item in a Set, one by one.
> 2. You can use the new `for...of` loop to loop through each item in a Set.

#### Using the SetIterator

> Because the `.values()` method returns a new iterator object (called `SetIterator`), you can store that iterator object in a variable and loop through each item in the Set using `.next()`.
>
> ```javascript
> const iterator = months.values();
> iterator.next();
> ```
>
> ```text
> Object {value: 'January', done: false}
> ```
>
> And if you run `.next()` again?
>
> ```javascript
> iterator.next();
> ```
>
> ```text
> Object {value: 'February', done: false}
> ```
>
> And so on until `done` equals `true` which marks the end of the Set.
>
>
> ```javascript
> const days = new Set(['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']);
> const iterator = days.values();
>
> iterator.next();  // {value: 'Mon', done: false}
> iterator.next();  // {value: 'Tue', done: false}
> iterator.next();  // {value: 'Wed', done: false}
> iterator.next();  // {value: 'Thu', done: false}
> iterator.next();  // {value: 'Fri', done: false}
> iterator.next();  // {value: 'Sat', done: false}
> iterator.next();  // {value: 'Mon', done: false}
> iterator.next();  // {value: undefined, done: true}
> ```

#### Using a for...of Loop

> An easier method to loop through the items in a Set is the for...of loop.
>
> ```javascript
> const colors = new Set(['red', 'orange', 'yellow', 'green', 'blue', 'violet', 'brown', 'black']);
> for (const color of colors) {
>   console.log(color);
> }
> ```
>
> ```text
> red
> orange
> yellow
> green
> blue
> violet
> brown
> black
> ```

### 3.09. Quiz: Using Sets

Quiz

Create a variable with the name `myFavoriteFlavors` and give it the value of an empty `Set` object. Then use the `.add()` method to add the following strings to it:

- "chocolate chip"
- "cookies and cream"
- "strawberry"
- "vanilla"

Then use the `.delete()` method to remove "strawberry" from the set.

```javascript
/*
 - Programming Quiz: Using Sets (3-1)
 *
 - Create a Set object and store it in a variable named `myFavoriteFlavors`. Add the following strings to the set:
 -     - chocolate chip
 -     - cookies and cream
 -     - strawberry
 -     - vanilla
 *
 - Then use the `.delete()` method to remove "strawberry" from the set.
 */
```

<details>
  <summary><em>Solution</em></summary>

```js
/*
 - Programming Quiz: Using Sets (3-1)
 *
 - Create a Set object and store it in a variable named `myFavoriteFlavors`.
 - Add the following strings to the set:
 -     - chocolate chip
 -     - cookies and cream
 -     - strawberry
 -     - vanilla
 *
 - Then use the `.delete()` method to remove "strawberry" from the set.
 */
const myFavoriteFlavors = new Set();

myFavoriteFlavors.add('chocolate chip');
myFavoriteFlavors.add('cookies and cream');
myFavoriteFlavors.add('strawberry');
myFavoriteFlavors.add('vanilla');

myFavoriteFlavors.delete('strawberry');

console.log(myFavoriteFlavors);
```

```text
Set { 'chocolate chip', 'cookies and cream', 'vanilla' }
```

> What Went Well
>
> - Your code should have a variable myFavoriteFlavors
> - Your code should use the .add() method to add required items to the set
> - Your code should use the .delete() method to remove "strawberry"
> - Your code should use the .delete() method only once
> - The myFavoriteFlavors object should contain "chocolate chip"
> - The myFavoriteFlavors object should contain "cookies and cream"
> - The myFavoriteFlavors object should contain "vanilla"
> - The myFavoriteFlavors object should not contain "strawberry"
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

### 3.10. WeakSets

#### What is a WeakSet

> A WeakSet is just like a normal Set with a few key differences:
>
> 1. a WeakSet can only contain objects
> 2. a WeakSet is not iterable which means it can’t be looped over
> 3. a WeakSet does not have a `.clear()` method
>
> You can create a WeakSet just like you would a normal Set, except that you use the `WeakSet` constructor.
>
> ```js
> const student1 = { name: 'James', age: 26, gender: 'male' };
> const student2 = { name: 'Julia', age: 27, gender: 'female' };
> const student3 = { name: 'Richard', age: 31, gender: 'male' };
>
> const roster = new WeakSet([student1, student2, student3]);
> console.log(roster);
> ```
>
> ```text
> WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'Richard', age: 31, gender: 'male'}, Object {name: 'James', age: 26, gender: 'male'}}
> ```
>
> …but if you try to add something other than an object, you’ll get an error!
>
> ```js
> roster.add('Amanda');
> ```
>
> ```text
> Uncaught TypeError: Invalid value used in weak set(…)
> ```
>
> This is expected behavior because WeakSets can only contain objects. But why should it only contain objects? **Why would you even use a WeakSet** if normal Sets can contain objects and other types of data? Well, the answer to that question has more to do with why WeakSets do not have a `.clear()` method...

#### Garbage Collection

> In JavaScript, memory is allocated when new values are created and is "automatically" freed up when those values are no longer needed. This process of freeing up memory after it is no longer needed is what is known as **garbage collection**.
>
> WeakSets take advantage of this by exclusively working with objects. If you set an object to `null`, then you’re essentially deleting the object. And when JavaScript’s garbage collector runs, the memory that object previously occupied will be freed up to be used later in your program.
>
> ```js
> let studentA = { name: 'Richard', age: 31 };
> let studentB = { name: 'Alexis', age: 28 };
> let studentC = { name: 'Jasmine', age: 29 };
>
> let roster = new WeakSet([studentA, studentB, studentC]);
>
> studentC = null;
> console.log(roster);
> ```
>
> ```text
> WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'James', age: 26, gender: 'male'}}
> ```
>
> What makes this so useful is you don’t have to worry about deleting references to deleted objects in your WeakSets, JavaScript does it for you! When an object is deleted, the object will also be deleted from the WeakSet when garbage collection runs.
>
> **This makes WeakSets useful in situations where you want an efficient, lightweight solution for creating groups of objects.**
>
> The point in time when garbage collection happens depends on a lot of different factors. Check out [MDN’s documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#Garbage_collection) to learn more about the algorithms used to handle garbage collection in JavaScript.

### 3.11. Quiz: Working With WeakSets

Quiz

Create the following variables:

- `uniqueFlavors` and give it the value of an empty `WeakSet` object
- `flavor1`, and set it to the object `{ flavor: 'chocolate' }`
- `flavor2`, and set it to an object with a property of `flavor` and a value of your choice

Use the `.add()` method to add the objects `flavor1` and `flavor2` to `uniqueFlavors`.

Use the `.add()` method to add the `flavor1` object to the `uniqueFlavors` set, again.

```js
/*
 - Programming Quiz: Using Sets (3-2)
 *
 - Create the following variables:
 -     - uniqueFlavors and set it to a new WeakSet object
 -     - flavor1 and set it equal to `{ flavor: 'chocolate' }`
 -     - flavor2 and set it equal to an object with property 'flavor'
 -       and value of your choice!
 *
 - Use the `.add()` method to add the objects `flavor1` and `flavor2`
 -    to `uniqueFlavors`
 - Use the `.add()` method to add the `flavor1` object (again!) to
 -    the `uniqueFlavors` set
 */
```

<details>
  <summary><em>Solution</em></summary>

```js
let uniqueFlavors = new WeakSet();
let flavor1 = { flavor: 'chocolate' }
let flavor2 = { flavor: 'peanut butter' }

uniqueFlavors.add(flavor1);
uniqueFlavors.add(flavor2);
uniqueFlavors.add(flavor1);

console.log(uniqueFlavors)
```

> What Went Well
>
> - Your code should have a variable uniqueFlavors
> - Your code should have a variable flavor1
> - Your code should have a variable flavor2
> - Your code should use the .add() method three times to add required items to the set
> - The uniqueFlavors object should contain a "chocolate" flavor object
> - The uniqueFlavors object should contain a custom flavor object
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

## Maps

### 3.12. Maps

> - Maps and Sets are both **iterable** which means you can loop over them
> - WeakMaps and WeakSets **don't prevent objects from being garbage collected**.
> - **Maps are collections of key-value pairs**,
>
>   ```js
>   {
>     key1: value1
>     richard: 'is awesome'
>     james: 'is also cool'
>   }
>   ```
>
> - whereas Sets are **collections of unique values**.
>
>   ```js
>   [val1, val2, val3]
>   ```
>
> - You could say that Sets are to arrays as maps are to objects.
>
>   ```text
>   Sets :: Arrays
>   Maps :: Objects
>   ```
>

### 3.13. Creating & Modifying Maps

#### Maps intro

> If Sets are similar to Arrays, then Maps are similar to Objects because Maps store key-value pairs similar to how objects contain named properties with values.
>
> Essentially, a Map is an object that lets you store key-value pairs where both the keys and the values can be objects, primitive values, or a combination of the two.

#### How to Create a Map

> To create a Map, simply type:
>
> ```js
> const employees = new Map();
> console.log(employees);
> ```
>
> ```text
> Map {}
> ```
>
> This creates an empty Map `employee` with no key-value pairs.

#### Modifying Maps

> Unlike Sets, you can’t create Maps from a list of values; instead, you add key-values by using the Map’s `.set()` method.
>
> ```js
> const employees = new Map();
>
> employees.set('james.parkes@udacity.com', {
>     firstName: 'James',
>     lastName: 'Parkes',
>     role: 'Content Developer'
> });
> employees.set('julia@udacity.com', {
>     firstName: 'Julia',
>     lastName: 'Van Cleve',
>     role: 'Content Developer'
> });
> employees.set('richard@udacity.com', {
>     firstName: 'Richard',
>     lastName: 'Kalehoff',
>     role: 'Content Developer'
> });
>
> console.log(employees);
> ```
>
> ```text
> Map {'james.parkes@udacity.com' => Object {...}, 'julia@udacity.com' => Object {...}, 'richard@udacity.com' => Object {...}}
> ```
>
> The `.set()` method takes two arguments. The first argument is the key, which is used to reference the second argument, the value.
>
> To remove key-value pairs, simply use the `.delete()` method.
>
> ```js
> employees.delete('julia@udacity.com');
> employees.delete('richard@udacity.com');
> console.log(employees);
> ```
>
> ```text
> Map {'james.parkes@udacity.com' => Object {firstName: 'James', lastName: 'Parkes', role: 'Course Developer'}}
> ```
>
> Again, similar to Sets, you can use the `.clear()` method to remove all key-value pairs from the Map.
>
> ```js
> employees.clear()
> console.log(employees);
> ```
>
> ```text
> Map {}
> ```
>
> **TIP:** If you `.set()` a key-value pair to a Map that already uses the same key, you won’t receive an error, but the key-value pair will overwrite what currently exists in the Map. Also, if you try to `.delete()` a key-value that is not in a Map, you won’t receive an error, and the Map will remain unchanged.
>
> The `.delete()` method returns `true` if a key-value pair is successfully deleted from the `Map` object, and `false` if unsuccessful. The return value of `.set()` is the `Map` object itself if successful.

### 3.14. Working with Maps

> After you’ve built your Map, you can use the `.has()` method to check if a key-value pair exists in your Map by passing it a key.
>
> ```js
> const members = new Map();
>
> members.set('Evelyn', 75.68);
> members.set('Liam', 20.16);
> members.set('Sophia', 0);
> members.set('Marcus', 10.25);
>
> console.log(members.has('Xavier'));
> console.log(members.has('Marcus'));
> ```
>
> ```text
> false
> true
> ```
>
> And you can also retrieve values from a Map, by passing a key to the `.get()` method.
>
> ```js
> console.log(members.get('Evelyn'));
> ```
>
> ```text
> 75.68
> ```

### 3.15. Looping Through Maps

#### Intro to looping through maps

> You’ve created a Map, added some key-value pairs, and now you want to loop through your Map. Thankfully, you’ve got three different options to choose from:
>
> 1. Step through each key or value using the Map’s default iterator
> 2. Loop through each key-value pair using the new `for..of` loop
> 3. Loop through each key-value pair using the Map’s `.forEach()` method

#### 1. Using the MapIterator

> Using both the `.keys()` and `.values()` methods on a Map will return a new iterator object called MapIterator. You can store that iterator object in a new variable and use `.next()` to loop through each key or value. Depending on which method you use, will determine if your iterator has access to the Map’s keys or the Map’s values.
>
> ```js
> let iteratorObjForKeys = members.keys();
> iteratorObjForKeys.next();
> ```
>
> ```text
> Object {value: 'Evelyn', done: false}
> ```
>
> Use `.next()` to the get the next key value.
>
> ```js
> iteratorObjForKeys.next();
> ```
>
> ```text
> Object {value: 'Liam', done: false}
> ```
>
> And so on.
>
> ```js
> iteratorObjForKeys.next();
> ```
>
> ```text
> Object {value: 'Sophia', done: false}
> ```
>
> On the flipside, use the `.values()` method to access the Map’s values, and then repeat the same process.
>
> ```js
> let iteratorObjForValues = members.values();
> iteratorObjForValues.next();
> ```
>
> ```text
> Object {value: 75.68, done: false}
> ```

#### 2. Using a for...of Loop

> Your second option for looping through a Map is with a `for..of` loop.
>
> ```js
> for (const member of members) {
>   console.log(member);
> }
> ```
>
> ```text
> ['Evelyn', 75.68]
> ['Liam', 20.16]
> ['Sophia', 0]
> ['Marcus', 10.25]
> ```
>
> However, when you use a `for..of` loop with a Map, you don’t exactly get back a key or a value. Instead, the key-value pair is split up into an array where the first element is the key and the second element is the value. If only there were a way to fix this?

#### 3.15 Mini-Quiz Question

```js
/*
 - Using array destructuring, fix the following code to print the
 - keys and values of the `members` Map to the console.
 */

const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

for (const member of members) {
    // console.log(key, value);
}
```

<details>
  <summary><em>Solution</em></summary>

```js
/*
 - Using array destructuring, fix the following code to print the
 - keys and values of the `members` Map to the console.
 */

const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

for (const member of members) {
    const [key, value] = member;
    console.log(key, value);
}
```

```text
['Evelyn', 75.68]
['Liam', 20.16]
['Sophia', 0]
['Marcus', 10.25]
```

> What Went Well
>
> - Your code should have a members variable
> - Your code should use destructuring
> - members should be a Map
>
> Feedback
>
> Your answer passed all our tests! Awesome job!

</details>

#### 3. Using a forEach Loop

> Your last option for looping through a Map is with the `.forEach()` method.
>
> ```js
> members.forEach((key, value) => console.log(key, value));
> ```
>
> ```text
> ['Evelyn', 75.68]
> ['Liam', 20.16]
> ['Sophia', 0]
> ['Marcus', 10.25]
> ```
>
> Notice how with the help of an arrow function, the `forEach` loop reads fairly straightforward. For each `value` and `key` in `members`, log the `value` and `key` to the console.

### 3.16. WeakMaps

> **TIP:** If you’ve gone through the WeakSets section, then this section should be somewhat of a review. WeakMaps exhibit the same behavior as a WeakSets, except WeakMaps work with key-values pairs instead of individual items.

#### What is a WeakMap

> A WeakMap is just like a normal Map with a few key differences:
>
> 1. a WeakMap can only contain objects as keys,
> 2. a WeakMap is not iterable which means it can’t be looped and
> 3. a WeakMap does not have a `.clear()` method.
>
> You can create a WeakMap just like you would a normal Map, except that you use the `WeakMap` constructor.
>
> ```js
> let book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
> let book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
> let book3 = { title: 'Gulliver’s Travels', author: 'Jonathan Swift' };
>
> const library = new WeakMap();
> library.set(book1, true);
> library.set(book2, false);
> library.set(book3, true);
>
> console.log(library);
> ```
>
> ```text
> WeakMap {Object {title: 'Pride and Prejudice', author: 'Jane Austen'} => true, Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}
> ```
>
> ...but if you try to add something other than an object as a key, you’ll get an error!
>
> ```js
> library.set('The Grapes of Wrath', false);
> ```
>
> ```text
> Uncaught TypeError: Invalid value used as weak map key(…)
> ```
>
> This is expected behavior because **WeakMap can only contain objects as keys**. Again, similar to WeakSets, WeakMaps leverage garbage collection for easier use and maintainability.

#### WeakMaps and Garbage Collection

> In JavaScript, memory is allocated when new values are created and is "automatically" freed up when those values are no longer needed. This process of freeing up memory after it is no longer needed is what is known as garbage collection.
>
> WeakMaps take advantage of this by exclusively working with objects as keys. If you set an object to null, then you’re essentially deleting the object. And when JavaScript’s garbage collector runs, the memory that object previously occupied will be freed up to be used later in your program.
>
> ```js
> book1 = null;
> console.log(library);
> ```
>
> ```text
> WeakMap {Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}
> ```
>
> What makes this so useful is **you don’t have to worry about deleting keys that are referencing deleted objects in your WeakMaps, JavaScript does it for you!** When an object is deleted, the object key will also be deleted from the WeakMap when garbage collection runs.
>
> **This makes WeakMaps useful in situations where you want an efficient, lightweight solution for creating groupings of objects with metadata.**
>
> The point in time when garbage collection happens is dependent on a lot of different factors. Check out [MDN’s documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#Garbage_collection) to learn more about the algorithms used to handle garbage collection in JavaScript.

## Promises

### 3.17. Promises Intro

**Promises are used to handle asynchronous requests.** It's like an IOU for a task. The computer will work on it and get back to you with the response.

> Do this thing now, then notify me when it's done so I can pick up where I left off.

### 3.18. Promises

#### Intro to promises

> A JavaScript Promise is created with the new [Promise constructor function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) - `new Promise()`. A promise will let you start some work that will be done **asynchronously** and let you get back to your regular work.
>
> When you create the promise, you must give it the code that will be run asynchronously. You provide this code as the argument of the constructor function:
>
> ```js
> new Promise(function () {
>     window.setTimeout(function createSundae(flavor = 'chocolate') {
>         const sundae = {};
>         // request ice cream
>         // get cone
>         // warm up ice cream scoop
>         // scoop generous portion into cone!
>     }, Math.random() - 2000);
> });
> ```
>
> This code creates a promise that will start in a few seconds after I make the request. Then there are a number of steps that need to be made in the `createSundae` function.

#### Indicated a Successful Request or a Failed Request

> But once that's all done, how does JavaScript notify us that it's finished and ready for us to pick back up? It does that by passing two functions into our initial function. Typically we call these `resolve` and `reject`.
>
> The function gets passed to the function we provide the Promise constructor - typically the word "resolve" is used to indicate that this function should be called when the request completes successfully. Notice the `resolve` on the first line:
>
> ```js
> new Promise(function (resolve, reject) {
>     window.setTimeout(function createSundae(flavor = 'chocolate') {
>         const sundae = {};
>         // request ice cream
>         // get cone
>         // warm up ice cream scoop
>         // scoop generous portion into cone!
>         resolve(sundae);
>     }, Math.random() - 2000);
> });
> ```
>
> Now when the sundae has been successfully created, it calls the `resolve` method and passes it the data we want to return - in this case the data that's being returned is the completed sundae. So the `resolve` method is used to indicate that the request is complete and that it completed _successfully_.
>
> If there is a problem with the request and it couldn't be completed, then we could use the second function that's passed to the function. Typically, this function is stored in an identifier called "reject" to indicate that this function should be used if the request fails for some reason. Check out the `reject` on the first line:
>
> ```js
> new Promise(function (resolve, reject) {
>     window.setTimeout(function createSundae(flavor = 'chocolate') {
>         const sundae = {};
>         // request ice cream
>         // get cone
>         // warm up ice cream scoop
>         // scoop generous portion into cone!
>         if ( /- iceCreamConeIsEmpty(flavor) */ ) {
>             reject(`Sorry, we're out of that flavor :-(`);
>         }
>         resolve(sundae);
>     }, Math.random() - 2000);
> });
> ```
>
> So the `reject` method is used when the request _could not be completed_. Notice that even though the request fails, we can still return data - in this case we're just returning text that says we don't have the desired ice cream flavor.
>
> A Promise constructor takes a function that will run and then, after some amount of time, will either complete successfully (using the `resolve` method) or unsuccessfully (using the `reject` method). When the outcome has been finalized (the request has either completed successfully or unsuccessfully), the promise is now _fulfilled_ and will notify us so we can decide what to do with the response.

#### Promises Return Immediately

> The first thing to understand is that a Promise will immediately return an object.
>
> ```js
> const myPromiseObj = new Promise(function (resolve, reject) {
>     // sundae creation code
> });
> ```
>
> That object has a `.then()` method on it that we can use to have it notify us if the request we made in the promise was either successful or failed. The `.then()` method takes two functions:
>
> 1. the function to run if the request completed successfully
> 2. the function to run if the request failed to complete
>
> ```js
> mySundae.then(function(sundae) {
>     console.log(`Time to eat my delicious ${sundae}`);
> }, function(msg) {
>     console.log(msg);
>     self.goCry(); // not a real method
> });
> ```
>
> As you can see, the first function that's passed to `.then()` will be called and passed the data that the Promise's `resolve` function used. In this case, the function would receive the `sundae` object. The second function will be called and passed the data that the Promise's `reject` function was called with. In this case, the function receives the error message "Sorry, we're out of that flavor :-(" that the `reject` function was called with in the Promise code above.

### 3.19. More Promises

> Promises are an incredibly powerful addition to the language. A ton of both existing and future changes make use of them. So being able to work with and write JavaScript Promises is vital.
>
> The reason is that Promises make it so much easier to do asynchronous code. With promises your code is gonna be easier to read, easier to write, and most importantly, it's going to be a lot easier to debug.
>
> They're so important Udacity has actually created a standalone course dedicated just to JavaScript Promises.
>
> Check out our [Promises course](https://www.udacity.com/course/javascript-promises--ud898) where we'll take a deep dive into:
>
> - JavaScript Promises
> - how to handle returned data and errors
> - build an app called Exoplanet Explorer that uses JavaScript Promises to fetch remote data asynchronously

## Proxies

### 3.20. Proxies Intro

Proxies are objects that stand in for other objects and handle all their interactions.

### 3.21. Proxies

#### Intro to proxies

> To create a proxy object, we use the Proxy constructor - `new Proxy();`. The proxy constructor takes two items:
>
> - the object that it will be the proxy for
> - an object containing the list of methods it will handle for the proxied object
>
> The second object is called the **handler**.

#### A Pass Through Proxy

> The simplest way to create a proxy is to provide an object and then an empty handler object.
>
> ```js
> var richard = {status: 'looking for work'};
> var agent = new Proxy(richard, {});
>
> agent.status; // returns 'looking for work'
> ```
>
> The above doesn't actually do anything special with the proxy - it just passes the request directly to the source object! If we want the proxy object to actually intercept the request, that's what the handler object is for!
>
> The key to making Proxies useful is the handler object that's passed as the second object to the Proxy constructor. The handler object is made up of a methods that will be used for property access. Let's look at the `get`:

#### Get Trap

> The `get` trap is used to "intercept" calls to properties:
>
> ```js
> const richard = {status: 'looking for work'};
> const handler = {
>     get(target, propName) {
>         console.log(target); // the `richard` object, not `handler`, not `agent`
>         console.log(propName); // the name of the property the proxy is checking
>                                // (`agent` in this case)
>     }
> };
> const agent = new Proxy(richard, handler);
> agent.status; // logs out the richard object (not the agent object!)
>               // and logs out the name of the property being accessed (`status`)
> ```
>
> In the code above, the `handler` object has a `get` method (called a "trap" since it's being used in a Proxy). When the code `agent.status;` is run on the last line, because the `get` trap exists, it "intercepts" the call to get the status property and runs the `get` trap function.
>
> This will log out the target object of the proxy (the `richard` object) and then logs out the name of the property being requested (the `status` property). _And that's all it does!_ It doesn't actually log out the property!
>
> This is important - _if a trap is used, you need to make sure you provide all the functionality for that specific trap._

#### Accessing the Target object from inside the proxy

> If we wanted to actually provide the real result, we would need to return the property on the target object:
>
> ```js
> const richard = {status: 'looking for work'};
> const handler = {
>     get(target, propName) {
>         console.log(target);
>         console.log(propName);
>         return target[propName];
>     }
> };
> const agent = new Proxy(richard, handler);
> agent.status; // (1)logs the richard object, (2)logs the property being accessed,
>               // (3)returns the text in richard.status
> ```
>
> Notice we added the `return target[propName];` as the last line of the `get` trap. This will access the property on the target object and will return it.

#### Having the proxy return info, directly

> Alternatively, we could use the proxy to provide direct feedback:
>
> ```js
> const richard = {status: 'looking for work'};
> const handler = {
>     get(target, propName) {
>         return `He's following many leads, so you should offer a contract ASAP!`;
>     }
> };
> const agent = new Proxy(richard, handler);
> agent.status; // returns the text `He's following many leads, so you should ...`
> ```
>
> With this code, the Proxy doesn't even check the target object, it just directly responds to the calling code.
>
> So the `get` trap will take over whenever any property on the proxy is accessed. If we want to intercept calls to change properties, then the `set` trap needs to be used!
>
> The `set` trap is used for intercepting code that will _change a property_. The `set` trap receives: the object it proxies the property that is being set the new value for the proxy.
>
> ```js
> const richard = {status: 'looking for work'};
> const handler = {
>     set(target, propName, value) {
>         // if the pay is being set, take 15% as commission
>         if (propName === 'payRate') {
>             value = value - 0.85;
>         }
>         target[propName] = value;
>     }
> };
> const agent = new Proxy(richard, handler);
> agent.payRate = 1000; // set the actor's pay to $1,000
> agent.payRate; // $850 the actor's actual pay
> ```
>
> In the code above, notice that the `set` trap checks to see if the `payRate` property is being set. If it is, then the proxy (the agent) takes 15 percent off the top for her own commission! Then, when the actor's pay is set to one thousand dollars, since the `payRate` property was used, the code took 15% off the top and set the actual `payRate` property to `850`;

#### Other Traps

> So we've looked at the `get` and `set` traps (which are probably the ones you'll use most often), but there are actually a total of 13 different traps that can be used in a handler!
>
> 1. [the get trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/get) - lets the proxy handle calls to property access
> 2. [the set trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/set) - lets the proxy handle setting the property to a new value
> 3. [the apply trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/apply) - lets the proxy handle being invoked (the object being proxied is a function)
> 4. [the has trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/has) - lets the proxy handle the using `in` operator
> 5. [the deleteProperty trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/deleteProperty) - lets the proxy handle if a property is deleted
> 6. [the ownKeys trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/ownKeys) - lets the proxy handle when all keys are requested
> 7. [the construct trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/construct) - lets the proxy handle when the proxy is used with the `new` keyword as a constructor
> 8. [the defineProperty trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/defineProperty) - lets the proxy handle when defineProperty is used to create a new property on the object
> 9. [the getOwnPropertyDescriptor trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/getOwnPropertyDescriptor) - lets the proxy handle getting the property's descriptors
> 10. [the preventExtenions trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/preventExtensions) - lets the proxy handle calls to `Object.preventExtensions()` on the proxy object
> 11. [the isExtensible trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/isExtensible) - lets the proxy handle calls to `Object.isExtensible` on the proxy object
> 12. [the getPrototypeOf trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/getPrototypeOf) - lets the proxy handle calls to `Object.getPrototypeOf` on the proxy object
> 13. [the setPrototypeOf trap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/setPrototypeOf) - lets the proxy handle calls to `Object.setPrototypeOf` on the proxy object
>
> As you can see, there are a lot of traps that let the proxy manage how it handles calls back and forth to the proxied object.

### 3.22. Proxies vs. ES5 Getter/Setter

> Initially, it can be a bit unclear as to why proxies are all that beneficial when there are already getter and setter methods provided in ES5. With ES5's getter and setter methods, you need to know _beforehand_ the properties that are going to be get/set:
>
> ```js
> var obj = {
>     _age: 5,
>     _height: 4,
>     get age() {
>         console.log(`getting the "age" property`);
>         console.log(this._age);
>     },
>     get height() {
>         console.log(`getting the "height" property`);
>         console.log(this._height);
>     }
> };
> ```
>
> With the code above, notice that we have to set `get age()` and `get height()` when initializing the object. So when we call the code below, we'll get the following results:
>
> ```js
> obj.age; // logs 'getting the "age" property' & 5
> obj.height; // logs 'getting the "height" property' & 4
> ```
>
> But look what happens when we now add a new property to the object:
>
> ```js
> obj.weight = 120; // set a new property on the object
> obj.weight; // logs just 120
> ```
>
> Notice that a `getting the "weight" property` message wasn't displayed like the `age` and `height` properties produced.
>
> With ES6 Proxies, we _do not need to know the properties beforehand_:
>
> ```js
> const proxyObj = new Proxy({age: 5, height: 4}, {
>     get(targetObj, property) {
>         console.log(`getting the ${property} property`);
>         console.log(targetObj[property]);
>     }
> });
>
> proxyObj.age; // logs 'getting the age property' & 5
> proxyObj.height; // logs 'getting the height property' & 4
> ```
>
> All well and good, just like the ES5 code, but look what happens when we add a new property:
>
> ```js
> proxyObj.weight = 120; // set a new property on the object
> proxyObj.weight; // logs 'getting the weight property' & 120
> ```
>
> See that?!? A `weight` property was added to the proxy object, and when it was later retrieved, it displayed a log message!
>
> So some functionality of proxy objects may seem similar to existing ES5 getter/setter methods. But with proxies, you do not need to initialize the object with getters/setters for each property when the object is initialized.

### 3.23. Proxies Recap

> A proxy object sits between a real object and the calling code. The calling code interacts with the proxy instead of the real object. To create a proxy:
>
> - use the `new Proxy()` constructor
>   - pass the object being proxied as the first item
>   - the second object is a handler object
> - the handler object is made up of 1 of 13 different "traps"
> - a trap is a function that will intercept calls to properties and let you run code
> - if a trap is not defined, the default behavior is sent to the target object
>
> Proxies are a powerful new way to create and manage the interactions between objects.

## Generators

### 3.24. Generators

#### Intro to generators

> Whenever a function is invoked, the JavaScript engine starts at the top of the function and runs every line of code until it gets to the bottom. There's no way to stop the execution of the function in the middle and pick up again at some later point. This **"run-to-completion"** is the way it's always been:
>
> ```js
> function getEmployee() {
>     console.log('the function has started');
>
>     const names = ['Amanda', 'Diego', 'Joe', 'James', 'Kagure', 'Kavita', 'Orit'];
>
>     for (const name of names) {
>         console.log(name);
>     }
>
>     console.log('the function has ended');
> }
>
> getEmployee();
> ```
>
> Running the code above produces the following output to the console:
>
> ```text
> the function has started
> Amanda
> Diego
> Joe
> James
> Kagure
> Kavita
> Orit
> the function has ended
> ```
>
> But what if you want to print out the first 3 employee names then stop for a bit, then, at some later point, you want to continue where you left off and print out more employee names. With a regular function, you can't do this since there's no way to "pause" a function in the middle of its execution.

#### Pausable Functions

> If we _do_ want to be able to pause a function mid-execution, then we'll need a new type of function available to us in ES6 - generator functions! Let's look at one:
>
> ```js
> function* getEmployee() {
>     console.log('the function has started');
>
>     const names = ['Amanda', 'Diego', 'Joe', 'James', 'Kagure', 'Kavita', 'Orit'];
>
>     for (const name of names) {
>         console.log( name );
>     }
>
>     console.log('the function has ended');
> }
> ```
>
> Notice the asterisk (i.e. `*`) right after the `function` keyword? That asterisk indicates that this function is actually a generator!
>
> Now check out what happens when we try running this function:
>
> ```js
> getEmployee();
>
> // this is the response I get in Chrome:
> getEmployee {[[GeneratorStatus]]: "suspended", [[GeneratorReceiver]]: Window}
> ```
>
> ...umm, what? Where's the "the function has started" text from the top of the function? And why didn't we get any names printed to the console? Those are good questions, but first, a quiz.

#### Quiz Question

Which of the following are valid generators? Pay attention to the placement of the asterisk.

If you're not sure, try running them in your browser's console.

- `function* names() { /* */ }`
- `function * names() { /* */ }`
- `function *names() { /* */ }`

<details>
  <summary><em>Solution</em></summary>

My first try was just the first option (which is actually the community consensus syntax), but I realized it would be all of them and got it on my second try.

- `function* names() { /* */ }`
- `function * names() { /* */ }`
- `function *names() { /* */ }`

> The asterisk of the generator can actually be placed anywhere between the `function` keyword and the function's name. So all three of these are valid generator declarations!
>
> The community has coalesced into having the asterisk appear right next to the `function` keyword (i.e. `function* name() { … }`). But there others that recommend having the asterisk touch the function's name instead. So it's important to realize that the asterisk indicates that it is a generator but that the placement of the asterisk is not important.

</details>

### 3.25. Generators & Iterators

> **WARNING:** We looked at iteration in a previous section, so if you're rusty on it, better check it out again because they're resurfacing here with generators!
>
> When a generator is invoked, it doesn't actually run any of the code inside the function. Instead, it creates and returns an iterator. This iterator can then be used to execute the actual generator's inner code.
>
> ```js
> const generatorIterator = getEmployee();
> generatorIterator.next();
> ```
>
> Produces the code we expect:
>
> ```text
> the function has started
> Amanda
> Diego
> Joe
> James
> Kagure
> Kavita
> Orit
> the function has ended
> ```
>
> Now if you tried the code out for yourself, the first time the iterator's `.next()` method was called it ran all of the code inside the generator. Did you notice anything? The code never paused! So how do we get this magical, pausing functionality?

#### The Yield Keyword

> The `yield` keyword is new and was introduced with ES6. It can only be used inside generator functions. `yield` is what causes the generator to pause. Let's add yield to our generator and give it a try:
>
> ```js
> function* getEmployee() {
>     console.log('the function has started');
>
>     const names = ['Amanda', 'Diego', 'Joe', 'James', 'Kagure', 'Kavita', 'Orit'];
>
>     for (const name of names) {
>         console.log(name);
>         yield;
>     }
>
>     console.log('the function has ended');
> }
> ```
>
> Notice that there's now a `yield` inside the `for..of` loop. If we invoke the generator (which produces an iterator) and then call `.next()`, we'll get the following output:
>
> ```js
> const generatorIterator = getEmployee();
> generatorIterator.next();
> ```
>
> Logs the following to the console:
>
> ```text
> the function has started
> Amanda
> ```
>
> It's paused! But to really be sure, let's check out the next iteration:
>
> ```js
> generatorIterator.next();
> ```
>
> Logs the following to the console:
>
> ```text
> Diego
> ```
>
> So it remembered exactly where we left off! It took the next item in the array (Diego), logged it, and then hit the `yield` again, so it paused again.
>
> Now pausing is all well and good, but what if we could send data from the generator back to the "outside" world? We can do this with `yield`.

#### Yielding Data to the "Outside" World

> Instead of logging the names to the console and then pausing, let's have the code "return" the name and then pause.
>
> ```js
> function* getEmployee() {
>     console.log('the function has started');
>
>     const names = ['Amanda', 'Diego', 'Joe', 'James', 'Kagure', 'Kavita', 'Orit'];
>
>     for (const name of names) {
>         yield name;
>     }
>
>     console.log('the function has ended');
> }
> ```
>
> Notice that now instead of `console.log(name)`; that it's been switched to `yield name;`. With this change, when the generator is run, it will "yield" the name back out to the function _and then pause its execution_. Let's see this in action:
>
> ```js
> const generatorIterator = getEmployee();
> let result = generatorIterator.next();
> result.value // "Amanda"
>
> generatorIterator.next().value // "Diego"
> generatorIterator.next().value // "Farrin"
> ```

#### Generators Quiz Question

How many times will the iterator's .next() method need to be called to fully complete/"use up" the udacity generator function below:

```js
function* udacity() {
    yield 'Richard';
    yield 'James'
}
```

- 0 times
- 1 time
- 2 times
- 3 times

#### Solution

3 times

> It will be called one more time than there are `yield` expressions in the generator function.
>
> The first call to `.next()` will start the function and run to the first `yield`. The second call to `.next()` will pick up where things left off and run to the second `yield`. The third and final call to `.next()` will pick up where things left off again and run to the end of the function.

### 3.26. Sending Data into/out of a Generator

#### Intro to sending data

> So we can get data out of a generator by using the `yield` keyword. We can also send data back _into_ the generator, too. We do this using the `.next()` method:
>
> ```js
> function* displayResponse() {
>     const response = yield;
>     console.log(`Your response is "${response}"!`);
> }
>
> const iterator = displayResponse();
>
> iterator.next(); // starts running the generator function
> iterator.next('Hello Udacity Student'); // send data into the generator
> // the line above logs to the console: Your response is "Hello Udacity Student"!
> ```
>
> Calling `.next()` with data (i.e. `.next('Richard')`) will send data into the generator function where it last left off. It will "replace" the yield keyword with the data that you provided.
>
> So the `yield` keyword is used to pause a generator _and_ used to send data outside of the generator, and then the `.next()` method is used to pass data `into` the generator. Here's an example that makes use of both of these to cycle through a list of names one at a time:
>
> ```js
> function* getEmployee() {
>     const names = ['Amanda', 'Diego', 'Joe', 'James', 'Kagure', 'Kavita', 'Orit'];
>     const facts = [];
>
>     for (const name of names) {
>         // yield *out- each name AND store the returned data into the facts array
>         facts.push(yield name);
>     }
>
>     return facts;
> }
>
> const generatorIterator = getEmployee();
>
> // get the first name out of the generator
> let name = generatorIterator.next().value;
>
> // pass data in *and* get the next name
> name = generatorIterator.next(`${name} is cool!`).value;
>
> // pass data in *and* get the next name
> name = generatorIterator.next(`${name} is awesome!`).value;
>
> // pass data in *and* get the next name
> name = generatorIterator.next(`${name} is stupendous!`).value;
>
> // you get the idea
> name = generatorIterator.next(`${name} is impressive!`).value;
> name = generatorIterator.next(`${name} is stunning!`).value;
> name = generatorIterator.next(`${name} is awe-inspiring!`).value;
>
> // pass the last data in, generator ends and returns the array
> const positions = generatorIterator.next(`${name} is magnificent!`).value;
>
> // displays each name with description on its own line
> positions.join('\n');
> ```

#### Sending Data Quiz Question

What will happen if the following code is run?

```js
function* createSundae() {
    const toppings = [];

    toppings.push(yield);
    toppings.push(yield);
    toppings.push(yield);

    return toppings;
}

var it = createSundae();
it.next('hot fudge');
it.next('sprinkles');
it.next('whipped cream');
it.next();
```

- The `toppings` array will have `undefined` as its last item
- An error will occur
- The generator will be paused, waiting for it's last call to `.next()`

<details>
  <summary><em>Solution</em></summary>

The `toppings` array will have `undefined` as its last item

> Because the first call to `.next()` passes in some data. But that data doesn't get stored anywhere. The last call to `.next()` should have some data since it's being yielded into the last call to `toppings.push()`.

*[Additional notes from James Priest](https://github.com/james-priest/100-days-of-code-log-r2/blob/master/ES6-Built-ins-Pt2.md#solution-2):*

> Remember that the first call to `.next()` will initiate the generator which will stop at the first `yield`. The second call to `.next()` is the call that will supply that `yield with the data.
>
> Count how many yields there are and when data is passed into each of the calls to `.next()`.

</details>

#### Generators Summary

> Generators are a powerful new kind of function that is able to pause its execution while also maintaining its own state. Generators are great for iterating over a list of items one at a time so you can handle each item on its own before moving on to the next one. You can also use generators to handle nested callbacks. For example, let's say that an app needs to get a list of all repositories _and_ the number of times they've been starred. Well, before you can get the number of stars for each repository, you'd need to get the user's information. Then after retrieving the user's profile the code can then take that information to find all of the repositories.
>
> Generators will also be used heavily in upcoming additions to the JavaScript language. One upcoming feature that will make use of them is [async functions](https://github.com/tc39/ecmascript-asyncawait).

### 3.27. Lesson 3 Summary

## Feedback on JavaScript ES6 lesson 3/4

Informative and helpful lesson.

Lesson 3.26 on generators mentions async functions. Async/await was introduced in ES2017. See my notes in [ajax-3-fetch.md](../ajax/ajax-3-fetch.md).

[Next lesson](es6-4-developer-fu.md)

[Previous lesson](es6-2-functions.md)

[(Back to top)](#top)