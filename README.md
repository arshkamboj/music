# music

A music player web application using Vue and Firebase.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```

### Run End-to-End Tests with [Cypress](https://www.cypress.io/)

```sh
npm run test:e2e:dev
```

This runs the end-to-end tests against the Vite development server.
It is much faster than the production build.

But it's still recommended to test the production build with `test:e2e` before deploying (e.g. in CI environments):

```sh
npm run build
npm run test:e2e
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

Backend Documentation (Firebase)
Go to your firebase console and create a new project.
Create a new web project.
Make sure to copy and paste the configuration into src/includes/firebase.js.
Go to the Authentication page and click on the Sign-in method tab, enable Email/Password login.
Go to the Firestore Database page and click on the rules tab, enter the following rules:

```sh
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
      match /{document=**} {
          allow read: if true;
          allow write: if request.auth.uid == resource.data.uid;
          allow create: if request.auth.uid != null;
          allow delete: if request.auth.uid == resource.data.uid;
      }
  }
}
```

Go to the Sorage page and click on the Rules page, enter the following rules:

```sh
  rules_version = '2';
  service firebase.storage {
      match /b/{bucket}/o {
          match /{allPaths=\*_} {
              allow read: if true;
              allow write: if request.auth != null &&
              request.resource.contentType == "audio/mpeg" &&
              request.resource.size < 10 _ 1024 \* 1024;
              allow delete: if request.auth != null;
          }
      }
  }
```
