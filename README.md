# Тестовое задание на позицию javascrpt разработчик (frontend)

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

Универсальное решение с тестами. При вызове данной функции в качестве второго параметра указывается массив с набором скобок, по которым будет проводиться анализ синтаксической верности. Так же если не указывать этот параметр при вызове, то сработает значение параметра по умолчанию с наьором скобок <,[,{,(

```js
"use strict";

function checkSyntax(string, spaples = ['()', '{}', '[]', '<>']) {
    let openStaples = new Array();
    let closeStaples = new Array();
    let arrSpaples = new Array();
    for (let i = 0; i < spaples.length; i++) {
        openStaples.push(spaples[i][0]);
        closeStaples.push(spaples[i][1]);
    }
    openStaples = openStaples.join();
    closeStaples = closeStaples.join();
    for (let i = 0; i < string.length; i++) {
            if (closeStaples.includes(string[i])) {
                if (arrSpaples.length < 1) {
                    return 1;
                } else if (string[i] == arrSpaples[arrSpaples.length - 1]){
                    arrSpaples.pop();
                }
            } else if (openStaples.includes(string[i])) {
                if (string[i] == '(') arrSpaples.push(')');
                if (string[i] == '<') arrSpaples.push('>');
                if (string[i] == '[') arrSpaples.push(']');
                if (string[i] == '{') arrSpaples.push('}');
            }
    }
    if (arrSpaples.length < 1) {
        return 0;
    } else return 1
}

console.log(checkSyntax("---(++++)----", ['()', '{}']));
console.log(checkSyntax(""));
console.log(checkSyntax("before ( middle [] after ", ['[]']));
console.log(checkSyntax(") ("), ['<>', '{}', '[]']);
console.log(checkSyntax("} {"));
console.log(checkSyntax("<(   >)"));
console.log(checkSyntax("(  [  <>  ()  ]  <>  )", ['<>', '{}']));
console.log(checkSyntax("   (      [)"));
```

## Алгоритмы
### Задача №1
Реализовать функцию, на вход которой передаются 
* массив целых чисел, упорядоченных по возрастанию,
* целое число.
Функция должна найти 2 числа в массиве, которые в сумме дают переданное вторым параметром число и вернуть их индексы. Если таких чисел нет, то функция должна вернуть пустой объект или массив.

Постарайтесь решить данную задачу наиболее оптимальным способом с наименьшим количество итераций. Также, пожалуйста, опишите ваш алгоритм.

#### Решение 
Код решения с примером вызова функции.

```js
"use strict";

function indexOfSum(arr, numSum) {
    let indexArr = new Array;
    for (let i = 0; i < arr.length - 1; i++) {
            if ((arr[i] <= numSum) || (arr[i] < 0)){
                for (let j = i + 1; j < arr.length; j++) {
                    if (arr[i] + arr[j] == numSum) {
                        indexArr.push(i);
                        indexArr.push(j);
                        return indexArr;
                    } else if (arr[i] + arr[j] > numSum) {
                        break;
                    }
                }
            } else {
                return indexArr;
            }
    }
    return indexArr;
}

console.log(indexOfSum([0, 1, 5, 9], 10));
```

Описание алгоритма: На вход в функцию поступает массив из целых упорядоченых по возврастанию чисел ```arr``` и целое число  ```numSum```. Функция ищет два числа, сумма которых равна целому числу, которое пришло на вход функции, и возвращает массив состоящий из индексов этих элементов массива. 

Алгорит состоит из двух циклов ```for``` вложенных друг в друга. Первый цикл "проходит" по всему массиву исключая последний элемент. Вложенный цикл "идёт" от следующего элемента, на котором в данный момент находиться первый цикл и до последнего. 
Перед вторым вложенным циклом выполняется проверка условия: ```((arr[i] <= numSum) || (arr[i] < 0))```, так как если элемент массива (!)положительный и он больше контрольной суммы ```numSum```, то нам нет смысла идти по вложенному циклу и проверять условие ```(arr[i] + arr[j] == numSum)```, так как все последующие суммы всегда будут больше конрольной и мы можем возвращать массив индексов ```indexArr``` и выходить из функции. Но если число отрицательное, то условие ```(arr[i] <= numSum)``` может не выполняться. 
Во вложенном цикле мы проверяем сумму элементов по первому итератору и второму итератору на равенство контрольной сумме. Если они равны ей, то добывляем индексы этих элементов в массив индексов и выходим из функции возвратив массив индексов. Также в этом цикле выполняется проверка условия ```(arr[i] + arr[j] == numSum)```, так как если элементов массива больше контрольной, то дальше идти по второму циклу бесмысленно, так как дальше она будет только увеличиваться и все последующие суммы уже точно не равны контрольной, поэтому мы останавливаем выполнение вложенного цикла и сразу переходим на следующую итерацию внешнего цикла. Далее всё повтроряется пока не встретяться два элемента массива в сумме дающих контрольную сумму или не законцаться итерации циклов, не найдя нужную нам сумму и вернув пустой массив.

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

#### Решение 
Можно предложить несколько решений. 

Первый вариант описать класс ```Url```. В функции ```parseUrl(string)``` описать алгоритм парсинга строки на составные данные и создать объект класса ```Url``` и вернуть этот объект при выходе из функции. Данное решение с тестами представлено ниже.

```js
"use strict";

class Url {
    constructor(href, hash, host, port, protocol, hostname, pathname, origin) {
        this.href = href;
        this.hash = hash;
        this.port = port;
        this.host = host;
        this.protocol = protocol;
        this.hostname = hostname;
        this.pathname = pathname;
        this.origin = origin;
    }
}

function parseUrl(string) {
    let hash = '#' + string.split('#')[1];
    let host = string.split('/')[2];
    let port = host.split(':')[1];
    let protocol = string.split('/')[0];
    let hostname = host.split(':')[0];
    let origin = protocol + '//' + host;
    let pathname = string.split('?')[0].replace(origin, '');
    if (string.split('#')[1] == undefined) hash = '';
    if (host.split(':')[1] == undefined) port = '';
    let url = new Url(string, hash, host, port, protocol, hostname, pathname, origin);
    return url 
}

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

Второй вариант описать класс ```Url``` с конструктором ```constructor(href)``` и описать весь алгоритм парсинга на составные данные в нём. В функции ```parseUrl(string)``` создать объект класса ```Url``` и вернуть этот объект при выходе из функции. Данное решение с тестами представлено ниже.

```js
"use strict";

class Url {
    href
    hash
    host
    port
    protocol
    hostname
    pathname
    origin

    constructor(href) {
        this.href = href;
        this.hash = '#' + href.split('#')[1];
        this.host = href.split('/')[2];
        this.port = this.host.split(':')[1];
        this.protocol = href.split('/')[0];
        this.hostname = this.host.split(':')[0];
        this.origin = this.protocol + '//' + this.host;
        this.pathname = href.split('?')[0].replace(this.origin, '');
        if (this.href.split('#')[1] == undefined) this.hash = '';
        if (this.host.split(':')[1] == undefined) this.port = '';
    }
}

function parseUrl(string) {
    let url = new Url(string);
    return url 
}

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

Возможных вариантов реализации данной задачи присутствует множество (в том числе реализация функции ```parseUrl(string)``` в качестве метода класса ```Url```). Выбирать какой-то конкретный вариант нужно исходя из наших потребностей. 

##Комментарии
Если предложенные мною решения имеют баги и ошибки, а также есть замечания по оформлению, то в оставшееся время выделенное на выполнение тестового задания могу делать правки.
