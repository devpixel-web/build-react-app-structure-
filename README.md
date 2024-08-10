# Project Configuration Guide

This guide provides detailed explanations of the configuration files used in this project, specifically the TypeScript configuration (`tsconfig.json`) and the Vite configuration (`vite.config.js`). These configurations are essential for setting up the development environment and ensuring a smooth workflow.

## Table of Contents
- TypeScript Configuration (`tsconfig.json`)
   - Explanation of Compiler Options
   - Included Files and References
- Additional TypeScript Configuration (tsconfig.node.json)
   - Explanation of Compiler Options
   - Bundler Mode
   - Linting and Strictness
   - Included Files
- TypeScript Configuration (`tsconfig.app.json`)
   - Explanation of Compiler Options
   - Bundler Mode
   - Linting and Strictness
   - Included Files
- Vite Configuration (`vite.config.js`)
   - Explanation of Configuration
- ESLint Configuration (`.eslintrc.json`)
   - Explanation of Configuration
- NPM Scripts
   - Explanation of Scripts
- Prettier Configuration(`.prettierrc or prettier.config.js`)
   - Explanation of Configuration

---

## TypeScript Configuration (`tsconfig.json`)

This project utilizes TypeScript for type-checking and code reliability. The `tsconfig.json` file defines compiler options and path aliases, allowing for a more efficient and organized codebase.

```json
{
  "compilerOptions": {
    "target": "ESNext", 
    "useDefineForClassFields": true, 
    "lib": ["DOM", "DOM.Iterable", "ESNext"], 
    "allowJs": false, 
    "skipLibCheck": true, 
    "esModuleInterop": false, 
    "allowSyntheticDefaultImports": true, 
    "strict": false, 
    "forceConsistentCasingInFileNames": true, 
    "module": "ESNext", 
    "moduleResolution": "Node", 
    "resolveJsonModule": true, 
    "isolatedModules": true, 
    "noEmit": true, 
    "jsx": "react-jsx", 
    "baseUrl": "./", 
    "paths": {
      "@UI/*": ["src/shared/UI/*"], 
      "@services/*": ["src/app/api/services/*"], 
      "@servicesTypes/*": ["src/app/api/types/*"], 
      "@constants/*": ["src/app/constants/*"], 
      "@app/*": ["src/app/*"], 
      "@store/*": ["src/store/*"], 
      "@shadecn/*": ["src/shadecn/*"], 
      "@components/*": ["src/components/*"], 
      "@assets/*": ["src/assets/*"], 
      "@hooks": ["src/hooks"], 
      "@/*": ["src/*"] 
    }
  },
  "include": ["src"], 
  "references": [
    {
      "path": "./tsconfig.node.json" 
    }
  ]
}
```
## Explanation of Compiler Options
 - `target`: Specifies the ECMAScript version target for the compiled output. ESNext ensures the use of the latest JavaScript features.
