### DTO
*상태를 저장하고, 상태를 전달하는 목적이기 때문에 로직을 가지지 않으며, 종종 API 응답이나 요청에서 사용됩니다.*
**==데이터 전달이 목적으로 로직을 가지지 않는다==**
(GETTER, SETTER)
### VO
불변 객체로 설계되어 변경할 수 없으며, 데이터가 동일하면 객체도 동일하다고 간주됩니다.
(GETTER) *SETTER는 없음 (불변)

### DAO
DB와의 상호작용을 담당하는 객체로, 데이터를 CRUD(create, read, update, delete)하는 로직을 포함


### DTO에서의 Boolean, boolean
### `boolean` vs `Boolean` 차이

#### 1. **`boolean` (원시 타입)**

- JavaScript의 원시 타입(`primitive type`).
- 값으로 `true` 또는 `false`만 가질 수 있음.
- `undefined`나 `null`을 직접 가질 수 없음.
- 초기화되지 않으면 `undefined`.

#### 2. **`Boolean` (객체 타입)**

- `new Boolean(value)`로 생성하는 객체(`Object`).
- `true`, `false`뿐만 아니라 **객체이므로 항상 truthy**.
- `undefined`, `null` 대신 객체로 값을 가질 수 있음.

---

### 왜 `boolean`은 `undefined`이고 `Boolean`은 값이 들어오는가?

1. **DTO에서 `boolean`을 사용했을 때:**
    
    - JavaScript에서 원시 `boolean` 타입의 기본값이 없기 때문에, 값이 주어지지 않으면 `undefined`가 됨.
    
    typescript
    
    복사편집
    
    `class MyDTO {     myBool?: boolean; }  const dto = new MyDTO(); console.log(dto.myBool); // undefined (값이 없으면 초기화되지 않음)`
    
2. **DTO에서 `Boolean`을 사용했을 때:**
    
    - `Boolean`은 객체 타입이므로, 값이 없어도 `undefined`가 아니라 **Boolean 객체의 기본값**이 설정될 가능성이 높음.
    
    typescript
    
    복사편집
    
    `class MyDTO {     myBool?: Boolean; }  const dto = new MyDTO(); console.log(dto.myBool); // undefined가 아니라 Boolean 객체가 들어갈 수도 있음.`
    

---

### 해결 방법

**기본값을 명확히 설정하려면 원시 타입(`boolean`)을 사용하고, 기본값을 지정하는 것이 좋음.**

typescript

복사편집

`class MyDTO {     myBool: boolean = false; // 기본값 설정 }  const dto = new MyDTO(); console.log(dto.myBool); // false`

**`Boolean`을 사용할 이유가 없다면 원시 타입(`boolean`)을 쓰는 게 낫다.**  
특히 객체 비교 시 `Boolean` 객체와 `boolean` 값이 다를 수 있어 혼란을 초래할 수 있음.

typescript

복사편집

`const a: boolean = false; const b: Boolean = new Boolean(false);  console.log(a === b); // false (객체 vs 원시 값 비교) console.log(b ? 'Truthy' : 'Falsy'); // 'Truthy' (Boolean 객체는 항상 truthy)`