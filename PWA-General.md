## Progressive Web Apps

Features 
1) push notification
2) background sync
3) Access Device camera
4) Install on Homescreen
5) Offline Accessibility
6) Get user location

You enhance your existing web pages to feel and work more like native mobile apps
Be reliable: Load fast and provide offline functionality
Fast : Respond quickly to user actions
Engaging: Feel like a native app

If we unregister Service worker then offline support will be removed.

Service Workers -> JS process running in background.
Caching/Offline Support
Background Sync
Push Notification

Application manifest
Installable on home screen
Responsive Design
Geolocation API
Media API

PWA -> Uses App manifest & Service Workers ( Collection of technologies )

---

### App Manifest

We place it in our root folder.
Add manifest.json in every page.
For SPA -> Only one
For multi-page in each page

Manifest Properties

```JSON
{
  "name":"Sweaty-Activity Tracker",
  "short_name":"Sweaty",
  "start_url":"/index.html",
  "scope":".",
  "display":"standalone",
  "background_color":"#fff",
  "theme_color":"#fff",
  "decsription":"App desc",
  "dir":"ltr",
  "lang":"en-US",
  "orientation":"potrait-primary",
  "icons":[Best fitting icons],
  "related_applications":[{"platform":"android"}]
  
}
```
Display Standalone property will remove the browser view like the url bar and stuff and give native app feeling
Back-color - splashscreen
Theme_color - status bar color
related applications ar url for native applications which user might use

scope . means all pages are part
standalone/fullscreen/minimal-ui/browser
potarit-primary/any.potrait/landscape


As Safari and IE does not support manifest we can add meta tags and link tags in the html file which can give certain basic support for PWA.

---

### Service Workers

Service workers run in the background and listens even if app is closed and are decoupled from the HTML DOM.
They run on the single thread which is different than the thread which runs the traditional JS files loaded by html
Service Workers have certain scope traditionally a domain

Service workers listen to specific events
return a cached asset
show a push notification.

XMLHttpRequest , axios do not trigger the fetch event.

| Event | Source |
| ----- |--------|
| Fetch | Http Request |
| Push Notification | SW Receives push notification |
| Notification Interaction | User intearcts with Notif |
| Background Sync | Internet is restored notify |
| service worker lifecycle | SW Phase Changes |


Service worker will be activated only if no previous instance of service worker is running

index.html -> loads app.js -> registers sw.js -> Installation (emits install event) -> Activation (emits activate event) -> Idle mode -> (terminated / sleeping will activate as soon as event comes in )

The default scope is the folder in which the service worker sits  

we register the service worker in app,js because it is imported in every html file so no matter which route the user visits we can be assured that service worker will be registered.

Service worker are served only with pages served with https

```javascript
if ('serviceWorker' in navigator) {
  //check if browser supports serviceWorker
  navigator.serviceWorker.register('/sw.js').then(function() {
    console.log('Service Worker Registered');
  });
}
```

We do not have access to DOM Events in service worker but we have access to a special set of events which can be used to react when a particular event is emitted.

```
self keyword is used to refer to the service-worker
```


```javascript
self.addEventListener('install', function(event) {
  console.log('Installed service worker ...', event);
});

self.addEventListener('activate', function(event) {
  console.log('Activated service worker ...', event);
  return self.clients.claim();
});

// clients.claim() makes sure that we do not run into any issues while 
// activating

```

SW will activate only if all the tabs of your app are closed and then reloaded because tab might be communicating with old service worker and activating new service worker might break the app.
For development purpose we can skipWaiting using chrome dev tools

Fetch event is triggered when we load js,img,css -> Assets
Fetch can be thought of as a proxy

Install and activate event are emitted from browser while Fetch event is emitted from our web app

we can defer when App Banner will be shown
beforeinstallprompt event listener will be triggered when chrome wants to show the installation prompt

prompt() will prompt the user
and their decision will be stored in the userChoice property.
We can ask for adding app to home screen only once
self.skipWaiting() willl not wait for page to be reloaded

Install event will be used to cache our resources
JS is single threaded.

---

Promise takes a callback function as a parameter having resolve and reject as parameter
we can also return synchronus code in then() and can chain it with another then().

fetch() is an alternative to XMLHTTPRequest() and returns a promise
response.json() will also return promise.

```JSON
fetch(url,options);
options = {
  method:'POST',
  headers:{

},
mode : 'no-cors'
  body:JSON.stringify({ message:'Hello'})
}
```

we cannot use XMLHttpRequest in service worker.
Polyfills are used to support promise and fetch in old legacy browsers.
we need to add promise.js and fetch.js for that.

Fetch event listener in SW can also listen to implict Fetch request like fetching js,css but also listen to API requests we explicitly send.




Explore:Payment Request API


---

## Caching [Offline Access]

Browser has an inbuilt cache which stores your assets but that is managed by browser and we cannot manage it.

In cache we generally store html , css , js , and images. For storing the dynamic content that we fetch from server we use IndexedDB

