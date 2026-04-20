# Vue-i18n XSS Demo

### Project created with VS Code chat agent

This project demonstrates an XSS vulnerability in `vue-i18n` (include 9.0.0 ⟶ < 9.14.5, and earlier 10/11 minors) when using `v-html` to render translations containing untrusted HTML.

## How the XSS Works

- The app sets a cookie named `secure_token` to simulate a sensitive value (e.g., an auth token).
- The translation for `welcome` contains a `{name}` parameter, which is set to a value that could come from an external API.
- In the demo, `name` is set to a malicious payload:
  ```js
  const name = `<img src=x onerror=alert(document.cookie)>`;
  ```
- The `XssDemo.vue` component renders this translation using `v-html`:
  ```vue
  <div v-html="$t('welcome', { name })"></div>
  ```
- When the page loads, the malicious code executes, reading `document.cookie` and displaying the stolen token in an alert. In a real attack, this could be exfiltrated to a remote server.

## How to Run

1. Install dependencies:
   ```sh
   npm install
   ```
2. Start the dev server:
   ```sh
   npm run dev
   ```
3. Open the app in your browser. You should see an alert triggered by the XSS payload.

## Important

**Never use `v-html` with untrusted translations or user input.**

---

This demo is for educational purposes only.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

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
test
