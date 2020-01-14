# Chrome Extension Starter Kit

## Setup Developement

1. Download the chrome extension starter kit

2. Install type hinting dependencies

```
npm install
```

4. Go to chrome://extensions in the browser

5. Turn on developer mode in the top right of the screen.

6. Click on load unpacked extension

## Chrome Extensions Snippets

### How to register your right click icons

```
var contextMenuItem = {
  id: 'spendMoney',
  title: 'SpendMoney',
  contexts: ['selection']
};

// This should only happen once
chrome.runtime.onInstalled.addListener(function() {
  chrome.contextMenus.create(contextMenuItem);
});
```

## How to respond to your own right click icon events

```
chrome.contextMenus.onClicked.addListener(function(clickedData) {
  if (clickedData.menuItemId == 'spendMoney' && clickedData.selectionText) {
      // Notice the id spend Money above
  }
});
```

### How to store data in for later

```
chrome.storage.sync.set({ example: data }, function() { });
```

### How to fetch data you stored

```
chrome.storage.sync.get(['example1', 'exampl2'], function(ex) { });
```

### How to send a simple notification

```
var notifOptions = {
    type: 'basic',
    iconUrl: 'icon48.png',
    title: 'Example!',
    message: 'Example Message!'
};
chrome.notifications.create(
    'limitNotif' + new Date().getTime(), // Id must be unique for every notification
    notifOptions
);
```

### How to register a content script

```
"content_scripts": [
    {
      "js": ["content.js"],
      "exclude_matches": ["*://*.youtube.com/watch*"],
      "matches": ["https://*.youtube.com/*"],
      "run_at": "document_end"
    }
  ],
```

### How Send Message from background script to content script

```
chrome.tabs.query({ active: true, currentWindow: true }, function(tabs) {
    chrome.tabs.sendMessage(tabs[0].id, {
      src: clickedData.srcUrl,
      type: 'replace_image'
    });
});
```

### How to recieve a message from background script to the content script

```
chrome.runtime.onMessage.addListener(function(message, sender, reply) { });
```

## Packing Chrome Extension

- Delete node_modules folder we are using it for type hinting only.


## Image Attribution

Icons made by <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon"> www.flaticon.com</a>
