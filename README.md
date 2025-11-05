
##  E01Instace.vue 변경 포인트

1. **`<script setup>` 사용**: 보일러플레이트 코드 제거
2. **`export default` 제거**: 더 이상 필요 없음
3. **`data()` → `ref()`**: 반응형 데이터는 `ref()`로 선언
4. **`return` 제거**: 최상위 변수는 자동으로 템플릿에 노출
5. **`name` 속성 제거**: 파일명으로 자동 추론

## 동작확인
![E01Instance 실행 결과](./screenshots/e01-instance.png)
![E02Reactive 실행 결과](./screenshots/e02-reactive.png)


## E02Reactive.vue 변경 포인트

1. **`<script setup>` 사용**: 보일러플레이트 코드 제거
2. **`export default` 제거**: 더 이상 필요 없음
3. **`data()` → `ref()`**: 반응형 데이터는 `ref()`로 선언
4. **`computed` → `computed()`**: 계산 속성을 함수로 변환
5. **`mounted()` → `onMounted()`**: 라이프사이클 훅을 함수로 변환
6. **.value 접근**: 스크립트 내에서 ref 변수는 `.value`로 접근
7. **자동 언래핑**: 템플릿에서는 `.value` 없이 사용 가능


## E03Binding.vue 변경 포인트

1. **`<script setup>` 사용**: 보일러플레이트 코드 제거
2. **`export default` 제거**: 더 이상 필요 없음
3. **`data()` → `ref()`**: 반응형 데이터는 `ref()`로 선언
4. **`return` 제거**: 최상위 변수는 자동으로 템플릿에 노출
5. **`v-model` 동일**: Vue 3에서도 동일하게 작동
6. **자동 언래핑**: 템플릿에서는 `.value` 없이 사용 가능


## E04Directives.vue 변경 포인트

1. **`<script setup>` 사용**: 보일러플레이트 코드 제거
2. **`export default` 제거**: 더 이상 필요 없음
3. **`data()` → `ref()`**: 모든 반응형 데이터를 `ref()`로 선언
4. **디렉티브 유지**: 모든 v-if, v-for, v-show, v-text, v-html, v-pre 등 디렉티브는 동일하게 작동
5. **자동 언래핑**: 템플릿에서는 자동으로 `.value` 언래핑


## ChildComponent
1. **`defineProps()` import**: vue에서 명시적으로 import
2. **`defineEmits()` import**: vue에서 명시적으로 import
3. **Props 선언**: `defineProps(['message'])`로 선언
4. **Emits 선언**: `defineEmits(['custom-event'])`로 선언
5. **`$emit` 유지**: 템플릿에서 동일하게 작동

## ParentComponent
1. **`import` 사용**: 컴포넌트 자동 등록 (components 제거)
2. **`data()` → `ref()`**: 반응형 데이터를 `ref()`로 선언
3. **`methods` → 함수**: 메서드를 일반 함수로 선언
4. **자동 노출**: 모든 변수와 함수가 템플릿에서 자동 사용 가능

## ParentComponent
1. **`provide()` 함수**: vue에서 import 후 직접 호출
2. **컴포넌트 자동 등록**: import만으로 등록 (components 제거)
3. **`export default` 제거**: script setup으로 대체

## ChildComponent1
1. **`inject()` 함수**: vue에서 import 후 변수에 할당
2. **명시적 선언**: `const sharedMessage = inject('sharedMessage')`
3. **컴포넌트 자동 등록**: import로 등록 (components 제거)

## ChildComponent2
1. **`inject()` 함수**: vue에서 import 후 변수에 할당
2. **명시적 선언**: `const sharedMessage = inject('sharedMessage')`

## Provide/Inject 패턴

- **Provide**: 부모에서 데이터 제공
- **Inject**: 자식에서 제공 데이터 주입받음
- 깊은 컴포넌트 트리에서 효율적인 데이터 전달

## E07Options-API.vue

## 변경 포인트

### Props
1. **`defineProps()` 사용**: props 정의
2. **`type`과 `default` 옵션**: 런타임 props 선언 방식
3. 템플릿에서 `props.title` 또는 직접 접근 가능

### Data
1. **`ref()` 사용**: 각 반응형 변수 개별 선언
2. **`.value` 접근**: 스크립트에서만 사용 (템플릿에서 자동 언래핑)

### Computed
1. **`computed()` 함수**: `vue`에서 import
2. **화살표 함수**: 계산된 값 반환
3. **`.value` 접근**: 스크립트에서 필요

### Methods
1. **일반 함수 선언**: `const greet = () => { }`
2. **자동 노출**: 템플릿에서 직접 사용 가능

### Watch
1. **`watch()` 함수**: `vue`에서 import
2. **명시적 선언**: `watch(greetCount, (newValue, oldValue) => {})`

