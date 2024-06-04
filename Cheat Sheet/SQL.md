# SQL
- 다중 정렬 `order by A (desc), B (desc)`
    - 우선 순위 높은 것부터 정렬
- 컬럼 별칭으로 출력 `as 별칭`
- 컬럼 개수 출력 `count(컬럼)`
- DATETIME 컬럼 형식 지정 `date_format(컬럼명, 'format')`
    - `%Y` 년
    - `%M` 월
    - `%D` 일
- `ifnull(A, B)` A가 null이면 A를 반환, A가 null이 아니면 B를 반환 