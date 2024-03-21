
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


### Create locales or with any name folder on root directory
```
# locales/en/home.jsn

{
    "welcome.to.the.home": "Welcome to the home",
    "en": "UR",
    "home": "Home",
    "about.us": "About Uus",
    "services": "Services",
    "pricing": "Pricing",
    "contact.us": "Contact Us",
    "lorem": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum."
}

# locales/ur/home.jsn

{
    "welcome.to.the.home": "گھر میں خوش آمدید",
    "en": "EN",
    "home": "گھر",
    "about.us": "کے بارے میں",
    "services": "خدمات",
    "pricing": "قیمتوں کا تعین",
    "contact.us": "رابطہ کریں۔",
    "lorem": "Lorem Ipsum پرنٹنگ اور ٹائپ سیٹنگ انڈسٹری کا محض ڈمی ٹیکسٹ ہے۔ Lorem Ipsum 1500 کی دہائی سے انڈسٹری کا معیاری ڈمی ٹیکسٹ رہا ہے، جب ایک نامعلوم پرنٹر نے قسم کی ایک گیلی لی اور اسے ایک قسم کے نمونے کی کتاب بنانے کے لیے کھینچا۔ یہ نہ صرف پانچ صدیوں تک زندہ رہا ہے بلکہ الیکٹرانک ٹائپ سیٹنگ میں بھی چھلانگ لگا ہوا ہے، بنیادی طور پر کوئی تبدیلی نہیں کی گئی۔ یہ 1960 کی دہائی میں Lorem Ipsum حصئوں پر مشتمل Letraset شیٹس کے اجراء کے ساتھ اور حال ہی میں Aldus PageMaker جیسے ڈیسک ٹاپ پبلشنگ سافٹ ویئر کے ساتھ مقبول ہوا جس میں Lorem Ipsum کے ورژن بھی شامل ہیں۔"
}

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
