
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

## Replace below code with src/pages/_app.tsx

``` 
import "@/styles/globals.css";
import type { AppProps } from "next/app";
import { useEffect } from "react";
import i18n from "../../i18n";
import { DEFAULT_LANGUAGE } from "@/constants/app";
import { I18nextProvider } from "react-i18next";
import { getCookie } from "cookies-next";

function MyApp({ Component, pageProps }: AppProps) {
  const _lang = getCookie("lang");

  useEffect(() => {
    i18n.changeLanguage(_lang || DEFAULT_LANGUAGE);
  }, []);
  return (
    <I18nextProvider i18n={i18n}>
      <Component {...pageProps} />
    </I18nextProvider>
  );
}

export default MyApp;

```


## Create components directory inside components create navbar.tax paste below code

``` 
import { DEFAULT_LANGUAGE, SECONDARY_LANGUAGE } from "@/constants/app";
import React, { useState } from "react";
import { useTranslation } from "react-i18next";
import i18n from "../../i18n";
import { setCookie } from "cookies-next";

function Navbar() {
  const [isOpen, setIsOpen] = useState(false);

  const toggleMenu = () => {
    setIsOpen(!isOpen);
  };

  const changeLanguage = () => {
    const change_lang =
      i18n.language != DEFAULT_LANGUAGE ? DEFAULT_LANGUAGE : SECONDARY_LANGUAGE;
    setCookie("lang", change_lang);
    i18n.changeLanguage(change_lang);
  };
  const { t } = useTranslation();

  return (
    <nav className="bg-white border-gray-200 dark:bg-gray-900">
      <div className="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
        <button
          onClick={toggleMenu}
          className="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
          aria-controls="navbar-default"
          aria-expanded={isOpen ? "true" : "false"}
        >
          <span className="sr-only">Open main menu</span>
          <svg
            className="w-5 h-5"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 17 14"
          >
            <path
              stroke="currentColor"
              strokeLinecap="round"
              strokeLinejoin="round"
              strokeWidth="2"
              d="M1 1h15M1 7h15M1 13h15"
            />
          </svg>
        </button>
        <div
          className={`md:block md:w-auto ${isOpen ? "" : "hidden"}`}
          id="navbar-default"
        >
          <ul className="font-medium flex flex-col p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 rtl:space-x-reverse md:mt-0 md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700">
            <li>
              <a
                href="#"
                className="block py-2 px-3 text-white bg-blue-700 rounded md:bg-transparent md:text-blue-700 md:p-0 dark:text-white md:dark:text-blue-500"
                aria-current="page"
              >
                {t("home")}
              </a>
            </li>
            <li>
              <a
                href="#"
                className="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent"
              >
                {t("about.us")}
              </a>
            </li>
            <li>
              <a
                href="#"
                className="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent"
              >
                {t("services")}
              </a>
            </li>
            <li>
              <a
                href="#"
                className="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent"
              >
                {t("pricing")}
              </a>
            </li>
            <li>
              <a
                href="#"
                className="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent"
              >
                {t("contact.us")}
              </a>
            </li>
            <li>
              <button
                className="upppercase text-center item   language-component"
                onClick={changeLanguage}
              >
                <span>{t("en")} </span>
              </button>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  );
}

export default Navbar;


```




## Replace below code with src/pages/index.tsx

``` 
import Image from "next/image";
import { Inter } from "next/font/google";
import { setCookie } from "cookies-next";
import i18n from "../../i18n";
import { DEFAULT_LANGUAGE, SECONDARY_LANGUAGE } from "@/constants/app";
import { useTranslation } from "react-i18next";
import Navbar from "@/components/navbar";

const inter = Inter({ subsets: ["latin"] });

export default function Home() {
  const { t } = useTranslation();

  return (
    <main
      className={`flex  flex-col items-center justify-between  ${inter.className}`}
    >
      <Navbar />
      <div className="container grid grid:cols-span-2 max-w-[700px]">
        <h4>{t("lorem")}</h4>
      </div>
    </main>
  );
}


export default MyApp;

```
