# An Overview of Service Worker

<a href="https://www.udacity.com/">
  <img src="https://s3-us-west-1.amazonaws.com/udacity-content/rebrand/svg/logo.min.svg" width="300" alt="Udacity logo">
</a>

[Offline Web Applications by Google course](https://www.udacity.com/course/offline-web-applications--ud899) lesson 2/3

Udacity Google Mobile Web Specialist Nanodegree program part 2 lesson 17

Udacity Grow with Google Scholarship challenge course lesson 03

Brendon Smith

br3ndonland

## Table of Contents <!-- omit in toc -->

- [Service Worker basics](#service-worker-basics)
  - [2.01. An Overview of Service Worker](#201-an-overview-of-service-worker)
  - [2.02. Quiz: Scoping Quiz](#202-quiz-scoping-quiz)
  - [2.03. Adding a Service Worker To the Project](#203-adding-a-service-worker-to-the-project)
  - [2.04. Quiz: Registering a Service Worker](#204-quiz-registering-a-service-worker)
  - [2.05. The Service Worker Lifecycle](#205-the-service-worker-lifecycle)
  - [2.06. Quiz: Enabling Service Worker Dev Tools](#206-quiz-enabling-service-worker-dev-tools)
  - [2.07. Quiz: Service Worker Dev Tools](#207-quiz-service-worker-dev-tools)
  - [2.08. Quiz: Service Worker Dev Tools 2](#208-quiz-service-worker-dev-tools-2)
  - [2.09. Service Worker Dev Tools Continued](#209-service-worker-dev-tools-continued)
- [Service Worker and requests](#service-worker-and-requests)
  - [2.10. Hijacking Requests](#210-hijacking-requests)
  - [2.11. Quiz: Hijacking Requests 1 Quiz](#211-quiz-hijacking-requests-1-quiz)
  - [2.12. Hijacking Requests 2](#212-hijacking-requests-2)
  - [2.13. Quiz: Hijacking Requests 2 Quiz](#213-quiz-hijacking-requests-2-quiz)
  - [2.14. Hijacking Requests 3](#214-hijacking-requests-3)
  - [2.15. Quiz: Hijacking Requests 3 Quiz](#215-quiz-hijacking-requests-3-quiz)
- [Service Worker and caching](#service-worker-and-caching)
  - [2.16. Caching and Serving Assets](#216-caching-and-serving-assets)
  - [2.17. Quiz: Install and Cache Quiz](#217-quiz-install-and-cache-quiz)
  - [2.18. Quiz: Cache Response Quiz](#218-quiz-cache-response-quiz)
  - [2.19. Updating the Static Cache](#219-updating-the-static-cache)
  - [2.20. Quiz: Update Your CSS Quiz](#220-quiz-update-your-css-quiz)
  - [2.21. Quiz: Update Your CSS 2](#221-quiz-update-your-css-2)
  - [2.22. Adding UX to the Update Process](#222-adding-ux-to-the-update-process)
  - [2.23. Quiz: Adding UX Quiz](#223-quiz-adding-ux-quiz)
  - [2.24. Triggering an Update](#224-triggering-an-update)
  - [2.25. Quiz: Triggering an Update Quiz](#225-quiz-triggering-an-update-quiz)
  - [2.26. Quiz: Caching the Page Skeleton](#226-quiz-caching-the-page-skeleton)
- [Lesson feedback](#lesson-feedback)

## Service Worker basics

### 2.01. An Overview of Service Worker

- **Service worker is a JavaScript file that sits between the browser and network requests.**
- It returns a **promise**.
- `navigator.serviceWorker.register('/sw.js')`
- Jake made a website called [is serviceworker ready?](https://jakearchibald.github.io/isserviceworkerready/), to evaluate browser compatibility with different aspects of Service Worker.

### 2.02. Quiz: Scoping Quiz

Got this on my first try.

<details>
  <summary><em>Solution</em></summary>
  <p>
    The scope defines the URLs to be handled. ServiceWorker will handle any deeper URL, but not shallower URLs.
  </p>
</details>

### 2.03. Adding a Service Worker To the Project

### 2.04. Quiz: Registering a Service Worker

- **This was the first coding task of the course.**
- */js/sw/index.js* is the ServiceWorker.
- JavaScript doesn't have "private methods," but it's common to call methods starting with an underscore, like `this._openSocket();`, if they will only be called by other methods of this object.
- Service workers are limited to HTTPS, except localhost.

Git

- Add the register service worker command. We want the scope to be the whole origin, so the default scope is fine.
- You don't actually need to stop the server to switch branches, but I did.

  ```shell
  $ git reset --hard
  $ git checkout task-register-sw
  ```

<details>
  <summary><em>Solution</em></summary>

- Service registration code:

  ```javascript
  IndexController.prototype._registerServiceWorker = function() {
    // register service worker
    if (!navigator.serviceWorker) return;

    navigator.serviceWorker.register('/sw.js').then(function() {
      console.log('Registration worked!');
    }).catch(function() {
      console.log('Registration failed!');
    });
  };
  ```

- Go to [http://localhost:8889/](http://localhost:8889/) and type `registered`.
- I tried several times, but it didn't work, and dev tools didn't help.
- I basically had the answer, just needed a little more code.
- I also needed to check my code in a different sequence:
  - Save the JavaScript file *IndexController.js*
  - Refresh [http://localhost:8888/](http://localhost:8888/)
  - Check JavaScript console with cmd+alt+j (note that Firefox developer tools separates the JavaScript console from the other dev tools)
  - Now go to [http://localhost:8889/](http://localhost:8889/) and type `registered`.

</details>

### 2.05. The Service Worker Lifecycle

### 2.06. Quiz: Enabling Service Worker Dev Tools

- We will be using Chrome Canary.

### 2.07. Quiz: Service Worker Dev Tools

- The Resources tab is no longer there in Chrome Canary. The resources are just shown directly.
- Typing "sw-waiting" into the test field shows there's a service worker waiting.

### 2.08. Quiz: Service Worker Dev Tools 2

### 2.09. Service Worker Dev Tools Continued

- **The Sources panel of dev tools should have a Service Workers tab next to Scope and Watch with the option to "Force update on page load." I don't see it.** I found the [answer](https://discussions.udacity.com/t/solved-force-update-on-page-load-not-appearing-in-chrome-canary/528320/4) in the discussion forum: It's now on the Applications tab. I also tried Firefox developer edition, but couldn't find the equivalent setting.

[(Back to top)](#top)

## Service Worker and requests

### 2.10. Hijacking Requests

- **Finally using the service worker to intercept requests and serve offline content!**
- This part demonstrated **general request hijacking.**
- *sw/index.js*:

  ```javascript
  self.addEventListener('fetch', function(event) {
    event.respondWith(
      new Response('Hello, Offline World!'));
    });
  ```

### 2.11. Quiz: Hijacking Requests 1 Quiz

Git

- We had to checkout to a new branch.
- I was getting an error:

  ```text
  $ git reset --hard
  HEAD is now at 1aff011 Method to register SW
  $ git checkout task-custom-response
  error: pathspec 'task-custom-response' did not match any file(s) known to git.
  ```

  I had to create the branch in a separate step:

  ```text
  $ git branch task-custom-response
  $ git checkout task-custom-response
  Switched to branch 'task-custom-response'
  ```

  But then the *sw/index.js* file was blank.

  I had to go back to master, find the branch on origin, and delete the branch I made:

  ```text
  $ git checkout master
  Switched to branch 'master'
  Your branch is up-to-date with 'origin/master'.
  $ git branch
  - master
    task-custom-response
    task-register-sw
  $ git branch -d task-custom-response
  Deleted branch task-custom-response (was 28d9ac3).
  $ git checkout origin/task-custom-response
  Note: checking out 'origin/task-custom-response'.

  You are in 'detached HEAD' state. You can look around, make experimental
  changes and commit them, and you can discard any commits you make in this
  state without impacting any branches by performing another checkout.

  If you want to create a new branch to retain commits you create, you may
  do so (now or later) by using -b with the checkout command again. Example:

    git checkout -b <new-branch-name>

  HEAD is now at 4f2c245... TODOs for custom response task
  br3ndonland ((4f2c245...)) wittr
  $
  ```

  This finally showed me the code I was supposed to see in *sw/index.js*:

  ```javascript
  self.addEventListener('fetch', function(event) {
    // TODO: respond to all requests with an html response
    // containing an element with class="a-winner-is-me".
    // Ensure the Content-Type of the response is "text/html"
    console.log(event.request);
  });
  ```

<details>
  <summary><em>Solution</em></summary>

- I had the HTML right on the first try, but didn't know how to set the content type so I checked the solution for that. So many curly braces.

  ```javascript
    self.addEventListener('fetch', function(event) {
      // respond to all requests with an html response
      // containing an element with class="a-winner-is-me".
      // Ensure the Content-Type of the response is "text/html"
      event.respondWith(
        new Response('<b class="a-winner-is-me">Hello, Offline HTML World!</b>', {
          headers: {'Content-Type': 'text/html'}
        })
      );
    });
  ```

- Refresh the app at [http://localhost:8888/](http://localhost:8888/)
- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "html-response"
- The test verified. As recommended in the video, I disabled the "Force update on reload" option (to keep the JavaScript after reload), switched to offline mode in [http://localhost:8889/](http://localhost:8889/) (not in dev tools), and the text still appears. Service worker is working!

</details>

### 2.12. Hijacking Requests 2

- Now that we are able to respond to all requests with the same HTML, we will customize the response based on the input. This is **selective response hijacking.**
- We will need to work with HTTP requests.
- **The original JavaScript HTTP request method `XMLHTTPRequest` sucks. The XHR API is over 15 years old. The syntax is strange: It says XML, though it deals with other file types, it says HTTP, although it works with filesystem also, and Request, even though the returned object is a strange mixture of request and response. The event handler puts you in "callback hell."**
- The [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) is an improvement over the [XMLHttpRequest API](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest).

  ```javascript
  fetch('/foo').then(function(response)) {
    return response.json();
  }).then(function(data) {
    console.log(data);
  }).catch(function() {
    console.log('It failed')
  })
  ```

### 2.13. Quiz: Hijacking Requests 2 Quiz

Git

- Checkout to the new branch:

  ```text
  $ git reset --hard
  HEAD is now at 4f2c245 TODOs for custom response task
  $ git checkout origin/gif-response
  Previous HEAD position was 4f2c245... TODOs for custom response task
  HEAD is now at adf8827... Responding with gif
  ```

- Return a response if the request is for a .jpg.

<details>
  <summary><em>Solution</em></summary>

- Here was my first attempt, based on what we had learned so far:

  ```javascript
  self.addEventListener('fetch', function(event) {
    // TODO: only respond to requests with a
    // url ending in ".jpg"
    if (!.jpg) return;
    event.respondWith(
      fetch('/imgs/dr-evil.gif')
    );
  });
  ```

- Refresh the app at [http://localhost:8888/](http://localhost:8888/)
- Test on settings page at [http://localhost:8889/](http://localhost:8889/)
- Jake demonstrated the solution.
  - What other properties does `event.Request()` have? He acknowledged that we didn't have enough information yet, and Google searched "mdn request".

  ```javascript
  self.addEventListener('fetch', function(event) {
    // TODO: only respond to requests with a
    // url ending in ".jpg"
    if (event.request.url.endsWith('.jpg')) {
      event.respondWith(
        fetch('/imgs/dr-evil.gif')
      );
    }
  });
  ```

</details>

### 2.14. Hijacking Requests 3

- New code from video:

  ```javascript
  self.addEventListener('fetch', function(event) {
    event.respondWith(
      fetch(event.request).then(function(response) {
        if (response.status == 404) {
          return new Response("Whoops, not found");
        }
        return response;
      }).catch(function() {
        return new Response("Uh oh, that totally failed!");
      })
    );
  });
  ```

### 2.15. Quiz: Hijacking Requests 3 Quiz

- Respond with Dr. Evil GIF instead of custom text.

  ```javascript
  self.addEventListener('fetch', function(event) {
    event.respondWith(
      fetch(event.request).then(function(response) {
        if (response.status === 404) {
          // TODO: instead, respond with the gif at
          // /imgs/dr-evil.gif
          // using a network request
          return new Response("Whoops, not found");
        }
        return response;
      }).catch(function() {
        return new Response("Uh oh, that totally failed!");
      })
    );
  });
  ```

Git

- Checkout to the new branch:

  ```text
  $ git reset --hard
  HEAD is now at adf8827 Responding with gif
  $ git checkout origin/error-handling
  Note: checking out 'origin/error-handling'.

  You are in 'detached HEAD' state. You can look around, make experimental
  changes and commit them, and you can discard any commits you make in this
  state without impacting any branches by performing another checkout.

  If you want to create a new branch to retain commits you create, you may
  do so (now or later) by using -b with the checkout command again. Example:

    git checkout -b <new-branch-name>

  HEAD is now at de59554... Handling 404 and failure
  ```

<details>
  <summary><em>Solution</em></summary>

- First attempt:

  ```javascript
  self.addEventListener('fetch', function(event) {
    event.respondWith(
      fetch(event.request).then(function(response) {
        if (response.status === 404) {
      event.respondWith(
        fetch('/imgs/dr-evil.gif'))
          return new Response("Whoops, not found");
        }
        return response;
      }).catch(function() {
        return new Response("Uh oh, that totally failed!");
      })
    );
  });
  ```

- Refresh the app at [http://localhost:8888/](http://localhost:8888/)
- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "gif-404"
- Solution
  - I just needed to simplify my code a little bit.
  - If you return a promise within a promise, it returns the eventual value to the outer promise.

  ```javascript
  self.addEventListener('fetch', function(event) {
    event.respondWith(
      fetch(event.request).then(function(response) {
        if (response.status === 404) {
          // instead, respond with the gif at
          // /imgs/dr-evil.gif
          // using a network request
          return fetch('/imgs/dr-evil.gif');
        }
        return response;
      }).catch(function() {
        return new Response("Uh oh, that totally failed!");
      })
    );
  });
  ```

</details>

[(Back to top)](#top)

## Service Worker and caching

### 2.16. Caching and Serving Assets

- The cache API gives us the `caches` object on the global namespace.
- Start the cache

  ```javascript
  caches.open('my-stuff').then(function(cache) {
    //...
  });
  ```

- Add cache items with `cache.put()`

  ```javascript
  cache.put(request, response);
  ```

- Add cache items with `cache.addAll()`: accepts array of URLs, fetches them, and puts the response pairs into the cache. This operation is **atomic**: if any fail to cache, none are added to the cache.

  ```javascript
  cache.addAll([
    '/foo',
    'bar'
  ]);
  ```

- To retrieve items from the cache, use `cache.match`. It will return a promise if the query is found in the cache.

  ```javascript
  cache.match(request)
  ```

- We can control caching when the service worker is installed.

### 2.17. Quiz: Install and Cache Quiz

Git

- Checkout to the new branch:

  ```shell
    $ git reset --hard
    $ git checkout task-install
  ```

<details>
  <summary><em>Solution</em></summary>

- Code

  ```javascript
    self.addEventListener('install', function(event) {
      event.waitUntil(
        caches.open('wittr-static-v1').then(function(cache) {
          return cache.addAll([
            '/',
            'js/main.js',
            'css/main.css',
            'imgs/icon.png',
            'https://fonts.gstatic.com/s/roboto/v15/2UX7WLTfW3W8TclTUvlFyQ.woff',
            'https://fonts.gstatic.com/s/roboto/v15/d-6IYplOFocCacKzxwXSOD8E0i7KZn-EPnyo3HZu7kw.woff'
          ])
        })
      );
    });

    self.addEventListener('fetch', function(event) {
      // Leave this blank for now.
      // We'll get to this in the next task.
    });
  ```

- Refresh the app at [http://localhost:8888/](http://localhost:8888/)
- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "install-cached"

</details>

### 2.18. Quiz: Cache Response Quiz

Combining `event.respondWith()` and `cache.match()`.

Git

- Checkout to the new branch:

  ```shell
  $ git reset --hard
  $ git checkout origin/task-cache-response
  ```

<details>
  <summary><em>Solution</em></summary>

- Code (Combined 17. Quiz: Install and Cache Quiz and 18. Quiz: Cache Response Quiz)

  ```javascript
  self.addEventListener('install', function(event) {
    event.waitUntil(
      caches.open('wittr-static-v1').then(function(cache) {
        return cache.addAll([
          '/',
          'js/main.js',
          'css/main.css',
          'imgs/icon.png',
          'https://fonts.gstatic.com/s/roboto/v15/2UX7WLTfW3W8TclTUvlFyQ.woff',
          'https://fonts.gstatic.com/s/roboto/v15/d-6IYplOFocCacKzxwXSOD8E0i7KZn-EPnyo3HZu7kw.woff'
        ])
      })
    );
  });

  self.addEventListener('fetch', function(event) {
    // respond with an entry from the cache if there is one.
    // if not, fetch from network.
    event.respondWith(
      caches.match(event.request).then(function(response) {
        if (response) return response;
        return fetch(event.request);
      })
    );
  });
  ```

- Refresh the app at [http://localhost:8888/](http://localhost:8888/)
- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "cache-served"
- At this point, we are starting to get a substantial amount of content offline.
- They could have combined the git commits here. We were working with a different function in 18 than in 17, so we didn't really need a git reset.

</details>

#### Goals

- Unobtrusive app updates
- Get the user onto the latest version
- Continually update cache of posts
- Cache photos
- Cache avatars

### 2.19. Updating the Static Cache

- Disabling force update on page load, to more closely simulate the end user experience.
- We are now going to clear the old cache, so that updates show up, even after disabling force update on page load.
- We can use `caches.delete(cacheName)` or `caches.keys();`
- Jake showed us the theme colors in the Sass .scss file at */public/scss/_theme.scss*.

### 2.20. Quiz: Update Your CSS Quiz

Git

- Checkout to new branch:

  ```shell
    $ git reset --hard
    $ git checkout origin/task-handling-updates
  ```

<details>
  <summary><em>Solution</em></summary>

- Code: Jake says there's a "simple way" and a "scalable way."
- Simple way:
  - Change CSS
  - Change name of cache to 'wittr-static-v2'
  - Add `caches.delete(wittr-static-v1)`
- Scalable way:
  - Can't simply delete the cache name each time. Too messy.
  - Instead, maintain a safe list of wanted cache names and remove unwanted ones.
  - Store the name of the static cache in a variable (at top of service worker).
    ```javascript
    var staticCacheName = 'wittr-static-v2';
    ```
  - In the activate event, get all the cache names that exist.
- Refresh the app at [http://localhost:8888/](http://localhost:8888/)
- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "new-cache-ready"
- *Jake also recommends auto-generating hashes for filenames, so they can be updated and ensure the latest versions.*

</details>

#### Goals after 2.20

- ~~Unobtrusive app updates~~
- Get the user onto the latest version
- Continually update cache of posts
- Cache photos
- Cache avatars

### 2.21. Quiz: Update Your CSS 2

- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "new-cache-used"

### 2.22. Adding UX to the Update Process

- As we have learned, new service workers have to wait until the old one goes away before they are active in the browser. Let's do something better. We will include an update notification for the user.
- As we have seen, when a service worker is registered, it returns a promise.
- The promise "fulfills with a service worker registration object," which can then be used to act on the registration, like `reg.unregister();` and `reg.update();`.
- We will also get three properties:

  ```javascript
  reg.installing;
  reg.waiting;
  reg.active;
  ```

- We can also operate on the service workers themselves.

  ```javascript
  var sw = reg.installing;
  console.log(sw.state); // ...logs "installing"
  // state can also be:
  // "installed"
  // "activating"
  // "activated"
  // "redundant" means the service worker has been thrown away
  sw.addEventListener('statechange', function() {
    // statechange event created when the service worker changes
  });
  ```

- `navigator.serviceWorker.controller` refers to the service worker controlling the current page.
- We can tell the user about updates whether they are already present, in progress, or will start later.

### 2.23. Quiz: Adding UX Quiz

Git

- Checkout to new branch:

  ```shell
  $ git reset --hard
  $ git checkout origin/task-update-notify
  ```

<details>
  <summary><em>Solution</em></summary>

- Code: For this exercise, we worked with *wittr/public/js/main/IndexController.js*.

  ```javascript
  import PostsView from './views/Posts';
  import ToastsView from './views/Toasts';
  import idb from 'idb';

  export default function IndexController(container) {
    this._container = container;
    this._postsView = new PostsView(this._container);
    this._toastsView = new ToastsView(this._container);
    this._lostConnectionToast = null;
    this._openSocket();
    this._registerServiceWorker();
  }

  IndexController.prototype._registerServiceWorker = function() {
    if (!navigator.serviceWorker) return;

    var indexController = this;

    navigator.serviceWorker.register('/sw.js').then(function(reg) {
      // TODO: if there's no controller, this page wasn't loaded
      // via a service worker, so they're looking at the latest version.
      // In that case, exit early
      if(!navigator.serviceWorker.controller) {
        return;
      }

      // TODO: if there's an updated worker already waiting, call
      // indexController._updateReady()
      if (reg.waiting) {
        indexController._updateReady();
        return;
      }

      // TODO: if there's an updated worker installing, track its
      // progress. If it becomes "installed", call
      // indexController._updateReady()
      if (reg.installing) {
        indexController._trackInstalling(reg.installing);
        return;
      }

      // TODO: otherwise, listen for new installing workers arriving.
      // If one arrives, track its progress.
      // If it becomes "installed", call
      // indexController._updateReady()
      reg.addEventListener('updatefound', function() {
        indexController._trackInstalling(reg.installing);
      });
    });
  };

  IndexController.prototype._trackInstalling = function(worker) {
    var indexController = this;
    // if service worker is installed, notify user
    worker.addEventListener('statechange', function() {
      if (worker.state == 'installed') {
        indexController._updateReady();
      }
    });
  };

  IndexController.prototype._updateReady = function() {
    var toast = this._toastsView.show("New version available", {
      buttons: ['whatever']
    });
  };

  // open a connection to the server for live updates
  IndexController.prototype._openSocket = function() {
    var indexController = this;
    var latestPostDate = this._postsView.getLatestPostDate();

    // create a url pointing to /updates with the ws protocol
    var socketUrl = new URL('/updates', window.location);
    socketUrl.protocol = 'ws';

    if (latestPostDate) {
      socketUrl.search = 'since=' + latestPostDate.valueOf();
    }

    // this is a little hack for the settings page's tests,
    // it isn't needed for Wittr
    socketUrl.search += '&' + location.search.slice(1);

    var ws = new WebSocket(socketUrl.href);

    // add listeners
    ws.addEventListener('open', function() {
      if (indexController._lostConnectionToast) {
        indexController._lostConnectionToast.hide();
      }
    });

    ws.addEventListener('message', function(event) {
      requestAnimationFrame(function() {
        indexController._onSocketMessage(event.data);
      });
    });

    ws.addEventListener('close', function() {
      // tell the user
      if (!indexController._lostConnectionToast) {
        indexController._lostConnectionToast = indexController._toastsView.show("Unable to connect. Retrying…");
      }

      // try and reconnect in 5 seconds
      setTimeout(function() {
        indexController._openSocket();
      }, 5000);
    });
  };

  // called when the web socket sends message data
  IndexController.prototype._onSocketMessage = function(data) {
    var messages = JSON.parse(data);
    this._postsView.addPosts(messages);
  };
  ```

- After completing the IndexController.js code, make a random change to the service worker in *sw/index.js*:

  ```javascript
  var staticCacheName = 'wittr-static-v2';
  // random change to trigger user notification
  ```

- Refresh the app at [http://localhost:8888/](http://localhost:8888/)
- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "update-notify"
- Got it working!

</details>

### 2.24. Triggering an Update

- Code previewed in intro video:

  ```javascript
  // have new service worker take over right when refresh is pressed
  self.skipWaiting()

  // from a page
  reg.installing.postMessage({foo: 'bar'});

  // in the service worker
  self.addEventListener('message', function(event) {
    event.data; // {foo: 'bar'}
  });

  // when the new service worker has taken over, signal page reload
  navigator.serviceWorker.addEventListener('controllerchange', function() {
    // navigator.serviceWorker.controller has changed
    });
  ```

### 2.25. Quiz: Triggering an Update Quiz

Git

- Checkout to new branch:

  ```shell
  $ git reset --hard
  $ git checkout origin/task-update-reload
  ```

<details>
  <summary><em>Solution</em></summary>

- Code:
- *wittr/public/js/main/IndexController.js*

  ```javascript
  import PostsView from './views/Posts';
  import ToastsView from './views/Toasts';
  import idb from 'idb';

  export default function IndexController(container) {
    this._container = container;
    this._postsView = new PostsView(this._container);
    this._toastsView = new ToastsView(this._container);
    this._lostConnectionToast = null;
    this._openSocket();
    this._registerServiceWorker();
  }

  IndexController.prototype._registerServiceWorker = function() {
    if (!navigator.serviceWorker) return;

    var indexController = this;

    navigator.serviceWorker.register('/sw.js').then(function(reg) {
      if (!navigator.serviceWorker.controller) {
        return;
      }

      if (reg.waiting) {
        indexController._updateReady(reg.waiting);
        return;
      }

      if (reg.installing) {
        indexController._trackInstalling(reg.installing);
        return;
      }

      reg.addEventListener('updatefound', function() {
        indexController._trackInstalling(reg.installing);
      });
    });

    // TODO: listen for the controlling service worker changing
    // and reload the page
    navigator.serviceWorker.addEventListener('controllerchange', function() {
      window.location.reload();
    });
  };

  IndexController.prototype._trackInstalling = function(worker) {
    var indexController = this;
    worker.addEventListener('statechange', function() {
      if (worker.state == 'installed') {
        indexController._updateReady(worker);
      }
    });
  };

  IndexController.prototype._updateReady = function(worker) {
    var toast = this._toastsView.show("New version available", {
      buttons: ['refresh', 'dismiss']
    });

    toast.answer.then(function(answer) {
      if (answer != 'refresh') return;
      // TODO: tell the service worker to skipWaiting
      worker.postMessage({action: 'skipWaiting'});
    });
  };

  // open a connection to the server for live updates
  IndexController.prototype._openSocket = function() {
    var indexController = this;
    var latestPostDate = this._postsView.getLatestPostDate();

    // create a url pointing to /updates with the ws protocol
    var socketUrl = new URL('/updates', window.location);
    socketUrl.protocol = 'ws';

    if (latestPostDate) {
      socketUrl.search = 'since=' + latestPostDate.valueOf();
    }

    // this is a little hack for the settings page's tests,
    // it isn't needed for Wittr
    socketUrl.search += '&' + location.search.slice(1);

    var ws = new WebSocket(socketUrl.href);

    // add listeners
    ws.addEventListener('open', function() {
      if (indexController._lostConnectionToast) {
        indexController._lostConnectionToast.hide();
      }
    });

    ws.addEventListener('message', function(event) {
      requestAnimationFrame(function() {
        indexController._onSocketMessage(event.data);
      });
    });

    ws.addEventListener('close', function() {
      // tell the user
      if (!indexController._lostConnectionToast) {
        indexController._lostConnectionToast = indexController._toastsView.show("Unable to connect. Retrying…");
      }

      // try and reconnect in 5 seconds
      setTimeout(function() {
        indexController._openSocket();
      }, 5000);
    });
  };

  // called when the web socket sends message data
  IndexController.prototype._onSocketMessage = function(data) {
    var messages = JSON.parse(data);
    this._postsView.addPosts(messages);
  };
  ```

- *sw/index.js*

  ```javascript
  // TODO: listen for the "message" event, and call
  // skipWaiting if you get the appropriate message
  self.addEventListener('message', function(event) {
    if (event.data.action == 'skipWaiting') {
      self.skipWaiting();
    }
  });
  ```

- Again, after completing the IndexController.js code, make a random change to the service worker in *sw/index.js*:

  ```javascript
  var staticCacheName = 'wittr-static-v2';
  // another random change to trigger user notification
  ```

- Refresh the app at [http://localhost:8888/](http://localhost:8888/)
- As before, you will see a notification that the app has changed, but now there is an option to refresh the page. Don't need to refresh again, we'll do this in the next step.
- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "update-reload"
- You then have eight seconds to refresh.
- Jake mentions SVGOMG for SVG compression.

</details>

#### Goals after 2.25

- ~~Unobtrusive app updates~~
- ~~Get the user onto the latest version~~
- Continually update cache of posts
- Cache photos
- Cache avatars

### 2.26. Quiz: Caching the Page Skeleton

Git

- Checkout to new branch:

  ```shell
  $ git reset --hard
  $ git checkout origin/task-page-skeleton
  ```

<details>
  <summary><em>Solution</em></summary>

- Code:
- In the service worker *sw/index.js*, cache `/skeleton` instead of the root page, and respond to requests for the root page with `/skeleton` instead:

  ```javascript
  var staticCacheName = 'wittr-static-v4';

  self.addEventListener('install', function(event) {
    // TODO: cache /skeleton rather than the root page

    event.waitUntil(
      caches.open(staticCacheName).then(function(cache) {
        return cache.addAll([
          '/skeleton',
          'js/main.js',
          'css/main.css',
          'imgs/icon.png',
          'https://fonts.gstatic.com/s/roboto/v15/2UX7WLTfW3W8TclTUvlFyQ.woff',
          'https://fonts.gstatic.com/s/roboto/v15/d-6IYplOFocCacKzxwXSOD8E0i7KZn-EPnyo3HZu7kw.woff'
        ]);
      })
    );
  });

  self.addEventListener('activate', function(event) {
    event.waitUntil(
      caches.keys().then(function(cacheNames) {
        return Promise.all(
          cacheNames.filter(function(cacheName) {
            return cacheName.startsWith('wittr-') &&
                   cacheName != staticCacheName;
          }).map(function(cacheName) {
            return caches.delete(cacheName);
          })
        );
      })
    );
  });

  self.addEventListener('fetch', function(event) {
    // TODO: respond to requests for the root page with
    // the page skeleton from the cache
    // note that we wrote URL three different ways in the line below
    var requestUrl = new URL(event.request.url);

    if (requestUrl.origin === location.origin) {
      if (requestUrl.pathname === '/') {
        event.respondWith(caches.match('/skeleton'));
        return;
      }
    }

    event.respondWith(
      caches.match(event.request).then(function(response) {
        return response || fetch(event.request);
      })
    );
  });

  self.addEventListener('message', function(event) {
    if (event.data.action === 'skipWaiting') {
      self.skipWaiting();
    }
  });
  ```

- Refresh the app at [http://localhost:8888/](http://localhost:8888/) and you will now need to also click "REFRESH" in the popup.
- Test on settings page at [http://localhost:8889/](http://localhost:8889/) with "serve-skeleton".

</details>

Next we will use "one of the web's most hated APIs," `IndexedDB`, and "tame" it to use the good aspects "without getting burned."

[(Back to top)](#top)

## Lesson feedback

Long lesson, but very informative.

I would encourage students to track their code and take notes in a separate Markdown file. It's very easy to lose data with all the git resets.

[Next lesson](offline-3-indexeddb.md)

[Previous lesson](offline-1-benefits.md)

[(Back to top)](#top)