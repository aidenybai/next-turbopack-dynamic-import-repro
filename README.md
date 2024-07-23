# Bug description

When using `next dev --turbo` with a package that uses `import()` to load a module, the dev server throws an error and the module fails to bundle:

```
Error: Module [project]/node_modules/next/dist/compiled/react/index.js [app-client] (ecmascript, async loader) was instantiated because it was required from module [project]/node_modules/next-turbopack-dynamic-import-repro-package/index.js [app-client] (ecmascript), but the module factory is not available. It might have been deleted in an HMR update.
```

# Repro instructions

I reproduced this by created a local package (`next-turbopack-dynamic-import-repro-package` under `/my-package`). The local package dynamically `import()`s react and react-dom. Then, I packed it with `npm pack` and installed it in the `/my-app` directory. I converted `app/page.tsx` to use the `use client` directive and imported the local package.

To run the app:

```bash
cd my-app
npm install
npm run dev
```

Then open http://localhost:3000 in your browser.
