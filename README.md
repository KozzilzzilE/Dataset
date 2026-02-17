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
