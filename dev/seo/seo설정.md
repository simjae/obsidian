Next.js 14 기준으로 SEO 최적화 작업을 위해 다양한 파일과 폴더를 설정하고, 이를 프로젝트에 통합하는 방법을 자세히 설명드리겠습니다. 이 가이드는 `app` 디렉토리 구조를 사용하는 프로젝트를 대상으로 합니다.

## 1. **메타 태그 및 SEO 설정**

### **폴더 및 파일 생성**

- 폴더 경로: `src/components/SEO`
- 파일명: `MetaTags.tsx`

### **MetaTags.tsx 파일 내용**

tsx

코드 복사

`import Head from 'next/head';  interface MetaTagsProps {   title: string;   description: string;   keywords?: string;   author?: string;   image?: string;   url?: string; }  const MetaTags: React.FC<MetaTagsProps> = ({   title,   description,   keywords,   author,   image,   url, }) => {   return (     <Head>       <title>{title}</title>       <meta name="description" content={description} />       {keywords && <meta name="keywords" content={keywords} />}       {author && <meta name="author" content={author} />}       <meta property="og:title" content={title} />       <meta property="og:description" content={description} />       {image && <meta property="og:image" content={image} />}       {url && <meta property="og:url" content={url} />}       <meta name="twitter:card" content="summary_large_image" />       <meta name="twitter:title" content={title} />       <meta name="twitter:description" content={description} />       {image && <meta name="twitter:image" content={image} />}       <meta name="viewport" content="width=device-width, initial-scale=1.0" />     </Head>   ); };  export default MetaTags;`

### **사용 방법**

1. 페이지 컴포넌트에서 `MetaTags` 컴포넌트를 import하여 사용합니다.

tsx

코드 복사

`import MetaTags from '@components/SEO/MetaTags';  const HomePage = () => {   return (     <>       <MetaTags         title="홈페이지 제목"         description="홈페이지 설명"         keywords="비즈 도안, 픽셀 아트, DIY"         author="YourName"         image="https://yoursitename.com/og-image.jpg"         url="https://yoursitename.com"       />       <main>         {/* 메인 콘텐츠 */}       </main>     </>   ); };  export default HomePage;`

## 2. **Canonical URL 설정**

### **폴더 및 파일 생성**

- 폴더 경로: `src/components/SEO`
- 파일명: `CanonicalTag.tsx`

### **CanonicalTag.tsx 파일 내용**

tsx

코드 복사

``import Head from 'next/head'; import { useRouter } from 'next/router';  const CanonicalTag = () => {   const router = useRouter();   const canonicalUrl = `https://yoursitename.com${router.asPath}`;    return (     <Head>       <link rel="canonical" href={canonicalUrl} />     </Head>   ); };  export default CanonicalTag;``

### **사용 방법**

1. 각 페이지에서 `CanonicalTag` 컴포넌트를 사용하여 Canonical URL을 설정합니다.

tsx

코드 복사

`import CanonicalTag from '@components/SEO/CanonicalTag';  const SomePage = () => {   return (     <>       <CanonicalTag />       <main>         {/* 페이지 콘텐츠 */}       </main>     </>   ); };  export default SomePage;`

## 3. **Sitemap 설정**

### **프로젝트 루트에 설정**

1. 프로젝트 루트에 `next-sitemap.config.js` 파일을 생성합니다.

### **next-sitemap.config.js 파일 내용**

javascript

코드 복사

`module.exports = {   siteUrl: 'https://yoursitename.com',   generateRobotsTxt: true,   sitemapSize: 7000,   changefreq: 'daily',   priority: 0.7,   exclude: ['/admin/*', '/login'],   alternateRefs: [     {       href: 'https://yoursitename.com',       hreflang: 'ko',     },     {       href: 'https://yoursitename.com/en',       hreflang: 'en',     },   ], };`

### **Sitemap 자동 생성 설정**

1. `package.json`에 다음 스크립트를 추가합니다:

json

코드 복사

`{   "scripts": {     "postbuild": "next-sitemap"   } }`

2. 빌드 시 자동으로 Sitemap이 생성됩니다:

bash

코드 복사

`npm run build`

## 4. **robots.txt 설정**

1. `public/robots.txt` 파일을 생성하여 검색 엔진 크롤러의 접근을 제어합니다.

### **robots.txt 파일 내용**

txt

코드 복사

`User-agent: * Allow: /  Sitemap: https://yoursitename.com/sitemap.xml`

## 5. **구조화된 데이터 설정**

### **폴더 및 파일 생성**

- 폴더 경로: `src/components/SEO`
- 파일명: `StructuredData.tsx`

### **StructuredData.tsx 파일 내용**

tsx

코드 복사

`import Head from 'next/head';  const StructuredData = () => {   const structuredData = {     "@context": "https://schema.org",     "@type": "WebSite",     "url": "https://yoursitename.com",     "name": "YourSiteName",     "potentialAction": {       "@type": "SearchAction",       "target": "https://yoursitename.com/search?query={search_term_string}",       "query-input": "required name=search_term_string"     }   };    return (     <Head>       <script         type="application/ld+json"         dangerouslySetInnerHTML={{ __html: JSON.stringify(structuredData) }}       />     </Head>   ); };  export default StructuredData;`

### **사용 방법**

1. 메인 페이지나 관련된 페이지에서 `StructuredData` 컴포넌트를 사용합니다.

tsx

코드 복사

`import StructuredData from '@components/SEO/StructuredData';  const HomePage = () => {   return (     <>       <StructuredData />       <main>         {/* 메인 콘텐츠 */}       </main>     </>   ); };  export default HomePage;`

---

이 작업들을 통해 Next.js 14 프로젝트에서 SEO 최적화를 할 수 있습니다. 각 컴포넌트는 SEO 관련 태그를 효율적으로 관리할 수 있게 도와주며, 필요에 따라 다양한 페이지에 쉽게 적용할 수 있습니다. 프로젝트 루트와 `src/components/SEO` 폴더에서 필요한 파일을 생성하고 적절히 import하여 사용하면 됩니다.