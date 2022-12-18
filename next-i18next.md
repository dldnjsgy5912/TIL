### i18n 이란?

i18n이란 internationalization(국제화) 라는 단어를 축약한 것이다. i부터 n까지 18개의 문자수를 축약해서 i18n으로 나타낸다.

### 동작 원리

next-i18next.config.js 파일을 통해 next-i18next에 대한 구성 환경을 제공하며 환경 세팅 후 appWithTranslation을 useTranslation 훅을 사용후 t를 통해서 해당 url에 맞는 번역 기능을 제공한다.

### next-i18next 설치

```
npm i next-i18next
yarn add next-i18next
```

### 셋업

```js
// next-i18next.config.js
module.exports = {
  i18n: {
    defaultLocale: 'en',
    locales: ['en', 'de'],
  },
};
```

```js
// next.config.js
const { i18n } = require('./next-i18next.config');
module.exports = {
  i18n,
};
```

### locale 파일 생성

public/locales 에 만들어주면 된다.
public/locales/en/home.json
public/locales/ko/home.json

```js
// public/locales/ko/home.json
{
    "h1": "홈 페이지",
    "description": "안녕하세요 홈 페이지입니다.",
    "currentUrl": "현재 url"
}

// public/locales/en/home.json
{
    "h1": "Home Page",
    "description": "Hello this is Home page",
    "currentUrl": "current url"
}
```

Home 페이지
serverSideTranslations 통해서 locale 정보를 넘겨주고
useTranslation 훅을 통해서 해당 json 에 값을 반환한다.

```js
import { appWithTranslation } from 'next-i18next';

const MyApp = ({ Component, pageProps }) => <Component {...pageProps} />;

export default appWithTranslation(MyApp);
```

```js

// /pages/about.tsx
import React from 'react'
import { useRouter } from 'next/router'
import { serverSideTranslations } from 'next-i18next/serverSideTranslations'
import { useTranslation } from 'next-i18next'

export const getStaticProps: GetStaticProps = async ({ locale }) => {
  return {
    props: {
      ...(await serverSideTranslations(locale as string, ["home"])),
    },
  };
};
const HomePage: React.FC = () => {
  const router = useRouter()
  const { t } = useTranslation('home')

  return (
    <div>
      <h1>{t('h1')}</h1>
      <ul>
        <li>
          {t('currentUrl')} : http://localhost:3000
          {router.locale !== 'ko' && '/' + router.locale}
          {router.pathname}
        </li>
        <li>locale: {router.locale}</li>
        <li>pathname: {router.pathname}</li>
      </ul>
    </div>
  )
}

export default HomePage
```
