# `@swc/plugin-styled-jsx` SVG data-uri transpilation issue

This repo contains a minimal reproduction of a bug in `@swc/plugin-styled-jsx`'s transpilation of
url-encoded SVG data-uris.

## Reproduction

(Tested using Node 20.15)

```
npm install
npm run build
```

**Expected:**

`dist/src/index.js` should contain a valid transpilation including the full url-encoded SVG from `src/index.tsx`.

**Actual:**

The SVG is truncated after the `xmlns`'s protocol:

```js
import _JSXStyle from "styled-jsx/style";
import React from "react";
export var MyComponent = function() {
    return /*#__PURE__*/ React.createElement(React.Fragment, null, /*#__PURE__*/ React.createElement("div", {
        className: "jsx-dc192c4e34fe1865"
    }), /*#__PURE__*/ React.createElement(_JSXStyle, {
        id: "dc192c4e34fe1865"
    }, "div.jsx-dc192c4e34fe1865{background-image:url(\"data:image/svg+xml,%3Csvg stroke='currentColor' fill='currentColor' stroke-width='0' viewBox='0 0 24 24' height='1em' width='1em' xmlns='http:\n}\n\n)}"));
};
```
