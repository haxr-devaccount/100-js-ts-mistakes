# 100 JavaScript ve TypeScript Hatası ve Çözümleri

## Değişken ve Kapsam Hataları (1-10)

1. **var Kullanımı**
```javascript
// Hatalı
var x = 5;
// Doğru
let x = 5;
```

2. **Değişken Hoisting**
```javascript
// Hatalı
console.log(x);
var x = 5;
// Doğru
let x = 5;
console.log(x);
```

3. **Blok Kapsamı İhlali**
```javascript
// Hatalı
if (true) {
    var blockScoped = 'value';
}
console.log(blockScoped); // Erişilebilir

// Doğru
if (true) {
    let blockScoped = 'value';
}
console.log(blockScoped); // ReferenceError
```

4. **Sabit Değişkenleri Yanlış Tanımlama**
```javascript
// Hatalı
let PI = 3.14;
PI = 3.15; // Değiştirilebilir

// Doğru
const PI = 3.14;
```

5. **Global Değişken Kirliği**
```javascript
// Hatalı
function sum(a, b) {
    result = a + b; // Global
    return result;
}

// Doğru
function sum(a, b) {
    const result = a + b;
    return result;
}
```

6. **Temporal Dead Zone (TDZ)**
```javascript
// Hatalı
console.log(x);
let x = 5;

// Doğru
let x;
console.log(x);
x = 5;
```

7. **const ile Obje Değişmezliği**
```javascript
// Hatalı - const objenin içeriğini değiştirmeyi engellemez
const user = { name: 'Ali' };
user.name = 'Veli'; // Çalışır

// Doğru
const user = Object.freeze({ name: 'Ali' });
```

8. **Döngü Değişkeni Kapsamı**
```javascript
// Hatalı
for (var i = 0; i < 5; i++) {
    setTimeout(() => console.log(i), 100);
}

// Doğru
for (let i = 0; i < 5; i++) {
    setTimeout(() => console.log(i), 100);
}
```

9. **Modül Kapsamı Karışıklığı**
```javascript
// Hatalı
window.globalVar = 'value';

// Doğru
export const moduleVar = 'value';
```

10. **İç İçe Kapsamlarda Değişken Gölgeleme**
```javascript
// Hatalı
const value = 5;
function test() {
    const value = 10;
    console.log(value); // 10
}

// Doğru - Farklı isimler kullan
const globalValue = 5;
function test() {
    const localValue = 10;
    console.log(localValue);
}
```

## Tip ve Karşılaştırma Hataları (11-20)

11. **Gevşek Eşitlik Kontrolü**
```javascript
// Hatalı
if (5 == "5") {}

// Doğru
if (5 === "5") {}
```

12. **Tip Dönüşümü Hataları**
```javascript
// Hatalı
const num = "5" + 2; // "52"

// Doğru
const num = Number("5") + 2; // 7
```

13. **Boolean Dönüşüm Hataları**
```javascript
// Hatalı
if (someValue) {}

// Doğru
if (Boolean(someValue)) {}
// veya
if (!!someValue) {}
```

14. **NaN Kontrolü**
```javascript
// Hatalı
if (x === NaN) {}

// Doğru
if (isNaN(x)) {}
// veya daha iyi
if (Number.isNaN(x)) {}
```

15. **Undefined Kontrolü**
```javascript
// Hatalı
if (x === undefined) {}

// Doğru
if (typeof x === 'undefined') {}
```

16. **Null Kontrolü**
```javascript
// Hatalı
if (x === null || x === undefined) {}

// Doğru
if (x == null) {}
```

17. **Array.isArray Kullanmama**
```javascript
// Hatalı
if (typeof arr === 'object') {}

// Doğru
if (Array.isArray(arr)) {}
```

18. **instanceof Yanlış Kullanımı**
```javascript
// Hatalı
if (obj.constructor === Array) {}

// Doğru
if (obj instanceof Array) {}
```

19. **Tip Güvenliği Olmayan Fonksiyonlar**
```typescript
// Hatalı
function process(value) {
    return value.length;
}

// Doğru
function process(value: string | Array<any>): number {
    return value.length;
}
```

20. **Union Types Hataları**
```typescript
// Hatalı
function handle(value: string | number) {
    return value.length; // Error

// Doğru
function handle(value: string | number) {
    if (typeof value === 'string') {
        return value.length;
    }
    return value.toString().length;
}
```

## Fonksiyon Hataları (21-30)

