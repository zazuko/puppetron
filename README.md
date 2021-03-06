# <img src="assets/logo.png" width="400" alt="Puppetron">

> [Puppeteer](https://github.com/GoogleChrome/puppeteer)-based rendering solution.
> Puppeteer is a Node library which provides a high-level API to control [headless](https://developers.google.com/web/updates/2017/04/headless-chrome) Chrome or Chromium.


This is just a demo site of what cool things `Puppeteer` can do.

Please check out what [Puppeteer](https://github.com/GoogleChrome/puppeteer) can do for your own use case and host on your own servers.

API
---

The API can perform 3 actions:

- [Screenshot](#screenshot) - take a screenshot of the web page
- [Render](#render) - render and serialize a HTML copy of the web page
- [PDF](#pdf) - generate a PDF of the web page

**`URL`** - the URL of the target page, [URI-encoded](https://en.wikipedia.org/wiki/Percent-encoding).

Global parameters:

- `width` - width of viewport/screenshot (default: `1024`)
- `height` - height of viewport/screenshot (default: `768`)
- `navigationTimeout` - timeout in milliseconds before navigation is aborted (default: timeout disabled) 
- `actionTimeout` - timeout in milliseconds before (screenshot|render|pdf) action is aborted (default: `10 * 1000`)

### Screenshot

```
/screenshot?url={URL}
...or
/?url={URL}
```

Parameters:

- `imageType` - screenshot image type, can be either `jpeg` or `png` (default: `png`).
- `jpegQuality` - the quality of the image, between 0-100. Not applicable to `png` images (default: `90`).
- `thumbWidth` - width of thumbnail, respecting aspect ratio (no default, has to be smaller than `width`).
- `fullPage` - takes a screenshot of the full scrollable page, instead of only the viewport (default: `false`).
- `clipSelector` - CSS selector of element to be clipped (no default). E.g.: `.weather-forecast`.

### Render

```
/render?url={URL}
```

Notes:

- `script` tags except `JSON-LD` will be removed
- `link[rel=import]` tags will be removed
- HTML comments will be removed
- `base` tag will be added for loading relative resources
- Elements with absolute paths like `src="/xxx"` or `href="/xxx"` will be prepended with the origin URL.

Parameters: *None*

### PDF

```
/pdf?url={URL}
```

Parameters:

- `format`: Paper format that [Puppeteer supports](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagepdfoptions). E.g.: `Letter`, `Legal`, `A4`, etc. (default: `A4`)
- `landscape`: Paper orientation. (default: `false`)
- `pageRanges`: Paper ranges to print. E.g., `1-5`, `8`, `11-13` (default all pages)

Development
---

### Requirements

- Node.js
- Docker

For local Chromium install:

1. `npm install`
2. `npm start`
3. Load `localhost:3000`

For Docker-based install:

1. `docker build . -t puppetron`
2. `docker run -p 8080:3000 puppetron`
3. Load `localhost:8080`

Credits
---

This is forked from [cheeaun/puppetron](https://github.com/cheeaun/puppetron).
