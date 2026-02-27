# Firestore 샘플 데이터셋 (분리 구조)

## 구조
- topics/{topicId}
- topics/{topicId}/notions/{pageNo}
- topics/{topicId}/notions/3/codes/{languageId}

## 규칙
- pageNo: 1(간단) / 2(심화) / 3(코드설명)
- pageNo=3에만 codes 존재

## 예시
- topic(topic_id) -> topics/{topicId}
- notion(topic_id, page_no, title, point, detail, img_url) -> topics/{topicId}/notions/{pageNo}
- notion_code(notion_id, language_id, content) -> topics/{topicId}/notions/3/codes/{languageId}

# Dataset 구조 변경 사항

## pageNo 정책

- pageNo는 난이도(간단/심화/코드) 가 아니라 페이지 식별/순서용 번호로 사용한다.
- 주제별 페이지 수는 3에 고정되지 않으며 4~N까지 확장 가능하다.
- 코드가 필요한 페이지는 pageNo와 무관하게 해당 페이지 JSON에 codes를 포함한다.

## codes 포함 방식

- 기존처럼 notions/{pageNo}/codes/{id}로 분리하지 않고,
- 코드가 있는 페이지는 해당 페이지 JSON 내부에 codes 배열로 합친다.

## 이미지 처리 방식

- 아직 연동상태를 몰라서 일단 이미지 파일을 github에 포함시켰음.

# 2026-2-27 수정, 추가 사항

## Notion 스키마 통일

- imgUrl: "" → imgUrl: null
- 코드 없는 페이지 → "codes": null 명시
- 코드 있는 페이지 → "codes": [ ... ]
- docPath 제거 (API에서 불필요)

## 코드 작성 규칙

- Java만 사용
- 들여쓰기 스타일 통일
- escape 문자 문제 없도록 `\n` 유지
- content 내부는 반드시 ```java

## 폴더명 변경

- sample -> notions로 폴더명 변경

## 문제 추가

- 이름으로만 하면 파일 정렬이 어려울 것 같아 NN_topic_level_index.json
- orderNo는 난이도 별로 테이블이 나눠져있는지 몰라서 1씩 증가하게 함