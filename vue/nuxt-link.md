# a태그와 nuxt-link 태그

nuxt3로 프로젝트 진행 중, 기존 코드는 a태그로 내부/외부 링크 이동함

## a태그로 이동했을 때 문제

- 상태관리하던게 초기화됨 → 이유: a태그는 페이지 이동 시 전체 새로고침
- a태그는 전체 새로고침하며 이동하고, 다른 웹사이트 이동 시 사용
- nuxt-link 태그는 새로고침 없이 이동하며, 프로젝트 내 페이지 이동 시 사용

이라고 하는데, 사실은 nuxt-link 태그만으로도 외부 링크 이동이 가능하다.

---

nuxt-link에서 외부 라우팅이 가능한데 a태그로 나누어줄 이유가 있는가? 라고 생각을 했던 지점은,

기존에 a태그로 blank(새 창으로 열기)를 설정했을 때, noopener 속성을 넣어줘야 안전하기 때문에 a태그를 작성 시  
`<a target=*"*blank" href="https://example.com" rel="noopener noreferrer">`  
이랬다면...

[`<NuxtLink>`](https://nuxt.com/docs/3.x/api/components/nuxt-link#rel-and-norel-attributes)  
공식문서를 봤을 때 nuxt-link 컴포넌트는 target="_blank" 이거나 to 속성이 절대 URL(http://, https://, //)인 경우, noopener과 noreferrer를 자동으로 추가해준다.

그렇기 때문에 외부 링크라는 이유만으로 a태그로 작성해줘야 할 이유가 없지 않은가… 라는 의문이 들었음  
(nuxt-link 자체가 to가 외부링크로 되어 있으면 a태그로 렌더링하니까… 그대로 작성하는 쪽이 코드가 더 깔끔하지 않나 싶었다.)

[Nuxtjsの <a> と <NuxtLink> の使い分けについて。](https://qiita.com/sonimaru/items/0f8c22542f026a535cf2)  
위 링크에서는 명확하게 a태그는 외부! nuxt-link는 내부!로 정의를 하고 있으며,  
챗선생님도 명확/직관을 위하여 외부 링크는 a태그로 작성하는 것이 좋다고 했다.

---

## + 챗선생님 🧑‍🏫
### ❗ a 태그를 나누는 이유

#### 1. 의도 명확성
- `<NuxtLink>` → 내부 라우팅
- `<a>` → 외부 이동  
👉 코드만 보고 바로 이해 가능

#### 2. 사이드 이펙트 방지
- 불필요한 prefetch / 라우팅 로직
- SSR hydration mismatch 가능성
- click 이벤트 충돌 가능성

#### 3. 유지보수 & 협업
- 팀 컨벤션에서 명확하게 구분하는 경우가 많음
- 실수 및 버그 예방

---

### ✅ 최종 결론

- **내부 링크 → NuxtLink**
- **외부 링크 → a 태그**

👉 NuxtLink로 통일도 가능하지만,  
실무에서는 "의도 명확성 + 안정성" 때문에 분리하는 것이 일반적

---
`2026-03-18`