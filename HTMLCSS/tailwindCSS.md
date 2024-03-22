# Tailwind

Utility-First를 지향하는 **CSS 프레임워크**





## Tailwind setting

```jsx
1) install tailwind

npm install -D tailwindcss
npx tailwindcss init

2)Configure path
# /tailwind.config.js

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js,vue,ts}"],
  theme: {
    extend: {},
  },
  plugins: [],
}

3)Add the Tailwind directives to your CSS
# /src/input.css
@tailwind base;
@tailwind components;
@tailwind utilities;

4)main.ts 에 import 하기
import './input.css'

5)Start the Tailwind CLI build process

npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch
```

npx tailwindcss -i ./src/index.css -o ./dist/output.css --watch

## VITE tailwindcss 설치

https://tailwindcss.com/docs/guides/vite#vue

## headlessUI

```
npm install @headlessui/vue
```

## HeroIcons

**`npm i @vue-hero-icons/outline`**

```
npm install @vue-hero-icons/solid
npm install @heroicons/vue
```