### Lifecycle Hooks
1. **`on`으로 시작**: `onMounted`, `onUpdated` 등
2. **함수 형태**: 콜백을 전달
3. **`beforeCreate`, `created` 제거**: `setup()` 실행 시점이 대체

## 라이프사이클 매핑

| Vue 2 | Vue 3 |
|-------|-------|
| beforeCreate | ❌ (setup 전) |
| created | ❌ (setup 실행 시점) |
| beforeMount | onBeforeMount |
| mounted | onMounted |
| beforeUpdate | onBeforeUpdate |
| updated | onUpdated |
| beforeUnmount | onBeforeUnmount |
| unmounted | onUnmounted |

## 주의사항

`withDefaults`는 TypeScript 타입 기반 선언에만 사용 가능하므로, JavaScript 런타임 선언에서는 `type`과 `default` 옵션을 사용하세요.

## E08Composition-API.vue

## 변경 포인트

### 제거된 항목
1. **`export default` 제거**: 더 이상 필요 없음
2. **`setup()` 함수 제거**: `<script setup>`으로 대체
3. **`return` 제거**: 자동으로 템플릿에 노출
4. **`name` 속성 제거**: 파일명으로 자동 추론
5. **`props` 옵션 제거**: `defineProps()` 함수로 대체

### 추가된 항목
1. **`defineProps()` import**: props 선언
2. **최상위 변수**: 자동으로 템플릿에서 사용 가능

### 동일 항목
1. **`ref()`, `computed()`, `watch()`**: 동일하게 작동
2. **라이프사이클 훅**: 동일 함수명 사용
3. **템플릿 코드**: 전혀 변경 없음

## 코드 라인 비교

| 구분 | Vue 2 Composition API | Vue 3 Script Setup |
|------|----------------------|-------------------|
| 전체 줄 수 | 약 80줄 | 약 70줄 |
| 들여쓰기 깊이 | setup() 내부 | 최상위 레벨 |
| 반환 필요 | 필수 (return {}) | 불필요 |

## 라이프사이클 훅

Vue 2 Composition API와 Vue 3 Script Setup에서 사용되는 라이프사이클 훅은 동일합니다:

- onBeforeMount
- onMounted
- onBeforeUpdate
- onUpdated
- onBeforeUnmount
- onUnmounted

## E09Composition-API2.vue

## 변경 사항

### Before
- 이중 `<script>` 블록 (`export default`와 `<script setup>`)
- `name: 'E09CompositionApi'` 명시적 선언

### After
- 단일 `<script setup>` 블록으로 통합
- 보일러플레이트 코드 제거
- 파일명으로 자동 인식

## 코드 정리

**제거됨:**
- `export default` 블록
- `name` 속성

**유지됨:**
- Props, ref, computed, watch, 라이프사이클 훅
- 모든 기능 동일
- 템플릿 변경 없음

## E10Ref.vue

**Before (Vue 2 - setup 함수)**
- export default 필수
- setup() 함수에서 ref() 사용
- return으로 반환

**After (Vue 3 - script setup)**
- (script setup) 사용
- 최상위 변수 자동 노출

**주요 차이**

| 항목 | Vue 2 | Vue 3 |
|------|-------|-------|
| 구조 | setup() 함수 | script setup 태그 |
| Return | 필수 | 불필요 |
| 라인 수 | ~12줄 | ~8줄 |

**기능**
- ref()로 반응형 데이터 생성
- 템플릿에서 자동 언래핑
- 메서드 자동 노출

---

## E11Reactive.vue

**Before (Vue 2 - setup 함수)**
- export default 필수
- setup() 함수에서 reactive() 사용
- return으로 반환

**After (Vue 3 - script setup)**
- export default 제거
- (script setup)에서 reactive() 직접 사용
- 자동 노출

**핵심 특징**
- reactive(): 객체를 반응형으로 변환
- .value 불필요 (ref와 다름)
- 템플릿에서 직접 접근
- 코드량 감소

**ref vs reactive**

| 구분 | ref | reactive |
|------|-----|----------|
| 타입 | 원시값, 객체 | 객체만 |
| 접근 | .value | 직접 |
| 사용 | 단일 값 | 객체 |

---

## E12RefComponent.vue

**Before (Vue 2 - setup 함수)**
- export default 필수
- setup() 함수 내부에서 ref 선언
- return으로 반환

**After (Vue 3 - script setup)**
- Export default 제거
- (script setup)에서 직접 ref 선언
- 자동 노출

**핵심**
- ref="inputField": 템플릿에서 요소 표시
- const inputField = ref(null): 변수명 일치 필수
- inputField.value: 스크립트에서 DOM 접근
- onMounted 후에만 접근 가능

**주의**
- onBeforeMount: ref가 null (DOM 생성 전)
- onMounted/onUpdated: ref 사용 가능 (DOM 생성 후)