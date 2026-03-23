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

---

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

---

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

---

# 2026-3-9 수정, 추가 사항

## code_problems 폴더, 코드 빈칸 문제 추가
- testcase 5개 정도로 생성
- topicid는 기준을 모르겠어서 일단 123 형식으로 linear하게 증가

## 폴더명 변경
- problems -> basic_problems 개념 예제라서 수정하는 것이 용이해보여 변경

## detail 부분 markdown
- 가독성 높이기위해 내용 추가와 markdown형식으로 변경하였음

## 문제 부분에서 선택지 추가
- contents가 하나만 있는 것으로 알았는데 객관식 선택지가 더 필요하다는 이야기를 듣고 수정

---

# 2026-3-16 수정, 추가 사항

## notion 파일 추가
- array, hash, stack에서 알고리즘 책 참고하여 queue, sort, binarysearch, bruteforce, greedy, heap, dp, dfs, bfs, graph 추가

## notion detail 마크다운 전면 개선
- 전체 40개 notion 파일 (array, stack, hash, queue, sort, binarysearch, bruteforce, greedy, heap, dp, dfs, bfs, graph) detail 마크다운 가시성 개선
- 볼드(`**`), 인라인 코드(`` ` ``), 표(`|`), 구분선(`---`), 이모지(💡🔍⚠️📊) 적용
- 복잡도 분석을 산문 나열에서 표 형식으로 통일
- 주의사항(⚠️) 섹션 신규 추가

## notion 파일 내용 오류 수정 (array, stack, hash)
- topicId=2(stack) pageNo=2 중복 항목 제거
- topicId=2(stack) pageNo=3 누락 파일 신규 생성 (배열 기반 스택 코드)
- topicId=2(stack) pageNo=2와 pageNo=4의 재귀 관련 내용 중복 제거

## code_problems topicId 및 파일명 수정
- 파일명 규칙을 `{notionTopicId}_lv{difficulty}_{영문제목}.json` 으로 통일
- 파일명과 내부 topicId 불일치 전수 검사 후 수정
  - valid_brackets: topicId 1→2 (STACK)
  - two_sum: topicId 2→4 (HASH)
  - prime_check: topicId 3→1 (ARRAY)
  - max_subarray: topicId 4→10 (DP)
  - fibonacci: topicId 5→10 (DP)
  - count_islands: topicId 6→12 (BFS)
  - lis: topicId 7→6 (BINARYSEARCH)

## code_problems solutionText 마크다운 개선
- 7개 문제 전체 solutionText 마크다운 개선 (볼드, 표, 구분선, 이모지, 주의사항 추가)

## code_problems 신규 문제 추가 (총 9개)
- `01_lv1_find_max_index.json` : 배열에서 최댓값 찾기 (ARRAY / lv1)
- `01_lv1_prime_check.json` : 소수 판별 (ARRAY / lv1)
- `02_lv2_valid_brackets.json` : 올바른 괄호 문자열 (STACK / lv2)
- `04_lv1_two_sum.json` : 두 수의 합 (HASH / lv1)
- `04_lv2_first_duplicate.json` : 첫 번째 중복 숫자 찾기 (HASH / lv2)
- `06_lv3_lis.json` : 가장 긴 증가하는 부분 수열 (BINARYSEARCH / lv3)
- `10_lv1_fibonacci.json` : 피보나치 수열 (DP / lv1)
- `10_lv2_max_subarray.json` : 연속 부분 배열의 최대 합 (DP / lv2)
- `12_lv3_count_islands.json` : 섬의 개수 (BFS / lv3)

## blank_problems 전면 개선
- 모든 파일에 `{ "requests": [ ... ] }` 래퍼 구조 추가
- codeTemplate에 `import`, `public class Main`, `public static void main` boilerplate 추가
- 정답이 2개 이상인 문제의 description에 "빈칸 N개를 채우세요" 명시
- 파일명 규칙을 `{topicId}_{name}_lv{orderNo}_1.json` 으로 통일
- topicId, orderNo, 빈칸 수, 정답 수 전수 검증 완료

# 2026-3-23 추가사항
## topicid별 주제 설명
 - 1. 배열
 - 2. 스택
 - 3. 큐
 - 4. 해시
 - 5. 정렬
 - 6. 이진 탐색
 - 7. 브루트 포스
 - 8. 탐욕법
 - 9. 힙
 - 10. 동적 프로그래밍
 - 11. dfs
 - 12. bfs
 - 13. 그래프
 