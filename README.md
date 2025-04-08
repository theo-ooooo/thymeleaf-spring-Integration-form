# ✅ 타임리프 - 스프링 통합과 폼

## th:object 와 *{}

`th:object`로 모델 객체를 바인딩하면 내부 필드를 `*{}`로 접근할 수 있음.

```html
<form th:action="@{/items/add}" th:object="${item}" method="post">
  <input type="text" th:field="*{itemName}" />
  <input type="number" th:field="*{price}" />
  <input type="number" th:field="*{quantity}" />
  <button type="submit">저장</button>
</form>
```

---

## th:field

`name`, `id`, `value` 등을 자동으로 설정해줌.

```html
<input type="text" th:field="*{itemName}" />
```

---

## label 태그와 th:for

`th:field`를 사용하면 `id`가 자동 생성되며, `th:for`로 `label`과 연결 가능.

```html
<label th:for="*{itemName}">상품명</label>
<input type="text" th:field="*{itemName}" />
```

---

## #ids.prev / #ids.next

`th:field`가 만든 자동 `id` 값을 기반으로 이전/다음 항목의 id를 참조할 수 있음.

```html
<ul>
  <li th:each="region, stat : ${regions}">
    <input type="radio" 
           th:field="*{region}" 
           th:value="${region.key}" />
    <label th:for="${#ids.prev('region')}">[[${region.value}]]</label>
  </li>
</ul>
```

---

## 체크박스, 라디오 버튼, 셀렉트 박스 처리

```html
<!-- 체크박스 -->
<input type="checkbox" th:field="*{open}" />

<!-- 라디오 버튼 -->
<input type="radio" th:field="*{region}" value="SEOUL" /> 서울
<input type="radio" th:field="*{region}" value="BUSAN" /> 부산

<!-- 셀렉트 박스 -->
<select th:field="*{region}">
  <option th:each="region : ${regions}" 
          th:value="${region.key}" 
          th:text="${region.value}">옵션</option>
</select>
```
