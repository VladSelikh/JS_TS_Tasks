# Задача (старое условие с правками)

## Класс Child

- создать класс `Child`, у которого есть 3 приватных свойства, отвечающие за его имя (строка), возраст (число) и пол (`"male"` или `"female"`). Конструктор должен принимать объект с 3 ключами: `name` (строка), `age` (число) и `gender` (`"male"` или `"female"`), и назначить свойствам соответствующие значения ключей данного объекта. Если передан возраст меньше 1 или больше 17, необходимо выбросить исключение с текстом `"Child's age should be in the range of 1-17 years"`
- создать геттеры для каждого из свойств

## Класс Person

- создать класс `Person`, у которого есть 3 приватных свойства: `name`, `surname` (строки), and `children` (массив экземпляров классов `Child`). конструктор должен принимать 2 аргумента: имя и фамилию, и назначать их соответствующим свойствам данного класса, а также назначить свойству `children` пустой массив
- создать метод `addChildren()`, который принимает неограниченное количество экземпляров класса `Child` и добавляет их в массив свойства `children`
- создать геттер `allChildren`, который должен возвращать строку в зависимости от того, сколько детей у `Person`, и сколько им лет:
  - `"I have no children!"`, если детей нет
  - `"My name is <имя>.<перенос троки>I have 1 child: <имя ребёнка> of <возраст ребёнка> year(s) old."`, если ребёнок только один
  - `"My name is <имя>.<перенос троки>I have <количество детей> children: <имя 1-го ребёнка> of <возраст 1-го ребёнка> year(s) old, <имя 2-го ребёнка> of <возраст 2-го ребёнка> year(s) old, ..."`, если детей больше 1
- Notes:
  - обрати внимание на то, что нужно поставить слово `"year"` во множественное число, если возраст больше 1 года
  - символ переноса строки - `"\n"`
- создать метод `getChildInfo()`, который принимает имя ребёнка и возвращает строку в формате `"This is <имя ребёнка> <фамилия ребёнка>. He/She is <возраст> year(s) old."`. Notes:
  - Фамилия ребёнка совпадает с именем его родителя
  - Подстрока `"He"` или `"She"` выводится в зависимости от пола ребёнка
  - Нужно поставить слово `"year"` во множественное число, если возраст больше 1 года
  - Если ребёнка с переданным именем нету в массиве `children`, необходимо выбросить исключение с текстом: `"<имя> is not my child!"`

## DEMO

```javascript
try {
  const Nastya = new Child({ name: "Nastya", age: 29, gender: "female"});
} catch(e) {
  console.log((e as Error).message)          // => Child's age should be in the range of 1-17 years
}

const Polina = new Child({ name: "Polina", age: 4, gender: "female"});
const Max = new Child({ name: "Max", age: 1, gender: "male"});
const Marina = new Child({ name: "Marina", age: 12, gender: "female"});
const Claire = new Child({ name: "Claire", age: 9, gender: "female"});

const person = new Person("Paul", "Andersen");

person.addChildren(Max, Marina, Claire);
person.addChildren(Polina);

console.log(person.allChildren);             // => My name is Paul.
// I have 4 children: Max of 1 year old, Marina of 12 years old, Claire of 9 years old, Polina of 4 years old!

try {
  console.log(person.getChildInfo('Chris'));
} catch(e) {
  console.log((e as Error).message)          // => Chris is not my child!
}

console.log(person.getChildInfo('Polina'));  // => This is Polina Andersen. She is 4 years old.
console.log(person.getChildInfo('Claire'));  // => This is Claire Andersen. She is 9 years old.
console.log(person.getChildInfo('Max'));     // => This is Max Andersen. He is 1 year old.
console.log(person.getChildInfo('Marina'));  // => This is Marina Andersen. She is 12 years old.
```

# Задача (новый функционал)

## Класс Child

- создать метод `increaseAge()`, который увеличивает возраст ребёнка на 1 год

## Класс Person

- создать метод `celebrateBirthday()` который принимает имя ребёнка, и увеличивает его возраст на 1 год (используя метод `increaseAge()` соответствующего экземпляра). Если ребёнка с переданным именем нету в массиве `children`, необходимо выбросить исключение с текстом: `"<имя> is not my child!"`

## DEMO

```javascript
console.log(person.getChildInfo('Max'));     // => This is Max Andersen. He is 1 year old.

person.celebrateBirthday('Max');

console.log(Max.age);                        // => 2
console.log(person.getChildInfo('Max'));     // => This is Max Andersen. He is 2 years old.

try {
  console.log(person.celebrateBirthday('Chris'));
} catch(e) {
  console.log((e as Error).message)          // => Chris is not my child!
}
```
