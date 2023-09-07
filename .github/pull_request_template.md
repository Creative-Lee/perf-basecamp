## 🔥 결과

<!-- 개선 목표에 있는 측정 항목들에 대해 개선 작업 전/후의 성능 측정 결과를 적어주세요. -->

- 배포한 CloudFront 접근 경로:
- 개선 전후 성능 측정 결과
  - 개선 전 (GitHub Pages)
  - 개선 후 (CloudFront)

## ✅ 개선 작업 목록

**1 요청 크기 줄이기**

- [ ] 소스코드 크기 줄이기
  - [x] prod 환경에서 `optimization.minimize` 옵션적용으로 `terserPlugin`을 통해 **minify, uglify** 적용
  - [x] css 파일 추출
    - [x] miniCssExtract 플러그인 적용
  - [x] gzip 적용
- [ ] 이미지 크기 줄이기
  - [x] `ImageMinimizerPlugin` 적용
    - [x] `sharp` 을 통해 gif,png -> webp로 변환 및 압축
    - [ ] `srcset` 적용(선택)
- [ ] 폰트(선택)
  - [ ] subset적용
  - [ ] FOUT 개선

**2 필요한 것만 요청하기**

- [x] 페이지별 리소스 분리(home 페이지에서 giphy모듈 제외하기)
  - [x] react.lazy 사용하여 page 단위 컴포넌트에 `코드 스플리팅 적용`
- [x] 아이콘 패키지 Tree Shaking
  - [x] usedExports 옵션 기본 적용으로 icons 패키지 `트리쉐이킹 완료`

**3 같은 건 매번 새로 요청하지 않기**

- [x] CloudFront 캐시 설정 (설정값, 해당 값을 설정한 이유 포함)
  - [x] 커스텀 캐시 정책 설정 X / 기본값 사용
  - [x] s3 메타 데이터 설정
    - [x] /static 경로 하위 image 파일(webp)은 max-age 1년
    - [x] 나머지 js, css와 같은 파일은 max-age 1일
- [x] GIPHY의 trending API를 Search 페이지에 들어올 때마다 새로 요청하지 않아야 한다.
  - [x] 간단한 캐시 구현(Map)

**4 최소한의 변경만 일으키기**

- [x] 검색 결과 > 추가 로드시 추가된 목록만 새로 렌더되어야 한다.
  - [x] gifItem 컴포넌트에 memo 적용
- [x] Layout Shift 없이 애니메이션이 일어나야 한다.
  - [x] 커스텀 스크롤 스타일링 / top, left => transform
  - [x] GifItem 컴포넌트 hover / top -> transform
  - [x] helpPanel 컴포넌트 open,close / right -> transform
- [ ] partially presented frame 최소화 및 Frame Drop x
  - [ ] 현재 성능 저하 환경에서 스크롤 시 Frame Drop 및 partially presented frame 다수 발생...
    - [ ] 리뷰 이후 `requestAnimationFrame` 학습 및 적용 예정

## 🧐 공유

<!-- 작업하면서 든 생각, 질문, 새롭게 학습하거나 시도해본 내용 등등 공유할 사항이 있다면 자유롭게 적어주세요 -->
