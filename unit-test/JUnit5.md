# JUnit5

## Assertions
- `org.junit.jupiter.api.Assertions`
- JUnit4에서는 `hamcrest` 패키지를 기본으로 포함했고, 이 패키지의 `assertThat` 등의 메소드를 주로 사용해서 테스트 가독성을 높임
- JUnit5는 더 이상 `hamcrest` 메소드를 기본으로 제공하지 않아서 따로 추가해야 함
- JUnit4의 `Assert` 클래스에 비교했을 때 JUnit5에는 `assertNotEquals()`, `assertNotNull()` 등의 메소드가 추가됨
- 그래도 `hamcrest`에서 제공하는 custom assert, custom matcher를 사용하면 더 좋은 테스트를 작성할 수 있음
→ `Junit5` & `hamcrest` 둘 다 사용!
