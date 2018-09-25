# PWA Reference
## Lifecycle methods
### On index.html load :memo:
- Load app.js or main javascript file which registers the service worker (usually sw.js)
```javascript
if ('serviceWorker' in navigator) {
  // service worker is supported
  navigator.serviceWorker
    // path to service worker main file
    .register('/sw.js')
    .then(() => 
      console.log('service worker registered')
    )
}
```
- First the service worker installs and then emits the install event so that we can listen to it for caching assets
- The service worker is accessed using the `self` keyword in the service worker file
```javascript
self.addEventListener('install', event => {
  // here we can add our main files
  // to the static cache
})
```
- After installation the service worker activates, not necessarily right after installation depending if a previous version of the service worker was present. After activation, the service worker controls all the pages of the scope
```javascript
self.addEventListener('activate', event => {
 // the ideal place to clean up old cache
 // this return is always required else the
 // activate event will behave unexpectedly
 return self.clients.claim()
})
```
- Fetch event fires on a fetch request of a resource (like an html, css, js file)
- Idle event when the service worker has nothng to do
- Terminated event when the service worker is unregistered
- To unregister a service worker we have to call the following method
```javascript
function unregister() {
  if ('serviceWorker' in navigator) {
    navigator.
    serviceWorker.
    getRegistrations().then(resgistrations => {
      for (reg of resgistrations)
        reg.unregister()
    })
  }
}
```
#### _Note:_ All the service worker events callback parameter have a method called `waitUntil` method which helps us perform any action such as _opening a cache_, _deleting the cache_ etc.
```javascript
self.addEventListener(event => {
  event.waitUntil(/* receives a promise */)
})
```
[Browser support for service Workers](https://caniuse.com/#feat=serviceworkers)
---
## Cache API
### To save static assets :memo:
- Access the Cache API in the service worker file using the `caches` object
- [Cache API Docs](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
- In the install lifecycle, open the cache by accessing the cache api using the `open` method
```javascript
caches.open('your-cache-name').then(cache => {
  // add all static assets to the cache
  // addAll method accepts an array
  return cache.addAll(urls)
})
```
- To access the caches of the current website, we use `caches.keys()` method which returns a Promise that resolves to the list of keys
- We can use dynamic caching to cache the routes that appear dynamically so we don't need to cache everything on install
### Dynamic Caching of Routes
- Strategy: Cache with Network Fallback (not good if you want to serve latest content)
- Strategy: Cache only request serve (also not good for internet connection -> only used for selected assets)
- Strategy: Network only which is by default and not good for offline use
- Strategy: Netwrk with Cache Fallback (the best use case for offline support and fetching latest from the network). Downside is not knowing when fetch fails, and so the cache will be available after the network fails, which will be bad ux
- Strategy: Cache then Network ->First fetch from cache, then get the latest from the network and override from cache. If not available, we still have the cache (the most powerful strategy)
#### _Note:_ We cannot store post requests in the cache API
---
## Indexed DB
### Save dynamic data
- Key-Value transactional database
- Asynchronous access
- Database => Object Store => Object
- [Browser Support for IndexedDB](https://caniuse.com/#feat=indexeddb)
### Caching Strategies
- We can use transactions for all types of requests especially json data
- Images and other files use dynamic caching i.e. the `caches` API
- The main difference between dynamic caching of request and caching dynamic data is the dynamic caching caches the images and new routes, while caching dynamic data means caching API responses
- [IDB to make IndexedDB Promise Friendly](https://github.com/jakearchibald/idb)
- [Alternative to IDB: Dexie](http://dexie.org/)
---
### Background Sync
- Background Sync is used if a user performs a POST request offline and we want to later save that data to the db when the user goes online
- The BackgroundSync object resides in the window object
- [Browser Support](https://caniuse.com/#feat=background-sync)
- We have to check both for Service Worker as well as Background Sync in the following way
```javascript
  if ('serviceWorker' in navigator 
    && 'BackgroundSync' in window) {
    // code goes here
  }
```
- Background Sync can be triggered on an event i.e. A form submit event
- Then we have to register the sync event describing it with a name on what operation we are performing
```javascript
 navigator.serviceWorker.ready.then(sw => {
  // perform async operation
  // then in promise or callback execute
  return sw.sync.register('my-sync-event')
 })
```
- In the above code we have registered a sync event with a given name by which we will access the sync event in the service worker file
#### *Note:* It is good practice to provide a fallback i.e. perform the API request in the case BackgroundSync is not supported
- In the service worker, we have to add an event listener to the sync event specifying that any sync event registered will be obtained here
- This event has a _tag_ property that specifies which event is loaded. This is the same text we specified in the __register__ method
- When we receive this event, we will perform our API request specifying the fetch call to be made
```javascript
if (event.tag === 'my-sync-event') {
  // check if it is the event we registered
  // perform our API call here
}
```
- Periodic Sync is a feature yet to come in browsers. This feature enables the app to load the new data in the background, where the service worker will register the periodic sync task and then the latest data fetched from the servcer will be loaded in the background speeding up app load time
- We can pass a schedule, which triggers the `periodicsync` event at a specific interval eg. 1 hour, 1 day etc.
- Periodic sync is not about solving offline issues, its about making the app fetch the latest data in the background thereby reducing app load time
- [Background Sync Introduction](https://developers.google.com/web/updates/2015/12/background-sync)
- [In-Depth Article on Background Sync](https://ponyfoo.com/articles/backgroundsync)
---
### Push Notifications
- The main use-case of Push Notifications is _to drive user_ engagement i.e. Show up even if App (and Browser) is closed
- To give a more mobile-app like experience
![Push Notification Working](/:storage/0.ed3wo6qgt6p.png)
- No Push Event or Service Worker is needed to display notifications, they can be triggered by the browser
- [Push API Browser Support](https://caniuse.com/#feat=push-api)
- To enable notifications, we need to ask the user for permission so that we can send normal as well as push notifications
```javascript
if ('Notification' in window) {
  // ask user for permission
  Notification.requestPermission(result => {
    // result === granted
    // means you have access
  })
}
```
- The user if clicks on deny, then we can never ask for permissions again
- The notification can be clicked by the user. This can happen even when the _app is closed_ and so we have to listen for this event in the service worker
```javascript
self.addEventListener('notificationclick', event => {
  const notification = event.notification
  const action = event.action
  // event.action contains the action performed
  // by the user
})
self.addEventListener('notificationclose', event => {
  // when notification is swiped by the user
  // on mobile devices
  console.log('Notification was closed')
})
```
- The service worker has an object called `pushManager` which has a method called `getSubscription` which when called returns a promise that resolves to the subscription of that device. Each browser and device spawns a new service worker so event if we open our app on a second browser in the same device a new scope and thus a new subscription is obtained
- The user has no way of knowing that we have sent the push notification. So anyone who knows our backend endpoint for push notifications can send notifications to users on our behalf
- For this, we use VAPID, a combination of public and private keys made using jwt and that helps in identifying that the notification has come from our server
- [Using VAPID with Web Push](https://blog.mozilla.org/services/2016/04/04/using-vapid-with-webpush/)
#### *Note:* Always update service workers but never unregister them because if unregistered, the subscription key and the push notification subscription all become invalid. This means that do not unregister service workers.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1NTc1MTQwMl19
-->