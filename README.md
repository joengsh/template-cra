# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `yarn start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `yarn test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `yarn build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

## setup

### eslint & prettier

cra default support eslint. All we need to do is to add custom extends and rules.

```bash
yarn add -D eslint-config-prettier eslint-plugin-prettier prettier @joengsh/eslint-config-react @joengsh/prettier-config
```

```javascript
// .prettierrc
'@joengsh/prettier-config';

// package.json or .eslintrc.js
module.exports = {
  extends: ['@joengsh/eslint-config-react/cra'],
};
```

### lint-staged and husky

```bash
yarn add -D husky lint-staged
```

Add lint-staged config

```json
{
  /*...*/
  "scripts": {
    "prepare": "husky install",
    "lint-staged": "lint-staged",
    "format": "prettier --write src/**/*.ts{,x} src/*.ts{,x}",
    "lint": "eslint src/**/*.ts{,x} src/*.ts{,x}",
    "lint-fix": "eslint --fix src/**/*.ts{,x} src/*.ts{,x}"
  },
  "lint-staged": {
    "*.{js,jsx,ts,tsx,css,json,md,mdx}": ["prettier --write", "git add"],
    "*.{js,jsx,ts,tsx}": ["eslint --fix", "git add"]
  }
  /*...*/
}
```

Add pre-commit hook

```bash
npx husky add .husky/pre-commit "yarn lint-staged"
```

### storybook

**downgrade to react 17**

since storybook not fully support react 18, so we need to downgrade to react 17 first. We can manually change the version number in package.json and force install again.

```json
{
  // suggested version
  "dependencies": {
    "@testing-library/react": "^12.1.5",
    "@types/react": "^17.0.0",
    "@types/react-dom": "^17.0.0",
    "react": "^17.0.2",
    "react-dom": "^17.0.2"
  }
}
```

```bash
yarn install --force
```

Then we need to update index.tsx

```typescript
// import ReactDOM from 'react-dom/client';

// const root = ReactDOM.createRoot(document.getElementById('root') as HTMLElement);
// root.render(
//   <React.StrictMode>
//     <App />
//   </React.StrictMode>
// );

import ReactDOM from 'react-dom';

const rootNode = document.getElementById('root');
ReactDOM.render(<App />, rootNode);
```

**install storybook**

```bash
npx storybook init
```
