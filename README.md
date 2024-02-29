# Minimal reproduction of a bug in Remix + Vite + verbatimModuleSyntax

## Changes I made after `npm create vite@latest` with the Remix template

1. In `tsconfig.json`, add `"verbatimModuleSyntax": true`
2. In `_index.tsx` change the `import type` for the `@remix-run/node` import to be inside the braces
   - ❌`import type { MetaFunction } from "@remix-run/node";`
   - ✅`import { type MetaFunction } from "@remix-run/node";`

# Steps to reproduce

1. `npm install`
2. `npm run dev`
3. Go to http://localhost:5173/
4. Open the browser console and see:

```
@remix-run_node.js?v=e931bf82:1543 Uncaught ReferenceError: process is not defined
    at node_modules/util/util.js (@remix-run_node.js?v=e931bf82:1543:5)
    at __require (chunk-WXXH56N5.js?v=4a3845ee:12:50)
    at node_modules/stream-slice/index.js (@remix-run_node.js?v=e931bf82:7121:16)
    at __require (chunk-WXXH56N5.js?v=4a3845ee:12:50)
    at node_modules/@remix-run/node/dist/upload/fileUploadHandler.js (@remix-run_node.js?v=e931bf82:7318:23)
    at __require (chunk-WXXH56N5.js?v=4a3845ee:12:50)
    at node_modules/@remix-run/node/dist/index.js (@remix-run_node.js?v=e931bf82:7506:29)
    at __require (chunk-WXXH56N5.js?v=4a3845ee:12:50)
    at @remix-run_node.js?v=e931bf82:7608:16
```
