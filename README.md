# Callback-in-JS
# Callback в JavaScript

## Что такое Callback?
Callback (обратный вызов) — это функция, передаваемая в другую функцию в качестве аргумента, которая затем вызывается внутри этой функции для выполнения определённого действия.

## Зачем нужны Callback-функции?
Callback-функции позволяют выполнять код **асинхронно** и **упрощают обработку событий**. Они часто используются в обработчиках событий, асинхронных операциях (например, запросах к серверу) и других задачах, требующих отложенного выполнения кода.

## Методы работы с Callback

### 1. `setTimeout` — задержка выполнения
Позволяет выполнить функцию через определённое время.
```javascript
setTimeout(function() {
    console.log("Сообщение появится через 2 секунды");
}, 2000);
```

### 2. `setInterval` — повторение выполнения через интервалы
```javascript
let count = 0;
let interval = setInterval(function() {
    count++;
    console.log("Прошло", count, "секунд");
    if (count === 5) clearInterval(interval);
}, 1000);
```

### 3. `addEventListener` — обработка событий
```javascript
document.getElementById("myButton").addEventListener("click", function() {
    console.log("Кнопка нажата!");
});
```

### 4. `forEach` — перебор массива
```javascript
let numbers = [1, 2, 3, 4, 5];
numbers.forEach(function(num) {
    console.log("Число:", num);
});
```

### 5. `map` — создание нового массива
```javascript
let doubled = numbers.map(function(num) {
    return num * 2;
});
console.log(doubled);
```

### 6. `filter` — фильтрация массива
```javascript
let evenNumbers = numbers.filter(function(num) {
    return num % 2 === 0;
});
console.log(evenNumbers);
```

### 7. `reduce` — свёртка массива
```javascript
let sum = numbers.reduce(function(acc, num) {
    return acc + num;
}, 0);
console.log("Сумма:", sum);
```

### 8. Обработка ошибок в callback
```javascript
function fetchData(url, callback) {
    setTimeout(() => {
        if (!url) {
            callback("Ошибка: URL не указан", null);
        } else {
            callback(null, "Данные загружены с " + url);
        }
    }, 1000);
}

fetchData("https://example.com", function(error, data) {
    if (error) {
        console.log("Ошибка:", error);
    } else {
        console.log("Результат:", data);
    }
});
```

### 9. Последовательное выполнение задач с callback
```javascript
function step1(callback) {
    setTimeout(() => {
        console.log("Шаг 1 выполнен");
        callback();
    }, 1000);
}

function step2(callback) {
    setTimeout(() => {
        console.log("Шаг 2 выполнен");
        callback();
    }, 1000);
}

function step3(callback) {
    setTimeout(() => {
        console.log("Шаг 3 выполнен");
        callback();
    }, 1000);
}

step1(() => {
    step2(() => {
        step3(() => {
            console.log("Все шаги завершены");
        });
    });
});
```

## Проблема callback hell
Когда в коде много вложенных callback-функций, он становится трудно читаемым. Это называют **callback hell**:
```javascript
asyncFunction1(function(result1) {
    asyncFunction2(result1, function(result2) {
        asyncFunction3(result2, function(result3) {
            asyncFunction4(result3, function(finalResult) {
                console.log("Финальный результат:", finalResult);
            });
        });
    });
});
```

### Как избежать callback hell?
1. Использовать **Promise**:
```javascript
function asyncFunction() {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve("Завершено"), 1000);
    });
}

asyncFunction().then(result => console.log(result));
```

2. Использовать **async/await**:
```javascript
async function fetchData() {
    let response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
    let data = await response.json();
    console.log(data);
}
fetchData();
```

## Заключение
Callback-функции — важная часть JavaScript, позволяющая управлять асинхронными операциями. Однако при сложных сценариях лучше использовать `Promise` и `async/await`, чтобы избежать callback hell и улучшить читаемость кода.

