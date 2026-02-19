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