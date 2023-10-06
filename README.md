# Тестовое задание на позицию javascrpt разработчик (frontend)
При решении задания нельзя использовать готовые фреймворки и компоненты. Нас интересует как вы умеете решать подобные задачи и создавать что-то с нуля. Обратите внимание, во всех задачах отсутствует привязка к конкретному языку или к его особенностям, для нас важно ваше умение строить алгоритмы, реализовывать базовые функции и писать читаемый код.

## Базовые знания JS
### Задача №1
Написать функцию dscount, которая подсчитывает количество идущих подряд символов s1 и s2 в строке (кол-во цепочек s1s2), без учёта регистра. Функция должна пройти следующие тесты, как минимум:

```js
"use strict";

// Yor code here ...
Ваш код реализации функции dscount
// ... //

// Для удобства можно использовать эти тесты:
try {
    test(dscount, ['ab___ab__', 'a', 'b'], 2);
    test(dscount, ['___cd____', 'c', 'd'], 1);
    test(dscount, ['de_______', 'd', 'e'], 1);
    test(dscount, ['12_12__12', '1', '2'], 3);
    test(dscount, ['_ba______', 'a', 'b'], 0);
    test(dscount, ['_a__b____', 'a', 'b'], 0);
    test(dscount, ['-ab-аb-ab', 'a', 'b'], 2);
    test(dscount, ['aAa', 'a', 'a'], 2);

    console.info("Congratulations! All tests passed.");
} catch(e) {
    console.error(e);
}

// Простая функция тестирования
function test(call, args, count, n) {
    let r = (call.apply(n, args) === count);
    console.assert(r, `Found items count: ${count}`);
    if (!r) throw "Test failed!";
}
```
Данный код - для примера и не обязателен к использованию в таком виде. Можно вносить модификации.

Обратите внимание на производительность вашего решения.
Решение должно быть компактным.
Решение должно быть простым, умещаться в 1м файле и содержать не более 20 строк кода.

#### Решение 
Код решения вместе с тестами.

```js
"use strict";

// Функция
function dscount(string, s1, s2) {
    let count = 0;
    for (let i = 0; i < string.length - 1; i++) {
        if ((string[i].toLowerCase() == s1.toLocaleLowerCase()) && (string[i + 1].toLowerCase() == s2.toLocaleLowerCase())) {
            count++;
        }
    }
    return count;
}

// Тесты
try {
    test(dscount, ['ab___ab__', 'a', 'b'], 2);
    test(dscount, ['___cd____', 'c', 'd'], 1);
    test(dscount, ['de_______', 'd', 'e'], 1);
    test(dscount, ['12_12__12', '1', '2'], 3);
    test(dscount, ['_ba______', 'a', 'b'], 0);
    test(dscount, ['_a__b____', 'a', 'b'], 0);
    test(dscount, ['-ab-аb-ab', 'a', 'b'], 2);
    test(dscount, ['aAa', 'a', 'a'], 2);

    console.info("Congratulations! All tests passed.");
} catch(e) {
    console.error(e);
}

// Простая функция тестирования
function test(call, args, count, n) {
    let r = (call.apply(n, args) === count);
    console.assert(r, `Found items count: ${count}`);
    if (!r) throw "Test failed!";
}
```

### Задача №2
Реализовать функцию ```checkSyntax(string)```, проверяющую на синтаксическую верность последовательность скобок. Задача не сводится к простой проверке сбалансированности скобок. Нужно еще учитывать их последовательность (вложенность).

Обратите внимание на производительность вашего решения.
Решение должно быть компактным.
Решение должно быть простым, умещаться в 1м файле и содержать 20-30 строк кода или меньше.

