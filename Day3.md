explain 항상 쳐서 제대로 indexing이 되었는지 확인해보기(쿼리 실행 결과 시간 확인)


# window function 예시
e.g. rank
```
SELECT   JOB, ENAME, SAL,
         RANK() OVER (ORDER BY SAL DESC) ALL_RANK,  -- 급여 높은 순
         RANK() OVER (PARTITION BY JOB ORDER BY SAL DESC) JOB_RANK -- job 별로 급여 높은 순
FROM     EMP ;   
```