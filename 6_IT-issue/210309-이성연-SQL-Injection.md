# SQL Injection

## 1. 현 상황

## 2. SQL Injection 및 대응방안

## 3. 방향



### 1. 현상황

- 해킹 및 개인정보 침해 사고
  - 20년 NC백화점 랜섬웨어 공격
  - 17년 숙박 사이트 여기 어때 개인정보 유출.
  - 15년 커뮤니티 사이트 뽐뿌 개인정보 유출.
- OWASP 에서 계속해서 순위를 차지하는 SQL Injection 공격이 가장 심각한 문제 중 하나.



### 2. SQL Injection 및 대응 방안

- SQL Injection ; 악의적인 SQL 문을 실행되게 하여, 데이터베이스를 비정상적으로 조작하는 Code Injection 공격 방법.

![SQL-1](/6_IT-issue/assets/SQL-1.png)

- 방어 방법
  - 방화벽 사용.
  - 시큐어 코딩
    - prepared statement ; 변수를 문자열로 변경.
    - 화이트리스트 사용.
  - 취약점 점검과 모니터링.



### 3. 방향

- 공격 기법이 지속적으로 진화.
- 해킹이 발전하면서 시스템 방어도 함께 발전시켜야 내부 자산을 강력하게 보호할 수 있다.

