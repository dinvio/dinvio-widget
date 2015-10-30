# Dinvio Виджет для корзины

## Демо
https://dinvio.github.io/dinvio-widget/

## Требования
Для установки виджета не требуется никаких дополнительных библиотек.

Поддержка браузерами: IE9+


## Подключение виджета
```js
var widget = new DinvioWidget(widgetPlace, {
    publicKey: ...
});
```
где
`widgetPlace` — id элемента, или сам DOM-элемент, куда будет встроен виджет,
`publicKey` — публичный ключ API


## Методы
### Данные отправления
```js
widget.setParcelData(packages, totalCost)
```
Сообщает виджету данные об отправлении.
`packages` — массив коробок:
```js
[
    {
        weight: ...,    // Вес коробки в килограммах
        length: ...,    // Длина в сантиметрах
        width: ...,     // Ширина в сантиметрах
        height: ...,    // Высота в сантиметрах
    },
    ...
]
```
`totalCost` — объявленная стоимость отправления в рублях

### Адрес получателя
```js
widget.setDestination(destination)
```
Сообщает виджету адрес получения
`destination` — полный адрес получения посылки в свободной форме (например: "Москва серебряническая набережная 29"


### Расчет стоиомсти
```js
widget.calc()
```
Запускает процесс расчета стоимости.
Этот метод будет вызван автоматически при вызове `widget.setDestination(...)` или `widget.setParcelData(...)`

### Получение иформации о выбранном варианте доставки
`widget.getSelectedVariant()` — получить данные по выбранному способу доставки
`widget.getRequestId()` — получить requestId для данного расчета. Для последующей регистрации заказа по API

## События
`select` — вызывается, при выборе варианта доставки
```js
widget.on('select', function() {
    console.log(widget.getSelectedVariant());
});
```