Покажите решение, если нужно проверять следующий набор скобок: <,[,{,(

Изменится ли ваше решение, если нужно проверять только такой набор скобок: <,[,{

В случае ошибки возвращаем 1.
В остальных случаех возвращаем 0.
Тесты для 1го набора:
```js
checkSyntax("---(++++)----") == 0
checkSyntax("") -> 0
checkSyntax("before ( middle []) after ") == 0
checkSyntax(") (") == 1
checkSyntax("} {") == 1
checkSyntax("<(   >)") == 1
checkSyntax("(  [  <>  ()  ]  <>  )") == 0
checkSyntax("   (      [)") == 1
// и так далее...
```


#### Решение 
Решение и тесты, если нужно проверять следующий набор скобок: <,[,{,(

```js
"use strict";

function checkSyntax(string) {
    let arr = new Array();
    let openStaples = "<[{(", closeStaples = ">]})";
    for (let i = 0; i < string.length; i++) {
            if (closeStaples.includes(string[i])) {
                if (arr.length < 1) {
                    return 1;
                } else if (string[i] == arr[arr.length - 1]){
                    arr.pop();
                }
            } else if (openStaples.includes(string[i])) {
                if (string[i] == '(') arr.push(')');
                if (string[i] == '<') arr.push('>');
                if (string[i] == '[') arr.push(']');
                if (string[i] == '{') arr.push('}');
            }
    }
    if (arr.length < 1) {
        return 0;
    } else return 1
}

console.log(checkSyntax("---(++++)----"));
console.log(checkSyntax(""));
console.log(checkSyntax("before ( middle []) after "));
console.log(checkSyntax(") ("));
console.log(checkSyntax("} {"));
console.log(checkSyntax("<(   >)"));
console.log(checkSyntax("(  [  <>  ()  ]  <>  )"));
console.log(checkSyntax("   (      [)"));
```

Решение, если нужно проверять только такой набор скобок: <,[,{
```js
"use strict";

function checkSyntax(string) {
    let arr = new Array();
    let openStaples = "<[{", closeStaples = ">]}";
    for (let i = 0; i < string.length; i++) {
            if (closeStaples.includes(string[i])) {
                if (arr.length < 1) {
                    return 1;
                } else if (string[i] == arr[arr.length - 1]){
                    arr.pop();
                }
            } else if (openStaples.includes(string[i])) {
                if (string[i] == '<') arr.push('>');
                if (string[i] == '[') arr.push(']');
                if (string[i] == '{') arr.push('}');
            }
    }
    if (arr.length < 1) {
        return 0;
    } else return 1
}

console.log(checkSyntax("---(++++)----"));
console.log(checkSyntax(""));
console.log(checkSyntax("before ( middle []) after "));
console.log(checkSyntax(") ("));
console.log(checkSyntax("} {"));
console.log(checkSyntax("<(   >)"));
console.log(checkSyntax("(  [  <>  ()  ]  <>  )"));
console.log(checkSyntax("   (      [)"));
```

Решение изменилось взависимости от набора скобок. Поэтому на мой взгляд удобнее создать универсальное решение, код которого не изменится от набора скобок. Набор скобок можно передавать в качестве параметров при вызове функции. Данное решение является более ёмким по коду, но тогда функция будет проверять синтаксическую верность на набор скобок которые мы передадим ей в качестве параметров.


## Алгоритмы
### Задача №1
Реализовать функцию, на вход которой передаются 
* массив целых чисел, упорядоченных по возрастанию,
* целое число.
Функция должна найти 2 числа в массиве, которые в сумме дают переданное вторым параметром число и вернуть их индексы. Если таких чисел нет, то функция должна вернуть пустой объект или массив.

Постарайтесь решить данную задачу наиболее оптимальным способом с наименьшим количество итераций. Также, пожалуйста, опишите ваш алгоритм.

## Практические задачи
### Задача №1
Реализуйте функцию ```parseUrl(string)```, которая будет парсить URL строку и возвращать объект с распарсенными данными. Пример:

```js
let a = parseUrl('http://sys.it-co.ru:8080/do/any.php?a=1&b[]=a&b[]=b#foo')

// Вернет объект, в котором будут следующие свойства:
console.log( a.href == "http://sys.it-co.ru:8080/do/any.php?a=1&b[]=a&b[]=b#foo" )
console.log( a.hash == "#foo" )
console.log( a.port == "8080" )
console.log( a.host == "sys.it-co.ru:8080" )
console.log( a.protocol == "http:" )
console.log( a.hostname == "sys.it-co.ru" )
console.log( a.pathname == "/do/any.php" )
console.log( a.origin == "http://sys.it-co.ru:8080" )
```
## Комментарии
Результат выполнения задания нужно будет оформить здесь же, на гитхабе. В качестве ответа не нужно присылать никаких(!) ZIP архивов и наборов файлов. Все ваши ответы должны быть оформлены на https://github.com/ . Вы присылаете только ссылку на ваш репозиторий. У нас в компании применяется GIT, и если вы его не знаете, вам стоит освоить данную систему SCM самостоятельно. Если у вас еще нет аккаунта, то это хороший повод его завести.

Если есть вопросы, вы всегда их можете задать, связавшись с человеком, который выдал вам задание.
