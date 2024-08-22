
## 광고 통합 (Ads Integration)

SEO 최적화와 함께 광고를 웹사이트에 통합하는 것도 중요합니다. 웹사이트에서 Google AdSense, Amazon Ads, Facebook Audience Network와 같은 광고 네트워크를 사용하여 수익을 창출할 수 있습니다.

### 1. Google AdSense 통합

Google AdSense는 웹사이트에서 광고를 통해 수익을 창출할 수 있는 가장 일반적인 방법 중 하나입니다. 이를 위해 웹사이트에 AdSense 스크립트를 추가해야 합니다.

Google AdSense 코드 예제:
```
import { useEffect } from 'react';

export default function GoogleAds() {
  useEffect(() => {
    (window.adsbygoogle = window.adsbygoogle || []).push({});
  }, []);

  return (
    <ins className="adsbygoogle"
      style={{ display: 'block' }}
      data-ad-client="ca-pub-xxxxxxxxxxxxxxxx"
      data-ad-slot="xxxxxxxxxx"
      data-ad-format="auto"
      data-full-width-responsive="true"></ins>
  );
}

```

`data-ad-client`와 `data-ad-slot` 값은 Google AdSense 계정에서 제공되는 실제 값을 사용해야 합니다.

### 2. 광고를 페이지에 적용하기

광고 컴포넌트를 특정 페이지나 레이아웃에 추가하여 광고를 표시할 수 있습니다. 예를 들어, 페이지의 상단, 사이드바, 또는 본문 중간에 광고를 배치할 수 있습니다.

**광고 컴포넌트 적용 예제:**

```
import GoogleAds from './GoogleAds';

export default function MyPage() {
  return (
    <div>
      <GoogleAds />
      <main>
        {/* 페이지 내용 */}
      </main>
      <GoogleAds />
    </div>
  );
}

```

### 광고를 페이지에 동적으로 로드하기

광고를 SPA(싱글 페이지 애플리케이션) 구조에서 동적으로 로드하려면, 광고 스크립트의 동작을 고려해야 합니다. 예를 들어, 페이지가 전환될 때마다 광고가 새로 로드되도록 설정해야 할 수 있습니다.

**광고 스크립트 재로드 예제:**
```
import { useEffect } from 'react';
import GoogleAds from './GoogleAds';

export default function MyPage() {
  useEffect(() => {
    if (typeof window !== 'undefined') {
      (window.adsbygoogle = window.adsbygoogle || []).push({});
    }
  }, []);

  return (
    <div>
      <GoogleAds />
      <main>
        {/* 페이지 내용 */}
      </main>
    </div>
  );
}

```

### 요약

- **Meta Tags**: 페이지의 제목, 설명, 키워드를 설정하여 검색 엔진에서의 가시성을 높입니다.
- **Canonical Tag**: 중복 콘텐츠 문제를 해결하고, 검색 엔진에게 원본 페이지를 알려줍니다.
- **Structured Data**: 페이지에 대한 추가 정보를 제공하여 리치 스니펫과 같은 검색 결과의 가시성을 높입니다.
- **광고 통합**: Google AdSense와 같은 광고 네트워크를 사용하여 웹사이트에서 수익을 창출합니다.

위의 내용들은 모두 Next.js 14의 `app` 디렉토리 구조에 맞춰 작성되었으며, 각 페이지에 필요한 부분을 적절히 삽입하여 적용할 수 있습니다