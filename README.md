
## Getting Started

First, clone the respo install yarn run the development server:

```bash
npm run dev
# or
yarn dev
```

#DEMO


### ENGLISH
![image](https://github.com/sajjadlaghari/next-js-localization-with-i18n/assets/68752819/5d8967c3-f553-4db2-b5c9-bd134e8764fa)

### URDU

![image](https://github.com/sajjadlaghari/next-js-localization-with-i18n/assets/68752819/9febb38d-2848-4997-a2b3-f9cc3c2c582c)


## First Install

```bash
yarn add i18next
# and
yarn add react-i18next
# and cookie you can use local session also
yarn add cookies-next 
```

### Create i18n.ts file one root directory
```
import i18n from "i18next";
import { initReactI18next } from "react-i18next"
// import Backend from "i18next-http-backend"
import homeEn from "./locales/en/home.json"
import homeUr from "./locales/ur/home.json"
// erros

import { DEFAULT_LANGUAGE } from "@/constants/app";

const resources = {
    en: {
        home: homeEn,
    },
    ur: {
        home: homeUr,
    },
};

i18n
    .use(initReactI18next)
    //   .use(Backend)
    .init({
        resources,
        fallbackLng: DEFAULT_LANGUAGE,
        supportedLngs: [
            "en",
            "ur"
        ],
        ns: ["home", "errors"],
        defaultNS: "home"
    });

export default i18n

# Replace Past Above code
```