21. **this Bağlamı Kaybı**
```javascript
// Hatalı
const obj = {
    value: 42,
    getValue: function() {
        setTimeout(function() {
            console.log(this.value);
        });
    }
};

// Doğru
const obj = {
    value: 42,
    getValue: function() {
        setTimeout(() => {
            console.log(this.value);
        });
    }
};
```

22. **Arguments Nesnesine Güvenme**
```javascript
// Hatalı
function sum() {
    return arguments[0] + arguments[1];
}

// Doğru
function sum(...args) {
    return args.reduce((a, b) => a + b, 0);
}
```

23. **Callback Hell**
```javascript
// Hatalı
getData(function(a) {
    getMoreData(a, function(b) {
        getMoreData(b, function(c) {
            console.log(c);
        });
    });
});

// Doğru
async function getAllData() {
    const a = await getData();
    const b = await getMoreData(a);
    const c = await getMoreData(b);
    console.log(c);
}
```

24. **Return Eksikliği**
```javascript
// Hatalı
function calculate(a, b) {
    const result = a + b;
}

// Doğru
function calculate(a, b) {
    return a + b;
}
```

25. **Parametre Varsayılan Değerleri**
```javascript
// Hatalı
function greet(name) {
    name = name || 'User';
    console.log(`Hello ${name}`);
}

// Doğru
function greet(name = 'User') {
    console.log(`Hello ${name}`);
}
```

26. **Fonksiyon Overloading Hataları**
```typescript
// Hatalı
function process(x: number): number;
function process(x: string): string;
function process(x: any): any {
    return x;
}

// Doğru
function process<T extends string | number>(x: T): T {
    return x;
}
```

27. **Pure Function İhlali**
```javascript
// Hatalı
let total = 0;
function add(x) {
    total += x;
    return total;
}

// Doğru
function add(total, x) {
    return total + x;
}
```

28. **Recursive Fonksiyon Base Case Eksikliği**
```javascript
// Hatalı
function factorial(n) {
    return n * factorial(n - 1);
}

// Doğru
function factorial(n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```

29. **Generator Fonksiyon Hataları**
```javascript
// Hatalı
function* generator() {
    yield 1;
    return 2; // Son değer kayboluyor
}

// Doğru
function* generator() {
    yield 1;
    yield 2;
}
```

30. **Asenkron Fonksiyon İsimlendirmesi**
```javascript
// Hatalı
async function getData() {
    return await fetchData();
}

// Doğru
async function fetchUserData() {
    return await fetchData();
}
```

## Nesne ve Prototip Hataları (31-40)

31. **Prototip Zinciri Değiştirme**
```javascript
// Hatalı
obj.__proto__ = someOtherObj;

// Doğru
Object.setPrototypeOf(obj, someOtherObj);
```

32. **Object Property Tanımlama**
```javascript
// Hatalı
obj.newProp = value;

// Doğru
Object.defineProperty(obj, 'newProp', {
    value: value,
    writable: true,
    enumerable: true,
    configurable: true
});
```

33. **Shallow Copy vs Deep Copy**
```javascript
// Hatalı - Shallow copy
const newObj = Object.assign({}, oldObj);

// Doğru - Deep copy
const newObj = JSON.parse(JSON.stringify(oldObj));
// veya
const newObj = structuredClone(oldObj);
```

34. **Nesne Karşılaştırma**
```javascript
// Hatalı
const isEqual = obj1 === obj2;

// Doğru
const isEqual = JSON.stringify(obj1) === JSON.stringify(obj2);
```

35. **Property Existence Check**
```javascript
// Hatalı
if (obj.prop !== undefined) {}

// Doğru
if (Object.prototype.hasOwnProperty.call(obj, 'prop')) {}
```

36. **Object Freeze vs Seal**
```javascript
// Hatalı
Object.seal(obj); // Sadece yeni property eklemeyi engeller

// Doğru
Object.freeze(obj); // Tüm değişiklikleri engeller
```

37. **Method Shorthand Syntax**
```javascript
// Hatalı
const obj = {
    method: function() {}
};

// Doğru
const obj = {
    method() {}
};
```

38. **Computed Property Names**
```javascript
// Hatalı
const obj = {};
obj[dynamicKey] = value;

// Doğru
const obj = {
    [dynamicKey]: value
};
```

39. **Private Fields**
```javascript
// Hatalı
class Example {
    private value; // TypeScript private
}

// Doğru
class Example {
    #value; // JavaScript private field
}
```

40. **Static Method Inheritance**
```javascript
// Hatalı
class Child extends Parent {
    static method() {
        return super.method();
    }
}

// Doğru
class Child extends Parent {
    static method() {
        return Parent.method();
    }
}
```

## Dizi Hataları (41-50)

