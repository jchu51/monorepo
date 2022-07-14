# Monorepos

## What are Monorepos ?

A monorepo is a group of small projects that can be combined to build bigger projects, or they could just be small projects that doesn't know anything about the other projects.

## Steps to setup

1. Create a package `npm init --y`
2. Add `"workspaces": [ "apps/*", "libs/*" ]` into `package.json`
3. Create `apps` folder, and create projects
   1. `npx create-next-app apps/blog --ts --use-npm`
   2. `npm create vite@latest`
4. Update `monorepos` `package.json` name to start with `@monorepo/${name}`
5. `npm install`
6. Create `libs/utils` folder, then `npm init --y`
   1. install `npm i -D tsup -w=@monorepo/utils`
7. update `libs/utils/package.json`
   ```"main": "dist/index.js",
      "module": "dist/index.mjs",
      "tsup": {
        "entry": [
          "src/index.ts"
        ],
        "dts": true,
        "sourcemap": true,
        "format": [
          "esm",
          "cjs"
        ]
      },
      "scripts": {
        "dev": "tsup --watch",
        "build": "tsup"
      },
   ```
8. Create `libs/utils/src/index.ts`
9. `npm i -D -W concurrently`
10. run all the project together, Add to root package script

    ```"scripts": {
    "dev": "concurrently \"npm run dev:utils\" \"npm run dev:blog\" \"npm run dev:dashboard\"",
    "dev:utils": "npm run dev -w @monorepo/utils",
    "dev:blog": "npm run dev -w @monorepo/blog",
    "dev:dashboard": "npm run dev -w @monorepo/dashboard"
    },

    ```

11. share code between a library and applications, install `@monorepo/utils` into other projects `npm i @monorepo/utils --save -w @monorepo/dashboard -w @monorepo/blog;`
12. add `check` and `typecheck` in `package.json`
