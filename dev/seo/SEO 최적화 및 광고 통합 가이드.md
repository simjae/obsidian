## SEO 최적화 및 광고 통합 가이드

이 문서는 Next.js 14 프로젝트에서 SEO 최적화와 광고 통합을 위한 방법을 상세하게 설명합니다. SEO와 광고(Ads)를 각각 분리하여 설명하며, Meta Tags, Canonical Tag, Structured Data의 역할과 구현 예제를 포함하고 있습니다.


---

### SEO 최적화

SEO(Search Engine Optimization)는 웹사이트의 검색 엔진 가시성을 높여 검색 결과에서 상위에 노출되도록 하는 작업입니다. 이를 통해 더 많은 트래픽을 유도하고, 사용자에게 더 나은 접근성을 제공합니다. SEO의 핵심 요소로는 Meta Tags, Canonical Tag, Structured Data가 있습니다.

#### 1. Meta Tags

**Meta Tags**는 검색 엔진이 페이지의 내용을 이해할 수 있도록 돕는 정보들을 HTML 문서의 `<head>` 섹션에 포함시키는 태그입니다. Meta Tags는 주로 페이지의 제목(title), 설명(description), 키워드(keywords) 등을 정의하며, 검색 엔진 최적화에 중요한 역할을 합니다.

- **Title Tag**: 페이지의 제목을 정의하며, 검색 엔진 결과 페이지(SERP)에서 주요하게 표시됩니다.
- **Description Tag**: 페이지의 요약 설명을 제공하여 사용자가 페이지를 클릭할지 결정하는 데 중요한 역할을 합니다.
- **Keywords Tag**: 페이지와 관련된 키워드를 지정하지만, 현재 대부분의 검색 엔진은 이를 중시하지 않습니다.


```typescript
import Head from 'next/head';

export default function MyPage() {
  return (
    <>
      <Head>
        <title>도안 만들기 - 나만의 비즈 도안</title>
        <meta name="description" content="온라인에서 나만의 비즈 도안을 만들고, 다양한 색상을 선택하여 창의력을 발휘하세요." />
        <meta name="keywords" content="비즈 도안, 펄러비즈, Artkal, 하마비즈, 온라인 도안, 색상 선택" />
      </Head>
      <main>
        {/* 페이지 내용 */}
      </main>
    </>
  );
}

```

#### 2. Canonical Tag

**Canonical Tag**는 검색 엔진에게 특정 페이지의 원본(표준) URL을 알려주는 데 사용됩니다. 이는 중복 콘텐츠 문제를 방지하여 동일한 내용의 여러 URL이 있을 때, 어떤 URL이 원본인지 명확히 함으로써 검색 엔진 순위 하락을 방지합니다.

- **Canonical URL 설정**: 페이지의 중복된 여러 버전이 있을 때, 검색 엔진에게 어떤 URL이 주가 되는지 알려줍니다.

```typescript
import Head from 'next/head';

export default function MyPage() {
  return (
    <>
      <Head>
        <link rel="canonical" href="https://www.mywebsite.com/original-page" />
      </Head>
      <main>
        {/* 페이지 내용 */}
      </main>
    </>
  );
}
```

#### 3. Structured Data (구조화된 데이터)

**Structured Data**는 검색 엔진이 페이지의 내용을 더 잘 이해할 수 있도록 도와주는 추가적인 데이터입니다. 주로 JSON-LD 형식으로 사용되며, 리치 스니펫(검색 엔진 결과 페이지에서의 풍부한 정보)을 표시하는 데 도움을 줍니다.

- **리치 스니펫**: 구조화된 데이터를 통해 검색 결과에 추가 정보(별점, 이미지, 가격 등)를 제공하여 클릭률을 높일 수 있습니다.

```
import Head from 'next/head';

export default function MyPage() {
  const structuredData = {
    "@context": "https://schema.org",
    "@type": "WebSite",
    "url": "https://www.mywebsite.com/",
    "name": "나만의 비즈 도안",
    "description": "온라인에서 나만의 비즈 도안을 만들고, 다양한 색상을 선택하여 창의력을 발휘하세요.",
    "potentialAction": {
      "@type": "SearchAction",
      "target": "https://www.mywebsite.com/search?q={search_term_string}",
      "query-input": "required name=search_term_string"
    }
  };

  return (
    <>
      <Head>
        <script type="application/ld+json">
          {JSON.stringify(structuredData)}
        </script>
      </Head>
      <main>
        {/* 페이지 내용 */}
      </main>
    </>
  );
}

```

### SEO 요소를 프로젝트에 적용하기

위의 Meta Tags, Canonical Tag, Structured Data는 모두 페이지별로 설정할 수 있으며, 각각의 페이지 컴포넌트 내에서 `<Head>` 컴포넌트를 사용해 설정합니다. Next.js의 `app` 디렉토리 구조에서는 각 페이지 파일에 직접적으로 `<Head>` 태그를 추가하여 SEO를 관리할 수 있습니다.

```
src/
  ├─ app/
  │  ├─ page1.tsx
  │  ├─ page2.tsx
  │  └─ ...
  └─ ...

```