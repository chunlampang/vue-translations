# vue-translations
Extremely simple code, flexible, and Javascript friendly translations plugin for Vue.
# Installation
Just download and place it inside your project. No npm.
# Usage
## Set locale
```javascript
this.$t = 'en';
```
## Vue dom
```vue
<p>{{$t.lang}}</p>
<p>{{$t.messages.welcome('guest')}}</p>
<p>{{$t.errors['404']}}</p>
```
## In pure Javascript
```javascript
import translations from 'your-path';
//set
translations.locale = 'en';
//get
translations.locale.lang;
translations.locale.messages.welcome('guest');
translations.locale.errors['404'];
```
## Import
```javascript
import translations from 'your-path';
import en from '@/locales/en';
import zh from '@/locales/zh';

Vue.use(translations, {
    alias: '$t',
    defaultLocale: 'en',
    locales: { en, zh }
});
```
### or use Webpack require.context
```javascript
import translations from 'your-path';

let locales = [];
let req = require.context("@/locales", true, /\.js$/);
req.keys().forEach(key => {
    locales[key.match(/^.\/(.*).js$/)[1]] = req(key).default
});

Vue.use(translations, {
    alias: '$t',
    defaultLocale: 'en',
    locales
});
```
## /locales/en.js
```javascript
export default {
    lang: 'en', // <-- You can use {{$t.lang}} to get current language code now
    pages: { // For menus
        home: 'Home',
    },
    actions: { // For buttons
        login: 'Login',
        logout: 'Logout',
    },
    keywords: {
        development: 'Development',
    },
    messages: {
        welcome: (name) => `Welcome ${name}.`,
    },
    validations: {
    },
    errors: {
        '404': 'Page Not Found',
    }
}
```
## /locales/zh.js
```javascript
export default {
    lang: 'zh',
    pages: {
        home: '首頁'
    },
    actions: {
        login: '登入',
        logout: '登出',
    },
    keywords: {
        development: '開發'
    },
    messages: {
        welcome: (name) => `歡迎，${name}。`,
    },
    validations: {
    },
    errors: {
        '404': '找不到頁面',
    }
}
```
## With vue-router
If you use URL to control the locale, e.g. your-ip/:locale/sub-path\
You should add a key into the router-view tag for updating the locale.
```vue
<router-view :key="$route.params.locale"/>
```