41. **Array Modifikasyon**
```javascript
// Hatalı
const arr = [1, 2, 3];
arr.push(4);

// Doğru
const newArr = [...arr, 4];
```

42. **Array.length Kullanımı**
```javascript
// Hatalı
const arr = [1, 2, 3];
arr.length = 2; // Diziyi kırpar

// Doğru
const newArr = arr.slice(0, 2);
```

43. **Array Boşaltma**
```javascript
// Hatalı
arr = [];

// Doğru
arr.length = 0;
// veya
arr.splice(0);
```

44. **indexOf ile Tip Kontrolü**
```javascript
// Hatalı
if (arr.indexOf(value) === -1) {}

// Doğru
if (!arr.includes(value)) {}
```

45. **Array to Object Dönüşümü**
```javascript
// Hatalı
const obj = {};
arr.forEach((item, index) => obj[index] = item);

// Doğru
const obj = Object.fromEntries(arr.map((item, index) => [index, item]));
```

46. **Array Filtreleme**
```javascript
// Hatalı
const filtered = [];
for (let item of arr) {
    if (condition) filtered.push(item);
}

// Doğru
const filtered = arr.filter(item => condition);
```

47. **Array Map Zincirleme**
```javascript
// Hatalı
arr.map().filter().reduce();

// Doğru
arr.reduce((acc, item) => {
    // Tek geçişte işlem
});
```

48. **Array Destructuring**
```javascript
// Hatalı
const first = arr[0];
const second = arr[1];

// Doğru
const [first, second] = arr;
```

49. **Sparse Array**
```javascript
// Hatalı
const arr = new Array(3);

// Doğru
const arr = Array(3).fill(null);
```

50. **Array-like Objects**
```javascript
// Hatalı
function func() {
    return arguments.map();
}

// Doğru
function func() {
    return Array.from(arguments).map();
}
```

## Asenkron Programlama Hataları (51-60)

51. **Promise Chain Kesme**
```javascript
// Hatalı
promise.then(data => {
    processData(data);
}).catch(err => {
    console.error(err);
});

// Doğru
promise
    .then(data => processData(data))
    .catch(err => console.error(err));
```

52. **async/await Hata Yakalama**
```javascript
// Hatalı
async function getData() {
    const data = await fetch('/api');
    return data;
}

// Doğru
async function getData() {
    try {
        const data = await fetch('/api');
        return data;
    } catch (error) {
        console.error(error);
        throw error;
    }
}
```

53. **Promise.all Kullanımı**
```javascript
// Hatalı
for (const item of items) {
    await processItem(item);
}

// Doğru
await Promise.all(items.map(item => processItem(item)));
```

54. **Race Condition**
```javascript
// Hatalı
let data;
fetch('/api').then(res => data = res);

// Doğru
const data = await fetch('/api');
```

55. **Promise Executor Hataları**
```javascript
// Hatalı
const promise = new Promise(() => {
    doSomething();
    throw new Error();
});

// Doğru
const promise = new Promise((resolve, reject) => {
    try {
        doSomething();
        resolve();
    } catch (error) {
        reject(error);
    }
});
```

56. **Promise Reject Sonrası İşlem**
```javascript
// Hatalı
promise.catch(error => {
    handleError(error);
    doMoreWork(); // Hata sonrası çalışır
});

// Doğru
promise
    .catch(error => {
        handleError(error);
        return Promise.reject(error); // Zinciri keser
    })
    .then(() => doMoreWork());
```

57. **async/await Loop**
```javascript
// Hatalı
async function processArray(arr) {
    arr.forEach(async (item) => {
        await processItem(item);
    });
}

// Doğru
async function processArray(arr) {
    for (const item of arr) {
        await processItem(item);
    }
}
```

58. **Promise.race Timeout**
```javascript
// Hatalı
fetch('/api');

// Doğru
Promise.race([
    fetch('/api'),
    new Promise((_, reject) => 
        setTimeout(() => reject(new Error('Timeout')), 5000)
    )
]);
```

59. **Asenkron İşlem Sıralama**
```javascript
// Hatalı
const results = [];
urls.forEach(async url => {
    const data = await fetch(url);
    results.push(data);
});

// Doğru
const results = await Promise.all(
    urls.map(url => fetch(url))
);
```

60. **Event Loop Bloklaması**
```javascript
// Hatalı
function heavyOperation() {
    while(condition) {
        // Uzun işlem
    }
}

// Doğru
async function heavyOperation() {
    while(condition) {
        await new Promise(resolve => setTimeout(resolve, 0));
        // İşlem parçası
    }
}
```

