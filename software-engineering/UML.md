# UML

## Relations

![image](https://user-images.githubusercontent.com/43198798/110248036-852a9a00-7fb2-11eb-9ba1-3e3bf5f5b3dc.png)

|Assocation|Aggregation|Composition|
|--|--|--|
|연관|전체와 부분|전체와 부분|
||has a|has a|
|생명주기 연관 없음|생명주기가 다름|생명주기가 같음|
||메소드 내 필드|멤버변수|

### Aggregation 사용의 필요성에 대한 논쟁
- Aggregation은 부분이 전체에 완전히 종속되지 않는 포함관계인 경우를 나타냄.
- 예) Person& A ddress, Student & Class
- 코드로 변환했을 때 다른 표현방법과 차이가 크지 않기 때문에 사용하지 않는 편.
