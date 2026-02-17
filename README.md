# Firestore 샘플 데이터셋 (분리 구조)

## 구조
- topics/{topicId}
- topics/{topicId}/notions/{pageNo}
- topics/{topicId}/notions/3/codes/{languageId}

## 규칙
- pageNo: 1(간단) / 2(심화) / 3(코드설명)
- pageNo=3에만 codes 존재
