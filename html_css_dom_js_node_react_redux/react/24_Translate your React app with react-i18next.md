### Translate your React app with react-i18next

```js
npm install react-i18next i18next --save
```

- Create a new file **i18n.js beside your index.js** containing following content:

```js
import i18n from 'i18next';
import { initReactI18next } from 'react-i18next';

// Translations
const resources = {
  en: {
    translation: {
      'welcome.title': 'Welcome to React and react-i18next',
    },
  },
};

i18n
  .use(initReactI18next) // passes i18n down to react-i18next
  .init({
    resources,
    lng: 'en',
    keySeparator: false, // we do not use keys in form messages.welcome
    interpolation: {
      escapeValue: false, // react already safes from xss
    },
  });

export default i18n;
```

we pass the i18n instance to react-i18next which will make it available for all the components via the context api.

```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import './i18n';
import App from './App';

// append app to dom
ReactDOM.render(<App />, document.getElementById('root'));
```

```js
// The t function is the main function in i18next to translate content.
import React from 'react';
import { useTranslation } from 'react-i18next';

function MyComponent() {
  const { t, i18n } = useTranslation();
  return <h1>{t('welcome.title')}</h1>;
}
```
