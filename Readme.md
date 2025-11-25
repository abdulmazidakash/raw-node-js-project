# 🚀 Raw Node.js + TypeScript Starter

This project is a **minimal Node.js + TypeScript setup**, created manually (no framework).  
I made this README mainly as a **note for my future self** so I don’t forget the setup steps. 😉

---

## 📁 Project Structure

```bash
my-project/
├── node_modules/
├── src/
│   └── index.ts
├── dist/            # compiled JS (after build)
├── package.json
├── tsconfig.json
└── README.md
````

* All **TypeScript source code** lives in `src/`
* All **compiled JavaScript** will go to `dist/` after running `npm run build`

---

## 1️⃣ Initialize the Project

### Step 1: Create folder & go inside

```bash
mkdir my-typescript-project
cd my-typescript-project
```

### Step 2: Initialize `package.json`

```bash
npm init -y
```

* Creates a default `package.json`.
* `-y` ➝ auto-accept all default options.

> 💬 *Bangla meaning:*
> `npm init -y` দিলে প্রজেক্টের basic config (`package.json`) auto তৈরি হয়।

---

## 2️⃣ Install TypeScript & Dev Tools

```bash
npm install --save-dev typescript ts-node ts-node-dev @types/node
```

### What these do:

* **typescript** → TypeScript compiler (`tsc`)
* **ts-node** → Directly run `.ts` files (without manual build)
* **ts-node-dev** → Like `nodemon` for TypeScript (auto restart on changes)
* **@types/node** → Type definitions for Node (`fs`, `http`, `process`, etc.)

> 💬 *Bangla:* এগুলো সব dev dependencies – development সময়ে দরকার, production এ সাধারনত compiled JS চলে।

---

## 3️⃣ Create & Configure `tsconfig.json`

Generate default config:

```bash
npx tsc --init
```

Then update `tsconfig.json` like this (simple Node setup):

```jsonc
{
  "compilerOptions": {
    "target": "esnext",          // output JS version
    "module": "commonjs",        // Node.js module system
    "rootDir": "./src",          // where TS files live
    "outDir": "./dist",          // where compiled JS will go
    "strict": true,              // enable strict type checking
    "esModuleInterop": true,     // easier import of commonjs modules
    "skipLibCheck": true,
    "types": ["node"],
    "moduleResolution": "node"
  }
}
```

> 💬 *Bangla summary:*
>
> * `rootDir` → সব `.ts` ফাইল `src` ফোল্ডারে
> * `outDir` → compiled `.js` `dist` ফোল্ডারে
> * `strict: true` → বেশি কড়াকড়ি টাইপ চেক, তাই bug কম।

---

## 4️⃣ Create `src` Folder & Example File

```bash
mkdir src
```

Create `src/index.ts`:

```ts
// src/index.ts

const greet = (name: string): string => {
  return `Hello, ${name}!`;
};

console.log(greet('Akash'));
```

---

## 5️⃣ Setup NPM Scripts

Edit `package.json` and add these scripts:

```jsonc
{
  "scripts": {
    "dev": "ts-node-dev --respawn --transpile-only ./src/index.ts",
    "build": "tsc",
    "start": "node ./dist/index.js"
  }
}
```

### Script meanings

* `npm run dev` ➝ Run TypeScript directly with auto-restart (development mode)
* `npm run build` ➝ Compile TypeScript to JavaScript (output in `dist/`)
* `npm start` ➝ Run compiled JS from `dist/`

> 💬 *Bangla:*
>
> * `dev` → development সময় দ্রুত কাজ করার জন্য
> * `build` → final JS বানানো
> * `start` → compiled JS চালানো

---

## 6️⃣ Run the Project

### 🔹 Development mode

```bash
npm run dev
```

Expected console output:

```bash
Hello, Akash!
```

### 🔹 Build & run compiled JS

```bash
npm run build
npm start
```

Same output, but now running from `dist/index.js`.

---

## 7️⃣ Quick Setup Checklist ✅ (for Future Me)

Whenever I start a **new raw Node + TypeScript project**, do this:

1. `mkdir project-name && cd project-name`
2. `npm init -y`
3. `npm install -D typescript ts-node ts-node-dev @types/node`
4. `npx tsc --init`
5. Set `rootDir: "./src"` and `outDir: "./dist"` in `tsconfig.json`
6. `mkdir src` and create `src/index.ts`
7. Add scripts in `package.json`:

   * `"dev": "ts-node-dev --respawn --transpile-only ./src/index.ts"`
   * `"build": "tsc"`
   * `"start": "node ./dist/index.js"`
8. Run `npm run dev` and start coding 🚀

---

## ℹ️ Notes

* This setup is for **raw Node.js (no Express)** with TypeScript.
* For bigger apps, I can later add:

  * `eslint`, `prettier`, `husky` (linting & formatting)
  * testing tools like `jest` or `vitest`