useDefineForClassFields: Enforces the ECMAScript standard behavior for class fields.
 - `lib`: Defines the libraries to include in the compilation. Here, we include DOM for browser APIs, DOM.Iterable for iterable DOM collections, and ESNext for the latest JavaScript features.
 - `allowJs`: Disallows JavaScript files from being compiled, ensuring a purely TypeScript codebase.
 - `skipLibCheck`: Skips type checking of declaration files to speed up the compilation process.
 - `esModuleInterop`: Disables interoperability between CommonJS and ES modules, which is often preferred for cleaner module imports.
 - `allowSyntheticDefaultImports`: Allows default imports from modules that may not have a default export.
 - `strict`: Disables strict type-checking options to allow more flexibility in the codebase.
 - `forceConsistentCasingInFileNames`: Enforces consistent casing in file names, preventing issues in case-sensitive file systems.
 - `module`: Specifies the module system for the project. ESNext allows for the use of the latest ES module features.
 - `moduleResolution`: Determines how modules are resolved, using Node.js-style resolution.
 - `resolveJsonModule`: Allows importing of JSON files as modules.
 - `isolatedModules`: Ensures that each file is treated as an isolated module, useful for projects using tools like Babel.
 - `noEmit`: Disables emitting output files; useful when TypeScript is only used for type-checking.
 - `jsx`: Specifies the JSX factory to use. react-jsx is the new JSX transform introduced in React 17.
 - `baseUrl`: Defines the base directory for resolving non-relative module names.
 - `paths`: Provides a set of path aliases to simplify module imports. For example, @UI/* maps to src/shared/UI/*, allowing for cleaner import statements.

## Included Files and References

 - `include`: Specifies the files or directories to include in the compilation. Here, it's set to include everything in the src directory.
 - `references`: Allows TypeScript projects to reference other configurations. This is useful for multi-package or monorepo setups.

---

## Additional TypeScript Configuration (`tsconfig.node.json`)

This section provides an overview of another TypeScript configuration used in this project, highlighting some advanced settings for bundler mode and linting.

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["ES2023"],
    "module": "ESNext",
    "skipLibCheck": true,
    "composite": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": false,
    "isolatedModules": true,
    "moduleDetection": "force",
    "noEmit": false,

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["vite.config.ts"]
}
```

### Explanation of Compiler Options
 - `target:` Specifies the target ECMAScript version for the output. ES2022 is a modern target, ensuring compatibility with the latest JavaScript features.
 - `lib:` Includes the ES2023 library for compiling the code, which provides the latest ECMAScript features.
 - `module:` Specifies the module system to be used, with ESNext allowing the latest module features.
 - `skipLibCheck:` Skips type checking for all declaration files (.d.ts), improving compilation speed.
- `composite:` Enables composite projects, which is useful for projects that use project references.
### Bundler Mode
 - `moduleResolution:`Set to bundler mode, which optimizes module resolution for bundlers like Vite.
 - `allowImportingTsExtensions:` Disallows importing files with .ts extensions, enforcing a cleaner import structure.
 - `isolatedModules:` Ensures each file is treated as an isolated module, useful for tooling like Babel.
 - `moduleDetection:` Forces the detection of modules, ensuring that files are treated as modules even without imports or exports.
 - `noEmit:` Controls whether the compiler emits output files. Here, set to false, indicating that output files will be generated.
Linting and Strictness
 - `strict:` Enables strict type-checking options for better code quality.
 - `noUnusedLocals:` Issues an error if there are any unused local variables.
 - `noUnusedParameters:`Issues an error if there are any unused parameters in functions or methods.
 - `noFallthroughCasesInSwitch:`Ensures that switch-case statements do not fall through, preventing potential bugs.
### Included Files
 - `include:`Specifies that only the vite.config.ts file is included in this particular TypeScript configuration, ensuring targeted compilation.

---

## TypeScript Configuration (`tsconfig.app.json`)

This section provides an overview of the TypeScript configuration used in this project, focusing on the compiler options and settings that are crucial for ensuring code quality and compatibility.

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "isolatedModules": true,
    "moduleDetection": "force",
    "noEmit": true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src"]
}
```

### Explanation of Compiler Options

- **`target:`** Specifies the target ECMAScript version for the output. ES2022 is a modern target, ensuring compatibility with the latest JavaScript features.
- **`useDefineForClassFields:`** Ensures that class fields are defined using the ECMAScript standard behavior. This option ensures that class fields are declared using the `define` semantics introduced in ECMAScript.
- **`lib:`** Includes the ES2023 library for compiling the code, which provides the latest ECMAScript features.
- **`module:`** Specifies the module system to be used, with ESNext allowing the latest module features.
- **`skipLibCheck:`** Skips type checking for all declaration files (.d.ts), improving compilation speed.

### Bundler Mode

- **`moduleResolution:`** Set to bundler mode, which optimizes module resolution for bundlers like Vite.
- **`allowImportingTsExtensions:`** Disallows importing files with .ts extensions, enforcing a cleaner import structure.
- **`isolatedModules:`** Ensures each file is treated as an isolated module, useful for tooling like Babel.
- **`moduleDetection:`** Forces the detection of modules, ensuring that files are treated as modules even without imports or exports.
- **`noEmit:`** Controls whether the compiler emits output files. Here, set to false, indicating that output files will be generated.

### Linting and Strictness

- **`strict:`** Enables strict type-checking options for better code quality.
- **`noUnusedLocals:`** Issues an error if there are any unused local variables.
- **`noUnusedParameters:`** Issues an error if there are any unused parameters in functions or methods.
- **`noFallthroughCasesInSwitch:`** Ensures that switch-case statements do not fall through, preventing potential bugs.

### Included Files

- **`include:`** Specifies that only the `vite.config.ts` file is included in this particular TypeScript configuration, ensuring targeted compilation.

---

## Vite Configuration (vite.config.js)
Vite is used as the build tool and development server for this project. The (`vite.config.js`). file contains important settings for module resolution and plugin integration.

```js 
import path from 'path';
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  resolve: {
    alias: {
      '@UI': path.resolve(__dirname, './src/shared/UI'),
      '@services': path.resolve(__dirname, './src/app/api/services'),
      '@servicesTypes': path.resolve(__dirname, './src/app/api/types'),
      '@constants': path.resolve(__dirname, './src/app/constants'),
      '@app': path.resolve(__dirname, './src/app'),
      '@assets': path.resolve(__dirname, './src/assets'),
      '@components': path.resolve(__dirname, './src/components'),
      '@shadecn': path.resolve(__dirname, './src/shadecn'),
      '@hooks': path.resolve(__dirname, './src/hooks'),
      '@store': path.resolve(__dirname, './src/store'),
      '@': path.resolve(__dirname, './src'),
    },
  },
  plugins: [react()],
});
```
### Explanation of Configuration
 #### resolve.alias:
 Defines custom aliases for directories in your project. This simplifies and organizes imports. For instance:
 - @UI points to `./src/shared/UI.`
 - @services points to `./src/app/api/services.`
 - @components points to `./src/components.`
 #### plugins:
 - The react plugin is included to enable React-specific optimizations and JSX transformation.

---

## ESLint Configuration (`.eslintrc.json`)

This project uses ESLint to maintain code quality and enforce consistent coding standards. Below is the ESLint configuration with detailed explanations for each setting.

```json
{
  "env": {
    "browser": true,          // Enables browser global variables like `window`.
    "es6": true,              // Enables ES6 syntax.
    "node": true              // Enables Node.js global variables like `process`.
  },
  "extends": [
    "eslint:recommended",     // Extends recommended ESLint rules.
    "plugin:react/recommended", // Adds recommended React-specific linting rules.
    "plugin:react-hooks/recommended", // Adds recommended React Hooks linting rules.
    "plugin:@typescript-eslint/eslint-recommended", // Adjusts ESLint's recommended rules for TypeScript.
    "plugin:@typescript-eslint/recommended", // Adds recommended TypeScript-specific linting rules.
    "plugin:import/warnings", // Enables warnings for import/export syntax.
    "plugin:import/typescript", // Adds TypeScript support to the import plugin.
    "prettier"                // Integrates Prettier for code formatting.
  ],
  "parser": "@typescript-eslint/parser", // Uses the TypeScript parser.
  "parserOptions": {
    "ecmaVersion": "latest",   // Specifies the latest ECMAScript version.
    "sourceType": "module",    // Enables ES6 module syntax.
    "ecmaFeatures": {
      "jsx": true              // Enables linting for JSX syntax.
    }
  },
  "plugins": [
    "react",                   // React-specific linting rules.
    "react-refresh",           // Supports fast refresh during development.
    "react-hooks",             // Lints React Hooks rules.
    "import",                  // Lints import/export syntax.
    "@typescript-eslint",      // TypeScript-specific linting rules.
    "prettier"                 // Integrates Prettier for formatting.
  ],
  "rules": {
    "react/jsx-key": "warn",               // Warns when a key is missing in a list of elements.
    "react/prop-types": "off",             // Disables prop-types checking (not needed with TypeScript).
    "react/display-name": "warn",          // Warns if display name is not specified in React components.
    "react/no-children-prop": "warn",      // Warns against passing children as a prop.
    "react/react-in-jsx-scope": "off",     // Disables the need for `React` to be in scope in JSX files.
    "react/button-has-type": "warn",       // Warns when button elements don't specify a type.
    "react-hooks/exhaustive-deps": "off",  // Disables exhaustive dependency checking for React Hooks.
    "react-hooks/rules-of-hooks": "error", // Enforces the rules of React Hooks.
    "@typescript-eslint/no-unused-vars": "warn", // Warns on unused variables.
    "no-case-declarations": "warn",        // Warns when declarations are made in case blocks without brackets.
    "no-console": "warn",                  // Warns on console usage.
    "react-refresh/only-export-components": "warn", // Ensures only components are exported in React files.
    "@typescript-eslint/explicit-function-return-type": "off", // Disables the need for explicit return types in functions.
    "@typescript-eslint/no-explicit-any": "warn", // Warns on the use of `any` type in TypeScript.
    "no-unsafe-optional-chaining": "warn", // Warns on potentially unsafe optional chaining.
    "import/order": [
      "error",
      {
        "groups": ["builtin", "external", "internal", "parent", "sibling"] // Enforces a specific order for import statements.
      }
    ],
    "prettier/prettier": [
      "warn",
      {
        "endOfLine": "auto"    // Ensures consistent line endings.
      }
    ]
  },
  "settings": {
    "react": {
      "version": "detect"      // Automatically detects the version of React to use.
    },
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"] // Specifies file extensions for module resolution.
      }
    }
  }
}
```

---

## ESLint Configuration (`.eslintrc.json`)

This project uses ESLint to maintain code quality and enforce consistent coding standards. Below is the ESLint configuration with detailed explanations for each setting.

```json
{
  "env": {
    "browser": true,          // Enables browser global variables like `window`.
    "es6": true,              // Enables ES6 syntax.
    "node": true              // Enables Node.js global variables like `process`.
  },
  "extends": [
    "eslint:recommended",     // Extends recommended ESLint rules.
    "plugin:react/recommended", // Adds recommended React-specific linting rules.
    "plugin:react-hooks/recommended", // Adds recommended React Hooks linting rules.
    "plugin:@typescript-eslint/eslint-recommended", // Adjusts ESLint's recommended rules for TypeScript.
    "plugin:@typescript-eslint/recommended", // Adds recommended TypeScript-specific linting rules.
    "plugin:import/warnings", // Enables warnings for import/export syntax.
    "plugin:import/typescript", // Adds TypeScript support to the import plugin.
    "prettier"                // Integrates Prettier for code formatting.
  ],
  "parser": "@typescript-eslint/parser", // Uses the TypeScript parser.
  "parserOptions": {
    "ecmaVersion": "latest",   // Specifies the latest ECMAScript version.
    "sourceType": "module",    // Enables ES6 module syntax.
    "ecmaFeatures": {
      "jsx": true              // Enables linting for JSX syntax.
    }
  },
  "plugins": [
    "react",                   // React-specific linting rules.
    "react-refresh",           // Supports fast refresh during development.
    "react-hooks",             // Lints React Hooks rules.
    "import",                  // Lints import/export syntax.
    "@typescript-eslint",      // TypeScript-specific linting rules.
    "prettier"                 // Integrates Prettier for formatting.
  ],
  "rules": {
    "react/jsx-key": "warn",               // Warns when a key is missing in a list of elements.
    "react/prop-types": "off",             // Disables prop-types checking (not needed with TypeScript).
    "react/display-name": "warn",          // Warns if display name is not specified in React components.
    "react/no-children-prop": "warn",      // Warns against passing children as a prop.
    "react/react-in-jsx-scope": "off",     // Disables the need for `React` to be in scope in JSX files.
    "react/button-has-type": "warn",       // Warns when button elements don't specify a type.
    "react-hooks/exhaustive-deps": "off",  // Disables exhaustive dependency checking for React Hooks.
    "react-hooks/rules-of-hooks": "error", // Enforces the rules of React Hooks.
    "@typescript-eslint/no-unused-vars": "warn", // Warns on unused variables.
    "no-case-declarations": "warn",        // Warns when declarations are made in case blocks without brackets.
    "no-console": "warn",                  // Warns on console usage.
    "react-refresh/only-export-components": "warn", // Ensures only components are exported in React files.
    "@typescript-eslint/explicit-function-return-type": "off", // Disables the need for explicit return types in functions.
    "@typescript-eslint/no-explicit-any": "warn", // Warns on the use of `any` type in TypeScript.
    "no-unsafe-optional-chaining": "warn", // Warns on potentially unsafe optional chaining.
    "import/order": [
      "error",
      {
        "groups": ["builtin", "external", "internal", "parent", "sibling"] // Enforces a specific order for import statements.
      }
    ],
    "prettier/prettier": [
      "warn",
      {
        "endOfLine": "auto"    // Ensures consistent line endings.
      }
    ]
  },
  "settings": {
    "react": {
      "version": "detect"      // Automatically detects the version of React to use.
    },
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"] // Specifies file extensions for module resolution.
      }
    }
  }
}
```
### Explanation of Configuration
 - `env:` Defines the environments that the code is expected to run in, enabling global variables specific to those environments.
 - `extends:` Specifies the base set of rules and configurations to extend, providing a foundation of recommended practices for React, TypeScript, and import/export syntax.
 - `parser:` Indicates which parser ESLint should use, in this case, the TypeScript parser to handle .ts and .tsx files.
 - `parserOptions:` Configures how ESLint parses the code, including ECMAScript version, module type, and JSX syntax.
 - `plugins:` Adds additional linting plugins that provide specific rules for React, TypeScript, and code formatting with Prettier.
 - `rules:` Customizes the behavior of individual linting rules, such as warning on missing JSX keys, enforcing import order, and using Prettier for consistent formatting.
 - `settings:`Provides additional configuration for specific plugins, like detecting the React version and resolving module imports.

---

 ## NPM Scripts

This project uses a series of NPM scripts to streamline development, building, and code quality checks. Below is an explanation of each script.

```json
{
  "scripts": {
    "dev": "vite --port=4000 --host",
    "build": "tsc -b && vite build",
    "lint": "eslint . --ext .js,.js,.jsx,.ts,.tsx",
    "format": "prettier-eslint --write \"src/**/*.{js,jsx,ts,tsx}\"",
    "preview": "vite preview"
  }
}
```
### Explanation of Scripts
 - `dev:` Starts the development server using Vite, with the server running on port 4000 and accessible from the local network (--host).
 - `build:` First compiles the TypeScript files (tsc -b), and then bundles the application using Vite for production.
 - `lint:` Runs ESLint across the entire codebase, checking files with extensions .js, .jsx, .ts, and .tsx for any linting issues.
 - `format:` Formats the code in the src directory using Prettier combined with ESLint, ensuring consistent code style across .js, .jsx, .ts, and .tsx files.
 - `preview:` Serves the production build locally to preview how the app will look and behave in production.

  ## Here's an explanation of the Prettier configuration file (`.prettierrc or prettier.config.js`) you provided:

```json
  {
  "arrowParens": "always", // Always include parentheses around arrow function parameters. Example: `(x) => x`.
  "bracketSpacing": true, // Add spaces between brackets in object literals. Example: `{ foo: bar }`.
  "endOfLine": "lf", // Use line feed (LF) as the line ending character. Helps maintain consistency across different operating systems.
  "htmlWhitespaceSensitivity": "css", // Respect the default value of CSS for handling whitespace in HTML.
  "insertPragma": false, // Do not automatically insert a @prettier pragma at the top of files.
  "jsxBracketSameLine": true, // Place the `>` of a multiline JSX element at the end of the last line rather than being on a new line.
  "jsxSingleQuote": false, // Use double quotes instead of single quotes in JSX attributes.
  "printWidth": 100, // Specify the line length that the printer will wrap on. Helps ensure that code stays within a readable width.
  "proseWrap": "always", // Wrap markdown text in the `printWidth` limit.
  "quoteProps": "as-needed", // Only add quotes around object properties when required (e.g., if the property name is not a valid identifier).
  "requirePragma": false, // Do not require a @prettier pragma to format files.
  "semi": true, // Always add a semicolon at the end of statements.
  "singleQuote": true, // Use single quotes instead of double quotes in JavaScript and TypeScript.
  "tabWidth": 2, // Specify the number of spaces per indentation level.
  "trailingComma": "es5", // Print trailing commas wherever possible in ES5 (objects, arrays, etc.).
  "useTabs": false, // Use spaces instead of tabs for indentation.
  "plugins": ["prettier-plugin-tailwindcss"] // Use the Tailwind CSS plugin to sort class names in Tailwind CSS files.
}
```