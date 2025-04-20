
## 🧱 Modern Vite + React + Tailwind + ShadCN Setup Guide

---

### ✅ 1. Initialize the Vite Project

```bash
npm create vite@latest
```

- Choose `React` and `JavaScript` (for TypeScript use documentation process)
    
- Go to the project folder:

```bash
cd your-project-name
```

### ✅ 2. Install Dependencies

```bash
npm install
```

---

## 🎨 TailwindCSS Setup

### ✅ 3. Install Tailwind and Vite Plugin

```bash
npm install tailwindcss @tailwindcss/vite
```

### ✅ 4. (Optional) Install `tw-animate-css` for animation utility support

```bash
npm install tw-animate-css
```

---

### ✅ 5. Configure Tailwind in `index.css`

Open `src/index.css`, **remove everything** and replace with:

```css
@import "tailwindcss";
```


---

## 🧠 Path Aliases with `@`

### ✅ 6. Create or edit `jsconfig.json` (for JavaScript projects)

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

For **TypeScript projects**, use `tsconfig.json` instead.

---

### ✅ 7. Install Node Types for Vite config and better IntelliSense

```bash
npm install -D @types/node
```

---

### ✅ 8. Replace `vite.config.js` with the following:

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";
import { fileURLToPath } from "url";
import tailwindcss from "@tailwindcss/vite";

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

export default defineConfig({
  plugins: [react(), tailwindcss()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

---

## ✨ ShadCN UI Integration

### ✅ 9. Initialize ShadCN

```bash
npx shadcn@latest init
```

- Choose your **base color** (e.g., `neutral`, `blue`, etc.)

This will add needed things in main css file... You can check and customize color according to your choice.

Now `shadcn/ui` will be available for use with beautifully pre-built components.

---

## 🎉 Done! You Can Now:

- Use `@/components/Button` and similar aliases
    
- Use Tailwind utilities
    
- Use ShadCN components out-of-the-box
    
- Build beautiful and scalable UI with clean structure


---



# 🌓 Theme Switching with shadcn/ui (React JSX)

This guide helps you integrate **dark/light mode switching** in your React (JSX) project using `shadcn/ui`.

---

## 🛠️ Prerequisites

- React project (JSX)
    
- Installed `shadcn/ui` 
    
- Proper folder structure (`@/components/` path alias setup) (Read from beginning for this)


---

## 1. 📁 Create Theme Provider

Create a new file:  
`src/components/theme-provider.jsx`

Copy the **ThemeProvider**(theme-provider) file content from the repo .  
Ensure you're copying the **JSX version** (or convert from TSX if needed).

---

## 2. 💡 Wrap App in ThemeProvider

Open your `App.jsx` file and wrap the root component with the `ThemeProvider`:

```jsx
import { ThemeProvider } from "@/components/theme-provider"

function App() {
  return (
    <ThemeProvider defaultTheme="dark" storageKey="vite-ui-theme">
      {/* Replace with your routes or layout */}
      {children}
    </ThemeProvider>
  )
}

export default App
```

> ✅ Replace `{children}` with your actual components or routes (e.g., `<Router />`).

---

## 3. 🎛️ Create Theme Switcher Component

You can design your own **Theme Switch** component, or use the provided example.

### ✅ Example: `ThemeChange.jsx`

Create a component to toggle theme:  
`src/components/ThemeChange.jsx`
 

Here is an [example]([ThemeChange/src/components/ThemeChange.jsx at main · Mutiur03/ThemeChange](https://github.com/Mutiur03/ThemeChange/blob/main/src/components/ThemeChange.jsx))

Then add this component where needed.

---
## 4. Add this script in index.html file to prevent any glitch

```html
<script>
      (function () {
        try {
          const theme = localStorage.getItem("vite-ui-theme");
          const prefersDark = window.matchMedia(
            "(prefers-color-scheme: dark)"
          ).matches;
          const resolved =
            theme === "dark" || (!theme && prefersDark)
              ? "dark"
              : theme === "light"
              ? "light"
              : prefersDark
              ? "dark"
              : "light";
          document.documentElement.classList.add(resolved);
        } catch (_) {}
      })();
</script>
```
---

## 🧪 Final Check

- ✅ Theme toggles between light/dark
    
- ✅ Stored in local storage with key `vite-ui-theme`
    
- ✅ Works across reloads and pages

