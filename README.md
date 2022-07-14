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
5. 
