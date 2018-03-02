
# Lesson 03. An Overview of Service Worker

Udacity Grow with Google Scholarship

Brendon Smith

br3ndonland

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Intro](#intro)
  - [4.01. Introducing the IDB Promised Library](#401-introducing-the-idb-promised-library)
  - [4.02. Getting Started with IDB](#402-getting-started-with-idb)
    - [Create database](#create-database)
    - [Read from database](#read-from-database)
    - [Add another value to the object store](#add-another-value-to-the-object-store)
  - [4.03. Quiz: Getting Started with IDB](#403-quiz-getting-started-with-idb)
    - [Diving deeper into the API](#diving-deeper-into-the-api)
  - [4.04. Quiz: More IDB](#404-quiz-more-idb)
- [Caching](#caching)
  - [4.05. Using the IDB Cache and Display Entries](#405-using-the-idb-cache-and-display-entries)
  - [4.06. Quiz: Using IDB Cache](#406-quiz-using-idb-cache)
  - [4.07. Quiz: Using IDB 2](#407-quiz-using-idb-2)
  - [4.08. Quiz: Cleaning IDB](#408-quiz-cleaning-idb)
    - [Goals](#goals)
    - [App performance changes](#app-performance-changes)
- [Cache photos and avatars](#cache-photos-and-avatars)
  - [4.09. Cache Photos](#409-cache-photos)
  - [4.10. Quiz: Cache Photos Quiz](#410-quiz-cache-photos-quiz)
  - [4.11. Cleaning Photo Cache](#411-cleaning-photo-cache)
  - [4.12. Quiz: Cleaning Photo Cache Quiz](#412-quiz-cleaning-photo-cache-quiz)
  - [4.13. Quiz: Caching Avatars](#413-quiz-caching-avatars)
  - [4.14. Outro](#414-outro)
- [Feedback on Lesson 4](#feedback-on-lesson-4)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Intro
[(back to top)](#top)

### 4.01. Introducing the IDB Promised Library

* This will be a crash course in IndexedDB
* The wittr app will benefit from a **database**. It will allow us to add and remove posts as needed.
* **IndexedDB** allows us to create a **database** for the app. You will generally have one database per app, with multiple **object stores**.
* The database object stores can contain JavaScript objects, strings, numbers, dates, or arrays.
* Changes are made to the database with **transactions**. Transactions are atomic-if one part fails, none of the changes are applied.
* **Indexes** (indices?) organize data by properties.

	<img src="img/udacity-google-04-0101.png" alt="Organizing IndexeDB with indexes" width="400px">

* Why does IndexedDB have a bad reputation?
	- The API is "a little... horrid" and it can create spaghetti code.
	- It has its own event-based promise system (it predates promises) that can be confusing.
* Jake believes in teaching the web platform rather than libraries, but in this case, we will use **[IndexedDB Promised (idb)](https://github.com/jakearchibald/idb)**, which Jake created. It mirrors the IndexedDB API and uses promises instead of events.


### 4.02. Getting Started with IDB

* Navigate to http://localhost:8888/idb-test which is currently just a blank page with a script tag to import `idb`.
* Jake walked through some of the code in `idb`.


#### Create database

* `createObjectStore`: Jake referred to [MDN](https://developer.mozilla.org/en-US/docs/Web/API/IDBDatabase/createObjectStore). Jake creates an object store named 'keyval'.
* `IDBObjectStore.put()`: [MDN](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/put)

```javascript
import idb from 'idb';

var dbPromise = idb.open('test-db', 1, function(upgradeDb) {
  var keyValStore = upgradeDb.createObjectStore('keyval');
  keyValStore.put('world', 'hello');
});
```


#### Read from database

```javascript
dbPromise.then(function(db) {
  var tx = db.transaction('keyval');
  var keyValStore = tx.objectStore('keyval');
  return keyValStore.get('hello');
}).then(function(val) {
   console.log('The value of "hello" is:', val);
});
```

#### Add another value to the object store


```javascript
dbPromise.then(function(db) {
  var tx = db.transaction('keyval', 'readwrite');
  var keyValStore = tx.objectStore('keyval');
  keyValStore.put('bar', 'foo');
  return tx.complete;
}).then(function() {
  console.log('Added foo:bar to keyval');
}).catch(function(error) {
  console.error('Transaction failed:', error);
});
```


### 4.03. Quiz: Getting Started with IDB

*Git*

* Checkout to new branch:
	```bash
	$ git reset --hard
	$ git checkout origin/page-skeleton
	```

<details>
	<summary><em>Solution</em></summary>

Based on the code [above](#add-another-value-to-the-object-store):

*public/js/idb-test/index.js*

```javascript
dbPromise.then(function(db) {
  var tx = db.transaction('keyval', 'readwrite');
  var keyValStore = tx.objectStore('keyval');
  keyValStore.put('sloth', 'favoriteAnimal');
  return tx.complete;
}).then(function() {
  console.log('Added favoriteAnimal:sloth to keyval');
}).catch(function(error) {
  console.error('Transaction failed:', error);
});
```

* Refresh the app at http://localhost:8888/ 
* Test on settings page at http://localhost:8889/ with "idb-animal".

</details>

"If you're still alive at this point, you're doing really well."


#### Diving deeper into the API

The code above was not very practical, because you would have to change and re-run it every time you added an object. What if we wanted to add a bunch of values?

```javascript
// upgrade database
var dbPromise = idb.open('test-db', 2, function(upgradeDb) {
  switch (upgradeDb.oldVersion) {
    case 0:
      var keyValStore = upgradeDb.createObjectStore('keyval');
      keyValStore.put('world', 'hello');
    case 1:
      upgradeDb.createObjectStore('people', {
        keyPath: 'name'
      });
  }
});

// add data to object store
// each person is a javascript object
dbPromise
  .then(function(db) {
    var tx = db.transaction('people', 'readwrite');
    var peopleStore = tx.objectStore('people');

    peopleStore.put({
      name: 'Sam Munoz',
      age: 25,
      favoriteAnimal: 'dog'
    });

    peopleStore.put({
      name: 'Susan Keller',
      age: 34,
      favoriteAnimal: 'cat'
    });

    peopleStore.put({
      name: 'Lillie Wolfe',
      age: 28,
      favoriteAnimal: 'dog'
    });

    peopleStore.put({
      name: 'Marc Stone',
      age: 39,
      favoriteAnimal: 'cat'
    });

    return tx.complete;
  })
  .then(function() {
    console.log('People added!');
  });
```


### 4.04. Quiz: More IDB

*Task*

Create an index that sorts people by age.


*Git*

* Checkout to new branch:
	```bash
	$ git reset --hard
	$ git checkout origin/task-idb-people
	```

<details>
	<summary><em>Solution</em></summary>

*public/js/idb-test/index.js*

```javascript
// upgrade database
var dbPromise = idb.open('test-db', 4, function(upgradeDb) {
  switch (upgradeDb.oldVersion) {
    case 0:
      var keyValStore = upgradeDb.createObjectStore('keyval');
      keyValStore.put('world', 'hello');
    case 1:
      upgradeDb.createObjectStore('people', { keyPath: 'name' });
    case 2:
      var peopleStore = upgradeDb.transaction.objectStore('people');
      peopleStore.createIndex('animal', 'favoriteAnimal');
    case 3:
      peopleStore = upgradeDb.transaction.objectStore('people');
      peopleStore.createIndex('age', 'age');
  }
});

// sort the people objects
dbPromise
  .then(function(db) {
    var tx = db.transaction('people');
    var peopleStore = tx.objectStore('people');
    var ageIndex = peopleStore.index('age');

    return ageIndex.getAll();
  })
  .then(function(people) {
    console.log('People by age:', people);
  });
```

* Test on settings page at http://localhost:8889/ with "idb-age".
* We can cycle through the people objects one at a time using **cursors**. I have used cursor objects in Python before (see my [SQL database analysis project](https://github.com/br3ndonland/udacity-fsnd03-p01-logs)).
	```javascript
	dbPromise
	  .then(function(db) {
	    var tx = db.transaction('people');
	    var peopleStore = tx.objectStore('people');
	    var ageIndex = peopleStore.index('age');

	    return ageIndex.openCursor();
	  })
	  .then(function(cursor) {
	    if (!cursor) return;
	    console.log('Cursored at:', cursor.value.name);
	    return cursor.continue();
	  });
	```
* We can store the cursor cycle as a function, a "neat trick":
	```javascript
	dbPromise
	  .then(function(db) {
	    var tx = db.transaction('people');
	    var peopleStore = tx.objectStore('people');
	    var ageIndex = peopleStore.index('age');

	    return ageIndex.openCursor();
	  })
	  .then(function logPerson(cursor) {
	    if (!cursor) return;
	    console.log('Cursored at:', cursor.value.name);
	    // cursor.update(newValue)
	    // cursor.delete()
	    return cursor.continue().then(logPerson);
	  })
	  .then(function() {
	    console.log('Done cursoring');
	  });
	```

* To restore the repo to this point in the future:	
	```bash
	$ git reset --hard
	$ git checkout origin/idb-cursoring
	```

</details>


## Caching
[(back to top)](#top)

### 4.05. Using the IDB Cache and Display Entries

Next, we will create a database for wittr posts. The posts will still arrive via a web socket,but can be served offline as well from `idb`.

<img src="img/udacity-google-04-0501.png" alt="Using the IDB Cache and Display Entries" width="400px">

* *public/js/main/IndexController.js*
* The `IndexController._openSocket` method is called to open the Web Socket.
* `IndexController._openSocket` listens for the message event, and passes data to the `IndexController._onSocketMessage` method.
* `IndexController._onSocketMessage` parses JSON data and passes it to `IndexController._postsView.addPosts`.


### 4.06. Quiz: Using IDB Cache

*Git*

* Checkout to new branch:
	```bash
	$ git reset --hard
	$ git checkout origin/task-idb-store
	```

*Task*

> Your task is to return a Promise for a database called 'wittr' that has an object store called 'wittrs' that uses 'id' as its key and has an index called called 'by-date', which is sorted by the 'time' property.
> 
> Once you've done that, you'll need to add messages to the database. Down in the IndexController._onSocketMessage method, the database has been fetched. Your task is to add each of the messages to the Wittr store. Note that we're not using the entries in the database yet - we'll do that in the next chapter.

If the database gets messed up, run `indexedDB.deleteDatabase('wittr')` in DevTools to reset.

<details>
	<summary><em>Solution</em></summary>

*public/js/main/IndexController.js*

```javascript
// Open the database
function openDatabase() {
  // If the browser doesn't support service worker,
  // we don't care about having a database
  if (!navigator.serviceWorker) {
    return Promise.resolve();
  }

  // return a promise for a database called 'wittr'
  // that contains one objectStore: 'wittrs'
  // that uses 'id' as its key
  // and has an index called 'by-date', which is sorted
  // by the 'time' property
  return idb.open('wittr', 1, function(upgradeDb) {
    var store = upgradeDb.createObjectStore('wittrs', {
      keyPath: 'id'
    });

    store.createIndex('by-date', 'time');
  });
}

// called when the web socket sends message data
IndexController.prototype._onSocketMessage = function(data) {
  var messages = JSON.parse(data);

  this._dbPromise.then(function(db) {
    if (!db) return;

    // loop through messages and add to store
    var tx = db.transaction('wittrs', 'readwrite');
    var store = tx.objectStore('wittrs');

    messages.forEach(function(message) {
      store.put(message);
    });

    return tx.complete;
  });

  this._postsView.addPosts(messages);
};
```

* Refresh the app at http://localhost:8888/ 
* Test on settings page at http://localhost:8889/ with "idb-store".

</details>



### 4.07. Quiz: Using IDB 2

We now have wittr posts in the database, but we need to serve posts from IDB wittrs before opening the web socket.

*Git*

* Checkout to new branch:
	```bash
	$ git reset --hard
	$ git checkout origin/task-show-stored
	```

<details>
	<summary><em>Solution</em></summary>

*public/js/main/IndexController.js*

```javascript
IndexController.prototype._showCachedMessages = function() {
  var indexController = this;

  return this._dbPromise.then(function(db) {
    // if we're already showing posts, eg shift-refresh
    // or the very first load, there's no point fetching
    // posts from IDB
    if (!db || indexController._postsView.showingPosts()) return;

    // TODO: get all of the wittr message objects from indexeddb,
    // then pass them to:
    // indexController._postsView.addPosts(messages)
    // in order of date, starting with the latest.
    // Remember to return a promise that does all this,
    // so the websocket isn't opened until you're done!
    var index = db
      .transaction('wittrs')
      .objectStore('wittrs')
      .index('by-date');

    return index.getAll().then(function(messages) {
      indexController._postsView.addPosts(messages.reverse());
    });
  });
};
```


* Refresh the app at http://localhost:8888/ 
* Test on settings page at http://localhost:8889/ with "serve-skeleton".

</details>


### 4.08. Quiz: Cleaning IDB

So far, so good, but we have only been adding posts to the database. We can't just keep adding posts indefinitely.

In this task, we will modify the database so it only has 30 wittr items at a time.

*Git*

* Checkout to new branch:
	```bash
	$ git reset --hard
	$ git checkout origin/task-clean-db
	```

<details>
	<summary><em>Solution</em></summary>

*public/js/main/IndexController.js*, `IndexController._onSocketMessage` method

```javascript
IndexController.prototype._onSocketMessage = function(data) {
  var messages = JSON.parse(data);

  this._dbPromise.then(function(db) {
    if (!db) return;

    var store = db.transaction('wittrs', 'readwrite').objectStore('wittrs');
    // create a variable to index the posts by date
    var index = store.index('by-date');

    messages.forEach(function(message) {
      store.put(message);
    });

    // keep the newest 30 entries in 'wittrs', delete the rest.
    //
    // Hint: you can use .openCursor(null, 'prev') to open a cursor
    // that goes through an index/store backwards.
    return index
      .openCursor(null, 'prev')
      .then(function(cursor) {
        return cursor.advance(30);
      })
      .then(function deletePost(cursor) {
      	// if the entry is undefined, stop
        if (!cursor) return;
        cursor.delete();
        // otherwise continue looping through and deleting posts
        return cursor.continue().then(deletePost);
      });
  });

  this._postsView.addPosts(messages);
};
```

* Refresh the app at http://localhost:8888/ 
* Test on settings page at http://localhost:8889/ with "idb-clean".

</details>


#### Goals

* ~~Unobtrusive app updates~~
* ~~Get the user onto the latest version~~
* ~~Continually update cache of posts~~
* Cache photos
* Cache avatars


#### App performance changes

* Perfect: Not much change, but "perfect doesn't really exist."
* Slow: Content renders much more quickly.
* Lie-Fi: Users actually get content, instead of a blank screen.
* Offline: Users still get content.
* Images are still slow or broken, so we will fix those next.


## Cache photos and avatars
[(back to top)](#top)

### 4.09. Cache Photos

* We want to cache photos as they appear.
* If we retrieve images from the cache API, it's more memory efficient and renders faster:

	<img src="img/udacity-google-04-0901.png" alt="Caching and serving photos from service worker" width="400px">

* Images will be stored in a separate cache from the other static content. This allows the photos to live on between different versions of the app.
* We will be working with a responsive image. It has different sizes based on the viewport width.
* Using responses multiple times: `response.json();` cannot be re-read with `response.blob();`. Once the data are read in as json, it disappears from memory. This applies to `event.respondWith(response);` as well. This is a problem for our photos. We want to open a cache, fetch from the network, and send the response both to the cache and the browser. To fix this, we clone the response with `response.clone()`. A clone goes to the cache, and the original response gets sent to the page.


### 4.10. Quiz: Cache Photos Quiz

*Git*

* Checkout to new branch:
	```bash
	$ git reset --hard
	$ git checkout origin/task-cache-photos
	```

*public/js/sw/index.js* (the service worker script)

<details>
	<summary><em>Solution</em></summary>

```javascript
function servePhoto(request) {
  // Photo urls look like:
  // /photos/9-8028-7527734776-e1d2bda28e-800px.jpg
  // But storageUrl has the -800px.jpg bit missing.
  // Use this url to store & match the image in the cache.
  // This means you only store one copy of each photo.
  var storageUrl = request.url.replace(/-\d+px\.jpg$/, '');

  // return images from the "wittr-content-imgs" cache
  // if they're in there. Otherwise, fetch the images from
  // the network, put them into the cache, and send it back
  // to the browser.
  //
  // HINT: cache.put supports a plain url as the first parameter
  return caches.open(contentImgsCache).then(function(cache) {
    return cache.match(storageUrl).then(function(response) {
      return (
        response ||
        fetch(request).then(function(networkResponse) {
          cache.put(storageUrl, networkResponse.clone());
          return networkResponse;
        })
      );
    });
  });
}
```

* Refresh the app at http://localhost:8888/ 
* Test on settings page at http://localhost:8889/ with "cache-photos".

</details>


### 4.11. Cleaning Photo Cache

As we saw in [4.08. Quiz: Cleaning IDB](#408-quiz-cleaning-idb), we eventually need to clear out the cache. We can't keep adding to it infinitely.

If we want to remove specific entries from the cache, we can use `cache.delete`, passing in the URL or the request of the thing we want to delete:
```javascript
cache.delete(request);
```

There's also a `cache.keys` method that returns a Promise providing all the requests for entries in the cache:
```javascript
cache.keys().then(function(requests) {
  // ...
});
```

Next, we will clean the image cache.


### 4.12. Quiz: Cleaning Photo Cache Quiz

*Git*

* Checkout to new branch:
	```bash
	$ git reset --hard
	$ git checkout origin/task-clean-photos
	```

Implement the `IndexController._cleanImageCache` method in *public/js/main/IndexController.js*.

<details>
	<summary><em>Solution</em></summary>

```javascript
IndexController.prototype._cleanImageCache = function() {
  return this._dbPromise.then(function(db) {
    if (!db) return;

    // open the 'wittr' object store, get all the messages,
    // gather all the photo urls.
    //
    // Open the 'wittr-content-imgs' cache, and delete any entry
    // that you no longer need.
    //
    // create an array of images to keep
    var imagesNeeded = [];

    var tx = db.transaction('wittrs');
    // get object store and messages
    return tx
      .objectStore('wittrs')
      .getAll()
      .then(function(messages) {
        messages.forEach(function(message) {
          if (message.photo) {
            imagesNeeded.push(message.photo);
          }
        });

        // open image cache and get stored image requests
        return caches.open('wittr-content-imgs');
      })
      .then(function(cache) {
        return cache.keys().then(function(requests) {
          requests.forEach(function(request) {
            var url = new URL(request.url);

            if (!imagesNeeded.includes(url.pathname)) {
              cache.delete(request);
            }
          });
        });
      });
  });
};
```

* Refresh the app at http://localhost:8888/ 
* Test on settings page at http://localhost:8889/ with "cache-clean".

</details>


#### Goals

* ~~Unobtrusive app updates~~
* ~~Get the user onto the latest version~~
* ~~Continually update cache of posts~~
* ~~Cache photos~~
* Cache avatars


### 4.13. Quiz: Caching Avatars

Final task! Caching avatars. Avatars are also responsive images, but they vary by density rather than width. The URL pattern is, correspondingly, a little different than for other images:

```html
<img width="40" height="40"
  src="/avatars/sam-1x.jpg"
  srcset="/avatars/sam-2x.jpg 2x,
          /avatars/sam-3x.jpb 3x">
```

*Git*

* Checkout to new branch:
	```bash
	$ git reset --hard
	$ git checkout origin/task-cache-avatars
	```

Call and implement the `serveAvatar` function in *public/js/sw/index.js* (the service worker script)

<details>
	<summary><em>Solution</em></summary>

*Call the `serveAvatar` function from within the `fetch` event handler:*

```javascript
// respond to avatar urls by responding with
// the return value of serveAvatar(event.request)
if (requestUrl.pathname.startsWith('/avatars/')) {
  event.respondWith(serveAvatar(event.request));
  return;
}
```

*Implement the `serveAvatar` function:*

```javascript
function serveAvatar(request) {
  // Avatar urls look like:
  // avatars/sam-2x.jpg
  // But storageUrl has the -2x.jpg bit missing.
  // Use this url to store & match the image in the cache.
  // This means you only store one copy of each avatar.
  var storageUrl = request.url.replace(/-\dx\.jpg$/, '');

  // return images from the "wittr-content-imgs" cache
  // if they're in there. But afterwards, go to the network
  // to update the entry in the cache.
  //
  // Note that this is slightly different from servePhoto!
  return caches.open(contentImgsCache).then(function(cache) {
    return cache.match(storageUrl).then(function(response) {
      var fetchPromise = fetch(request).then(function(networkResponse) {
        cache.put(storageUrl, networkResponse.clone());
        return networkResponse;
      });

      return response || fetchPromise;
    });
  });
}
```

* Refresh the app at http://localhost:8888/ 
* Test on settings page at http://localhost:8889/ with "cache-avatars".

</details>


### 4.14. Outro

#### Goals

* ~~Unobtrusive app updates~~
* ~~Get the user onto the latest version~~
* ~~Continually update cache of posts~~
* ~~Cache photos~~
* ~~Cache avatars~~

**We're now completely offline first!**


#### App performance changes

* Perfect: Not much change, but "perfect doesn't really exist."
* Slow: Content renders instantly.
* Lie-Fi: Users get content instantly, instead of a blank screen.
* Offline: Users get content, and a non-disruptive custom error, instead of error page.

<img src="img/udacity-google-05-0101.png" alt="Offline web apps completion" width="75%">


## Feedback on Lesson 4

Again, a very informative and helpful lesson. It would be nice to use Udacity's browser-based quiz system instead of all the git resets, but I understand that it would be difficult to demo the app without a local clone of the git repo.

[next lesson](udacity-google-05.md)

[previous lesson](udacity-google-03.md)

[(back to top)](#top)