The Cache API is manged by the Developer.
- Cache API stores Key/Value pairs where Key is the Http Request you want to send and value is the response we get back
 - We need to have sent the Key Http Request atleast once so that we can store the response as value and can use it later when we have to send the same fetch request again and there is no internet connection

- Can be accessed from SW and normal js pages

- We should cache the App Shell -> Static content like toolbars , headers , footers which do not change often. We cache this content when our service worker is installing

- In the SW install event we cache the assets which can then be used when user is navigating to other pages too.

- caches object is used to access the storage of our cache.
- caches.open() tries to open a sub-cache and if not present then creates it and returns a promise.
- In the then callback function we are given a reference to that cache 

- Caching is an asynchronus event so it will return a promise. we have to make sure that install event is not finished util caching is done. because it may happen that page would like to fetch the assest while still we are caching it.
- So to avoid that we use event.waitUntil() which will make sure that caching is finished first and then only we complete the install event.
- Cache.match() and Cache.matchAll() allows us to check whether a key for the given request is present in the cache. matchAll() takes an array.
- Cache.add() and Cache.addAll() is used to first send a request and then cache the response. addAll() takes an Array.
- Cache.keys() gives you the list of keys in the cache.
- Cache.delete() to remove an asset from cache
- In Cache.put() we have to manually set the url as key and the response as value.

### Dynamic Caching

- In Dynamic Caching you have to invoke a fetch event anyways and we want to store the response which are getting.
- We use put method of cache in dynamic caching
- we need to return response after caching it. Response can be consumed only once so we store the clone of response in the cache.


```Javascript
self.addEventListener('fetch', function(event) {
  event.respondWith(
  // Checks if present in the cache
    caches.match(event.request).then(function(response) {
      if (response) {
        return response;
      } else {
      // If not present then fetch from server
        return fetch(event.request).then(function(res) {
    // After fetching from the server add the clone of res to cache    
          return caches.open('dynamic').then(function(cache) {
            cache.put(event.request.url, res.clone());
            // return response back to the requestor
            return res;
          });
        });
      }
    })
  );
});
```

- If we change any of the files we have pre-cached then also our app will serve the old content from the cache. so to avoid that we add a new version to the cache and clean the old cache.
- we clean our cache in the activate event life-cycle
- when we change the cached files we have to add a version in the cache name and delete the previous versions.
- Only if server-worker is changed then only new content will be reflected else content from the cache will be served always.

---

## Advanced Caching

- We can Provide ondemand Caching. E.g If user wants to add an article for reading it later then we can provide caching. we can access cache object from our normal js files as well.

```Javascript
function onSaveButtonClicked(event) {
  console.log('clicked');
  if ('caches' in window) {
    caches.open('user-requested')
      .then(function(cache) {
        cache.add('https://httpbin.org/get');
        cache.add('/src/images/sf-boat.jpg');
      });
  }
}
```

- we can provide offline fallbacksupport i.e if a page is not cached then user will be shown our custom page and maybe we can redirect them to pages which are cached.
```JavaScript
self.addEventListener('fetch', function(event) {
  event.respondWith(
    caches.match(event.request).then(function(response) {
      if (response) {
        return response;
      } else {
        return fetch(event.request)
          .then(function(res) {
            return caches.open(CACHE_DYNAMIC_NAME).then(function(cache) {
              cache.put(event.request.url, res.clone());
              return res;
            });
          })
          .catch(function(err) {
            return caches.open(CACHE_STATIC_NAME).then(function(cache) {
              return cache.match('/offline.html');
            });
          });
      }
    })
  );
});
```

---

## Caching Startegies

1) Cache with Network Fallback : First look in cache if present do not make request else make request
2) Cache Only
3) Network Only
4) Network with cache fallback
5) Cache then network: First we present asset from cache and then try to find updated version then cache. If found then we replace the cache with updated content and then add that new content in cache.
6) For certain assets we want to implement one strategy and for other assets we want another strategy then we can parse the url by using
```Javascript
if(event.request.url.indexOf(url) > -1 ) {
  // First Strategy
}else{
  // Second Strategy
}
```
To check when to serve fallback files we can use the condition 
```
event.request.headers.get('accept').includes('text/html)
```

- If we send a post request and there is no internet connection then we can serve content from the cache but when internet connection is regained then it will not try to make the post request when online for that we need to make use of background sync

- If we unregister service worker then cache will be cleared automatically.

---

## Caching Dynamic Content with Indexed DB

- Indexed DB is used to store dynamic data.
- Indexed DB is a transactional key-value database in the Browser     
- Transactional :- If one action within a transaction fails, none of the actions of that transaction are applied.
- Indexed DB can be accessed Asynchronously. But LocalStorage can be accessed only synchronusly.
- In IndexedDb there can be multiple object stores which hold multiple objects.
- we use idb.js as a wrapper so that we can use indexedDB asynchronously and wrap the logic in a promise.
- importScripts() allows us to use a script in our service-worker.





















<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEzODUyMzYxMl19
-->