## DOM ve Event Hataları (61-70)

61. **Event Listener Memory Leak**
```javascript
// Hatalı
element.addEventListener('click', () => {});

// Doğru
const handler = () => {};
element.addEventListener('click', handler);
// Kullanım bittiğinde
element.removeEventListener('click', handler);
```

62. **innerHTML Güvenlik Riski**
```javascript
// Hatalı
element.innerHTML = userInput;

// Doğru
element.textContent = userInput;
```

63. **Event Delegation**
```javascript
// Hatalı
document.querySelectorAll('.item').forEach(item => {
    item.addEventListener('click', handler);
});

// Doğru
document.querySelector('.container').addEventListener('click', e => {
    if (e.target.matches('.item')) {
        handler(e);
    }
});
```

64. **DOM Traversal**
```javascript
// Hatalı
element.parentElement.parentElement;

// Doğru
element.closest('.target-class');
```

65. **setAttribute vs className**
```javascript
// Hatalı
element.setAttribute('class', 'new-class');

// Doğru
element.classList.add('new-class');
```

66. **Event Default Prevention**
```javascript
// Hatalı
function handler() {
    return false;
}

// Doğru
function handler(e) {
    e.preventDefault();
}
```

67. **DOM Element Oluşturma**
```javascript
// Hatalı
const div = document.createElement('div');
div.innerHTML = '<span>Text</span>';

// Doğru
const span = document.createElement('span');
span.textContent = 'Text';
div.appendChild(span);
```

68. **Event Bubbling**
```javascript
// Hatalı
element.addEventListener('click', e => {
    e.stopPropagation(); // Her zaman
});

// Doğru
element.addEventListener('click', e => {
    if (shouldStopPropagation) {
        e.stopPropagation();
    }
});
```

69. **DOM Query Performansı**
```javascript
// Hatalı
for (let i = 0; i < 1000; i++) {
    document.querySelector('.item');
}

// Doğru
const item = document.querySelector('.item');
for (let i = 0; i < 1000; i++) {
    // item kullanımı
}
```

70. **window.onload vs DOMContentLoaded**
```javascript
// Hatalı
window.onload = () => {};

// Doğru
document.addEventListener('DOMContentLoaded', () => {});
```

## TypeScript Spesifik Hatalar (71-80)

71. **any Tipini Aşırı Kullanma**
```typescript
// Hatalı
function process(data: any) {
    return data.someProperty;
}

// Doğru
interface Data {
    someProperty: string;
}
function process(data: Data) {
    return data.someProperty;
}
```

72. **Interface vs Type**
```typescript
// Hatalı
type User = {
    name: string;
}
type User = {
    age: number;
} // Hata

// Doğru
interface User {
    name: string;
}
interface User {
    age: number;
} // Birleşir
```

73. **Generic Constraints**
```typescript
// Hatalı
function getLength<T>(arr: T) {
    return arr.length; // Hata
}

// Doğru
function getLength<T extends { length: number }>(arr: T) {
    return arr.length;
}
```

74. **Nullable Tip Kontrolü**
```typescript
// Hatalı
function process(value: string | null) {
    return value.toUpperCase();
}

// Doğru
function process(value: string | null) {
    return value?.toUpperCase() ?? '';
}
```

75. **Readonly Kullanımı**
```typescript
// Hatalı
interface Config {
    api: string;
}

// Doğru
interface Config {
    readonly api: string;
}
```

76. **Type Guard**
```typescript
// Hatalı
function process(value: string | number) {
    if (typeof value === 'string') {
        value.toUpperCase();
    }
    value.toUpperCase(); // Hata
}

// Doğru
function process(value: string | number) {
    if (typeof value === 'string') {
        value.toUpperCase(); // OK
    }
}
```

77. **Utility Types**
```typescript
// Hatalı
interface PartialUser {
    name?: string;
    age?: number;
}

// Doğru
interface User {
    name: string;
    age: number;
}
type PartialUser = Partial<User>;
```

78. **keyof Kullanımı**
```typescript
// Hatalı
function getProperty(obj: object, key: string) {
    return obj[key]; // Hata
}

// Doğru
function getProperty<T, K extends keyof T>(obj: T, key: K) {
    return obj[key];
}
```

79. **Index Signatures**
```typescript
// Hatalı
interface StringMap {
    [key: string]: string;
    length: number; // Hata
}

// Doğru
interface StringMap {
    [key: string]: string | number;
    length: number;
}
```

80. **Conditional Types**
```typescript
// Hatalı
type MessageOf<T> = T['message'];

// Doğru
type MessageOf<T> = T extends { message: unknown } 
    ? T['message'] 
    : never;
```

