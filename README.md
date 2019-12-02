Quasar Firebase Messaging App Extension
===

# Install
```bash
yarn add firebase
yarn add https://github.com/motia/quasar-app-extension-firebase-messaging
quasar ext invoke firebase-messaging
```

# Setup
Create a file named `firebase-messaging-sw.js` in `src-pwa`
The package will concatenate the firebase imports at its start

```js
firebase.initializeApp({...});

const messaging = firebase.messaging();

messaging.setBackgroundMessageHandler(function(payload) {
  console.log('[firebase-messaging-sw.js] Received background message ', payload);
  // Customize notification here
  const notificationTitle = 'Background Message Title';
  const notificationOptions = {
    body: 'Background Message body.',
    icon: '/firebase-logo.png'
  };

  return self.registration.showNotification(notificationTitle,
    notificationOptions);
});
```

Also, make the entry `firebase-messaging-sw.js` the entry service worker for your pwa
```js
// replace line
register(process.env.SERVICE_WORKER_FILE, {
--->
// by
register('firebase-messaging-sw.js', {
```
