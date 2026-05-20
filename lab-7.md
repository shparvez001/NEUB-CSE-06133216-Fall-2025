# NEUB CSE-06133216 Fall 2025 Lab 7

In this lab we discuss about Progressive Web Apps(PWA) and How to deploy static sites in github pages.


## What is a Progressive Web App (PWA)?

A **Progressive Web App (PWA)** is a web application that combines the best features of both web applications and mobile applications.

PWAs are:
- Responsive
- Installable
- Fast
- Secure
- Offline-capable

PWAs are built using:
- HTML
- CSS
- JavaScript

### Examples of PWAs
- Twitter Lite
- Airbnb

---

## Key Features of PWAs

| Feature | Description |
|---|---|
| Responsive | Works on desktops, tablets, and mobile devices |
| Offline Support | Uses caching to work without internet |
| Installable | Can be installed like native apps |
| Secure | Requires HTTPS |
| Fast & Reliable | Uses background caching for performance |

---

## Core Components of a PWA

A PWA mainly consists of three components:

1. **Web App Manifest**
   - Defines app metadata
   - Controls installation behavior

2. **Service Worker**
   - Enables offline support
   - Handles caching and network requests

3. **HTTPS**
   - Required for security
   - Ensures secure communication

4. **Responsive Design**
   - Makes the app usable across devices

---

## Architecture Overview

### PWA Architecture Flow
![PWA Architecture](/PWA.png "PWA Architecture")

- Service Worker intercepts network requests
- Cache API stores assets locally
- Manifest controls app installation behavior

---

## Setting Up a Simple PWA

Barebones setup needs 3 main files:

1. index.html
2. manifest.json
3. service-worker.js

## Example: index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mini PWA</title>
  <link rel="manifest" href="manifest.json">
</head>
<body>
  <h1>My PWA To-Do App</h1>
  <input id="task" placeholder="Enter task">
  <button onclick="addTask()">Add</button>
  <ul id="list"></ul>

  <script>
    function addTask() {
      const task = document.getElementById("task").value;
      if (!task) return;
      const li = document.createElement("li");
      li.textContent = task;
      document.getElementById("list").appendChild(li);
    }

    // Register Service Worker
    if ("serviceWorker" in navigator) {
      navigator.serviceWorker.register("service-worker.js");
    }
  </script>
</body>
</html>
```

## Example: manifest.json
```javascript
{
  "name": "Mini To-Do PWA",
  "short_name": "ToDoApp",
  "start_url": "./index.html",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#2196f3",
  "icons": [
    {
      "src": "icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

## Manifest Properties Overview
| Property | Description | Values |
| --- | --- | --- |
| ``name`` | Full name of the app | String |
| ``short_name`` | Name shown on home screen | String (≤12 chars) |
| ``description`` | App description | String |
| ``start_url`` | Launch URL | URL path |
| ``display`` | Display mode | fullscreen, standalone, minimal-ui, browser |
| ``background_color`` | Splash screen background | Hex color |
| ``theme_color`` | Browser theme color | Hex color |
| ``orientation`` | Screen orientation | portrait, landscape, any |
| ``icons`` | App icons | Array |
| ``categories`` | App categories | Array |
| ``screenshots`` | App screenshots | Array |

Display Modes
```
// fullscreen  -> Uses the entire display area

// standalone -> Looks like a native app without browser UI

// minimal-ui -> Standalone mode with minimal navigation controls

// browser -> Regular browser tab
```

## Service Workers
A Service Worker is a background script that enables advanced features:

* Offline functionality
* Background sync
* Push notifications
* Caching strategies
* Intercepting network requests

## Example: service-worker.js
```javascript
const CACHE_NAME = 'pwa-demo-v1';
const urlsToCache = [
  './',
  './index.html',
  './manifest.json'
];

self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME).then((cache) => {
      return cache.addAll(urlsToCache);
    })
  );
});

self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});
```
## Service Worker Lifecycle
1. Register → Browser registers the service worker
2. Install → Cache required resources
3. Activate → Remove old caches
4. Fetch → Intercept and respond to network requests

## Testing Your PWA
You can test your PWA using:

* Local server (VS Code Live Server, XAMPP)
* GitHub Pages

Steps:
1. Open the app in Chrome/Edge
2. Go to DevTools → Application → Manifest
3. Click Install App
4. Turn off internet → App still works offline

## Advantages of PWAs
* No app store required
* Works offline
* Auto-updates
* Push notifications
* Better user engagement

# Introduction to GitHub Pages
GitHub Pages is a free hosting service for static websites.

Ideal for:
* Portfolios
* Documentation
* Academic sites
* Small apps & demos

## How GitHub Pages Works
* Push your HTML/CSS/JS files to a GitHub repo
* GitHub serves your site at:
https://yourusername.github.io/ 
* Uses the main or gh-pages branch

## Setting Up GitHub Pages
1. reate a GitHub repository
2. Upload your website files
3. Go to Settings → Pages
4. Select branch (main or gh-pages)
5. Save → Your site goes live

## Class Task
* Create any progressive web app as your choice
* Deploy the app using GitHub pages
* Submit the link to GitHub page through google classroom.



**_Important Notes_**

* Grades depend on quality of your app
* All code will be checked for AI-generated content
* If AI-generated code is detected, you will be expelled