## Performans Hataları (81-90)

81. **Gereksiz Re-render**
```javascript
// Hatalı
function Component() {
    const [count, setCount] = useState(0);
    const data = expensiveCalculation();
    return <div>{data}</div>;
}

// Doğru
function Component() {
    const [count, setCount] = useState(0);
    const data = useMemo(() => expensiveCalculation(), []);
    return <div>{data}</div>;
}
```

82. **Memory Leak**
```javascript
// Hatalı
setInterval(() => {
    // Sürekli çalışır
}, 1000);

// Doğru
const interval = setInterval(() => {
    // İşlem
}, 1000);
cleanup(() => clearInterval(interval));
```

83. **Layout Thrashing**
```javascript
// Hatalı
elements.forEach(el => {
    const height = el.offsetHeight;
    el.style.height = `${height * 2}px`;
});

// Doğru
const heights = elements.map(el => el.offsetHeight);
elements.forEach((el, i) => {
    el.style.height = `${heights[i] * 2}px`;
});
```

84. **Bundle Size**
```javascript
// Hatalı
import { everything } from 'lodash';

// Doğru
import map from 'lodash/map';
```

85. **Mikro-optimizasyon**
```javascript
// Hatalı
for (let i = 0; i < arr.length; i++) {}

// Doğru
const len = arr.length;
for (let i = 0; i < len; i++) {}
```

86. **CSS Animation vs JS Animation**
```javascript
// Hatalı
setInterval(() => {
    element.style.left = `${position++}px`;
}, 16);

// Doğru
element.style.transition = 'left 1s';
element.style.left = '100px';
```

87. **Event Handler Throttling**
```javascript
// Hatalı
window.addEventListener('scroll', handler);

// Doğru
window.addEventListener('scroll', _.throttle(handler, 100));
```

88. **String Concatenation**
```javascript
// Hatalı
let str = '';
for (let i = 0; i < 1000; i++) {
    str += i;
}

// Doğru
const arr = [];
for (let i = 0; i < 1000; i++) {
    arr.push(i);
}
const str = arr.join('');
```

89. **Recursive setTimeout**
```javascript
// Hatalı
setInterval(() => {
    heavyOperation();
}, 1000);

// Doğru
function schedule() {
    setTimeout(() => {
        heavyOperation();
        schedule();
    }, 1000);
}
```

90. **Web Worker Kullanımı**
```javascript
// Hatalı
function heavyCalculation() {
    // Ana thread'i bloklar
}

// Doğru
const worker = new Worker('worker.js');
worker.postMessage(data);
```

## Güvenlik ve İyi Pratikler (91-100)

91. **eval() Kullanımı**
```javascript
// Hatalı
eval(userInput);

// Doğru
// Güvenli alternatif yöntem kullan
Function(`"use strict";return (${userInput})`)();
```

92. **XSS Korunması**
```javascript
// Hatalı
div.innerHTML = userInput;

// Doğru
div.textContent = userInput;
```

93. **Prototype Pollution**
```javascript
// Hatalı
Object.assign(target, source);

// Doğru
const sanitizedSource = JSON.parse(JSON.stringify(source));
Object.assign(target, sanitizedSource);
```

94. **Secure Headers**
```javascript
// Hatalı
fetch(url);

// Doğru
fetch(url, {
    headers: {
        'Content-Security-Policy': "default-src 'self'",
    }
});
```

95. **CSRF Koruması**
```javascript
// Hatalı
fetch('/api/data', { method: 'POST' });

// Doğru
fetch('/api/data', {
    method: 'POST',
    headers: {
        'X-CSRF-Token': csrfToken
    }
});
```

96. **Sensitive Data Exposure**
```javascript
// Hatalı
console.log(password);

// Doğru
// Hassas veriyi loglama
```

97. **Regular Expression DoS**
```javascript
// Hatalı
/^(a+)+$/

// Doğru
/^[a]+$/
```

98. **Error Object Exposure**
```javascript
// Hatalı
app.use((err, req, res, next) => {
    res.json(err);
});

// Doğru
app.use((err, req, res, next) => {
    res.json({ message: 'An error occurred' });
    console.error(err);
});
```

99. **Path Traversal**
```javascript
// Hatalı
fs.readFile(userInput);

// Doğru
const safePath = path.normalize(userInput).replace(/^(\.\.[\/\\])+/, '');
fs.readFile(safePath);
```

100. **Secure Random Values**
```javascript
// Hatalı
Math.random();

// Doğru
crypto.getRandomValues(new Uint8Array(16));
```
