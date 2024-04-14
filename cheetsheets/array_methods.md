# Методи **array []**
✅ ```let array1 = [];``` 👁‍🗨 ```let arr = new Array();```

## ❗❗❗ 
### У масивах можуть зберігатись елементи будь-якого типу
### В основі масивів — об’єкти
- ⛔ Додавання нечислових властивостей, таких як arr.test = 5.
- ⛔ Створення “дірок”, наприклад: arr[0] а за ним arr[1000] (та нічого між цими елементами).
- ⛔ Заповнення масиву в зворотньому порядку, наприклад: arr[1000], arr[999] і т. д.
- `typeof` не може відрізнити простий обʼєкт від масиву. `Array.isArray(value)` повертає true, якщо value – це масив, інакше false.
### Загальна кількість елементів масиву зберігається у його властивості `array1.length`. 
### Якщо змешити `array1.length`, масив стане коротшим. Цей процес незворотній.
### ⛔ ~~`fruits[-1]`~~ ✅ `fruits.at(-1)` 👁‍🗨 `fruits[fruits.length-1]`
### Якщо `let arr = new Array(2);` викликається з одним аргументом, а саме числом, він створить порожній масив з довжиною, яка дорівнює цьому числу.
### Масив toString повертає список елементів розділених комою. ```alert( arr ); // 1,2,3```
### [ ] в JS не варто порівнювати за допомогою оператора `==`
- Два об’єкти рівні == лише коли вони посилаються на один об’єкт.
- Якщо один з аргументів оператора == об’єкт, а інший — примітив, тоді об’єкт конвертується в примітив.

## Видалення і додавання елементів
Методи `push/pop` працюють швидко, на відміну від методів `shift/unshift`, які працюють повільно.
### Додавання
1. `array1.push(elementN)` [0,1,2,3,4] ⬅5
2. `array1.unshift(elementN)` 5➡ [0,1,2,3,4]
### Видалення
1. `array1.pop(elementN)` [0,1,2,3,4➡]
2. `array1.shift(elementN)` [⬅0,1,2,3,4]

### splice
`array1.splice(start, deleteCount?, itemToAddN?)` може додавати, видаляти і замінювати елементи. ⭕ Дозволяються відʼємні індекси
```
let arr = ["I", "study", "JavaScript", "right", "now"];

// видалимо 2 перших елементи
let removed = arr.splice(0, 2);

alert( removed ); // "I", "study" <-- повертає масив видалених елементів
```
Метод splice також може вставляти елементи без будь-яких видалень: `0` для `deleteCount`

## Повертають новий масив
### slice
`array1.slice(start?, end?)` повертає новий масив, копіюючи до нього всі елементи від індексу start до end (не включаючи end). Без аргументів. array1.slice() створить копію масиву array1

### concat
`concat(valueN?)` створює новий масив, в який копіює дані з інших масивів та додаткові значення. `arr.concat([3, 4], 5, 6)`
```
let arrayLike = {
  0: "something",
  //[Symbol.isConcatSpreadable]: true, - якщо обʼєкт має, то *1
  length: 1
};

alert( arr.concat(arrayLike) ); // 1,2,[object Object] *1: 1,2,something,else
```
## Перебір
### Цикли
`for..of` не надає доступу до індексу поточного елементу, тільки до його **значення**:
```
let fruits = ["Apple", "Orange", "Plum"];

for (let fruit of fruits) {
  alert( fruit );
}
```
`for` надає доступу до **індексу** поточного елементу, **значення**:
```
let arr = ["Apple", "Orange", "Pear"];

for (let i = 0; i < arr.length; i++) {
  alert( arr[i] );
}
```
Цикл `for..in` оптимізований для довільних об’єктів, не для масивів, і тому в 10-100 разів повільніше. Цикл `for..in` ітерується по всіх властивостях, не тільки по числових.

### forEach
1/`array1.forEach(callbackFn, thisArg?)`
```
["Hi", "learners", "~~"].forEach(alert);

["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
  alert(`${item} має позицію ${index} в масиві ${array}`);
});
```
###  Для обчислення якогось одного значення на основі всього масиву
1. `array1.reduce(callbackFn, initialValue?)`
```
let arr = [1, 2, 3, 4, 5];
let result = arr.reduce((sum, current) => sum + current, 0);
alert(result); // 15
```
2. `array1.reduceRight(callbackFn, initialValue?)` працює аналогічно `reduce`, але проходить по масиву справа наліво.

## Пошук в масиві
1. `arr.indexOf(searchElement, fromIndex?)` ➡ Number(елемент знайдено на позиції Number) : -1 (збігів не знайдено).
- indexOf використовує суворе порівняння ===. Таким чином, якщо ми шукаємо false, він знаходить саме false, але не нуль. 

2. `arr.includes(searchElement, fromIndex?)` ➡ true : false
``` 
alert( arr.indexOf(NaN) ); // -1 (повинен бути 0, але === перевірка на рівність не працює з NaN)
alert( arr.includes(NaN) );// true (вірно)
```
3. `arr.lastIndexOf(searchElement, fromIndex?)`
4. `array1.find(callbackFn, thisArg?)` ➡ перший елемент масиву, який задовольняє задану функцію тестування.
```
const array1 = [5, 12, 8, 130, 44];
const found = array1.find((element) => element > 10);
```
5. `array1.filter(callbackFn, thisArg?)` - поверхнева копія заданого масиву, що містить тільки ті елементи, які пройшли тест

## Перетворення масиву
1. `array1.map(callbackFn, thisArg?)` - викликає функцію для кожного елемента масиву і повертає масив результатів виконання цієї функції.
```
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
```
2. `array1.sort(compareFn?)` - повертає відсортований масив, але зазвичай повернене значення ігнорується, оскільки змінюється сам arr. <br>
**За замовчуванням елементи сортуються як рядки** <br>
`arr.sort(compareNumeric)` - як числа <br>
- 🔊 Краще використовувати стрілочні функції
- 🔊 localeCompare для рядків (Ö абощо..)
3. `array1.reverse()` - повертає масив array1 зі зміненим порядком елементів
4. `string1.split(separator, limit?)` - другий числовий аргумент – обмеження на кількість елементів в повернутому масиві. 
```
let arr = 'Вася, Петя, Маша, Іван'.split(', ', 2);
alert(arr); // Вася, Петя
```
5. `array1.join(separator?)` - створює рядок з елементів array1, вставляючи separator між ними.
```
let arr = ["Вася", "Петя", "Маша"];
let str = arr.join(';'); // обʼєднуємо масив в рядок за допомогою ";" Вася;Петя;Маша
```