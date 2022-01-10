### Quick Google Meet Chrome Extension


## Installing and Running

### Procedures:

1. Check if your [Node.js](https://nodejs.org/) version is >= **10.13**.
2. Clone this repository.
3. Run `npm install` to install the dependencies. If you get any authorization issues, try running `sudo npm install`
4. Run `npm start` or `sudo npm start`
5. Load your extension on Chrome following:
   1. Access `chrome://extensions/`
   2. Check `Developer mode`
   3. Click on `Load unpacked extension`
   4. Select the `build` folder.
6. Now you are all set to use the extension.

## Structure

All the extension's code is placed in the `src` folder.

## Features

This is a Chrome Extension to help you to ease the process of Google Meeting creation.
Following are the basic features targeted  around this chrome extension:

1. Allow users to create a new google meet meeting and and allow users to quickly share the link with others.
2. Optimize meeting creation by allowing users to create and share links via keyboard alone.
3. Allow users to choose which email to create a meeting with and cache the first selection for simultaneous meetings.



## Optimization Specification

1. API_KEY and access codes to the google API are supposed to be hidden in a separate file and must not be shared. But for the sake of **convenience and testing** are shared with you.
2. This project can be easily enhanced by adding a feature to open the **newly created link in a new tab**.
3. New features like **adding the attendees and notifying them** can be very easily added as a feature because of the use of Google Calendar Api.
## Webpack auto-reload and HRM

To make your workflow much more efficient this boilerplate uses the [webpack server](https://webpack.github.io/docs/webpack-dev-server.html) to development (started with `npm start`) with auto reload feature that reloads the browser automatically every time that you save some file in your editor.

You can run the dev mode on other port if you want. Just specify the env var `port` like this:

```
$ PORT=6002 npm run start
```

## Content Scripts

Although this boilerplate uses the webpack dev server, it's also prepared to write all your bundles files on the disk at every code change, so you can point, on your extension manifest, to your bundles that you want to use as [content scripts](https://developer.chrome.com/extensions/content_scripts), but you need to exclude these entry points from hot reloading [(why?)](https://github.com/samuelsimoes/chrome-extension-webpack-boilerplate/issues/4#issuecomment-261788690). To do so you need to expose which entry points are content scripts on the `webpack.config.js` using the `chromeExtensionBoilerplate -> notHotReload` config. Look the example below.

Let's say that you want use the `myContentScript` entry point as content script, so on your `webpack.config.js` you will configure the entry point and exclude it from hot reloading, like this:

```js
{
  …
  entry: {
    myContentScript: "./src/js/myContentScript.js"
  },
  chromeExtensionBoilerplate: {
    notHotReload: ["myContentScript"]
  }
  …
}
```

and on your `src/manifest.json`:

```json
{
  "content_scripts": [
    {
      "matches": ["https://www.google.com/*"],
      "js": ["myContentScript.bundle.js"]
    }
  ]
}
```







