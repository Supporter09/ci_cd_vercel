
# Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

# Setting Up a Next.js Project with Jest for Testing

## 1. Install Next.js
Run the following command to create a new Next.js project:
```sh
npx create-next-app@latest
```

## 2. Install Necessary Testing Packages
Install Jest and related packages for testing with the following command:

Using npm:
```sh
npm install -D jest jest-environment-jsdom @testing-library/react @testing-library/dom @testing-library/jest-dom ts-node
```

Using yarn:
```sh
yarn add -D jest jest-environment-jsdom @testing-library/react @testing-library/dom @testing-library/jest-dom ts-node
```

Using pnpm:
```sh
pnpm install -D jest jest-environment-jsdom @testing-library/react @testing-library/dom @testing-library/jest-dom ts-node
```

## 3. Create a Basic Jest Configuration

Using npm:
```sh
npm init jest@latest
```

Using yarn:
```sh
yarn create jest@latest
```

Using pnpm:
```sh
pnpm create jest@latest
```

## 4. Update Jest Configuration for Next.js

Modify `jest.config.js` to use `next/jest` for compatibility with Next.js:

```js
const nextJest = require('next/jest');

/** @type {import('jest').Config} */
const createJestConfig = nextJest({
  // Provide the path to your Next.js app to load next.config.js and .env files in your test environment
  dir: './',
});

// Add any custom config to be passed to Jest
const config = {
  coverageProvider: 'v8',
  testEnvironment: 'jsdom',
  // Add more setup options before each test is run
  // setupFilesAfterEnv: ['<rootDir>/jest.setup.ts'],
};

// Export Jest configuration
module.exports = createJestConfig(config);
```

## 5. Add Jest Setup File

Create a `jest.setup.js` file to configure Jest with additional setup options:

```js
import '@testing-library/jest-dom';
```

## 6. Write Some Tests

Create test files inside the `__tests__` directory, for example:

`__tests__/index.test.js`

```js
import "@testing-library/jest-dom";
import { render, screen } from "@testing-library/react";
import Home from "../src/pages/index";

describe("Home Page", () => {
  it("renders a heading", () => {
    render(<Home />);

    const heading = screen.getByRole("heading", { level: 1 });

    expect(heading).toBeInTheDocument();
  });
});
```

Run tests using:
```bash
npm test
# or
yarn test
# or
pnpm test
