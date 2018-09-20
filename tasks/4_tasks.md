# jQuery Basics

## Chapter 4. Working with properties, attributes, and data

### 4.1 Defining element properties and attributes

1. Опишите особенности DOM-свойств и атрибутов HTML
- Чем отличаются свойства и атрибуты элементов?
    Атрибуты задаются в html и после формирования DOM на их основе создаются свойства DOM-элементов.
    Атрибуты: содержат только строки, не чувствительны к регистру, видны в innerHTML
    Свойства: содержат любые значения, регистрозависимы, не видны в innerHTML.
    
- Как они синхронизируются между собой (строки, булевы значения, цифры)?
    Изменение аттрибута отражается на свойстве всегда.
    Изменение свойства не всегда изменяет аттрибут.

- Каковы особенности именования атрибутов и соответствующих им свойств?
    Аттрибуты - через дефис.
    Свойства - кэмелкейсом.

- Приведите примеры, когда нужно работать с атрибутами, а когда со свойствами?
    Аттрибуты: для получения изначального значения (можно также использовать `.defaultValue`)
    Свойства: для получения текущего значения

2. Что будет и почему
```html
<img src="../pic.png" alt="Picture" id="myPic">

<script>
    var img = document.getElementById('myPic');

    // Что будет и почему?
    console.log(img.src == img.getAttribute('src'));
</script>
```
    В результате будет `false`, т.к.:
    - в аттрибуте: относительная ссылка,
    - в свойстве: абсолютная ссылка.

3. Определите поддержку HTML5-атрибута
- Как определить, поддерживает ли браузер атрибут `draggable` у элементов?
    ```javascript
    if ('draggable' in document.createElement('elementName')) {
        console.log('supported');
    }
    ```

### 4.2 Working with attributes

1. Добавить `alt` для картинок

Добавьте картинкам атрибут `alt` на основании названия файла:

- замените - на пробел;
- первое слово должно начинаться с большой буквы

Пример: ../big-fish.jpg → Big fish.

Картинок может быть произвольное количество, путь к картинкам может быть любой. Существующие альты трогать не нужно.

```html
<img class="image" src="../big-fish.png">
<img class="image" src="../wild-lizard.png">
<img class="image" src="../melanholic-dinosaur.png">

<script>
    var images = $('.image');

    images.each(function(i, image) {
        var src = image.getAttribute('src'),
            // improve regExp
            r = /[^/\\]+(?:jpg|gif|png)/gi,
            value = src.match(r);

        console.log(value);

        image.setAttribute('alt', value);
        console.log(image.getAttribute('alt'));
    })
</script>
```

### 4.3 Manipulating element properties

1. Как чекнуть чекбокс из JS? Как узнать, чекнут ли чекбокс?

```javascript
$elem.prop('checked', true);


$elem.prop('checked') ? 'checked' : 'not checked';
```

2. Работа с атрибутом/свойством checked

```html
<input type="checkbox" checked id="myCheckBox">

<script>
    var $cb = $('#myCheckBox');
    
    console.log($cb.prop('checked'), $cb.attr('checked'));
    // true, 'checked'

    $cb.prop('checked', false);

    // Что будет и почему? 
    console.log($cb.prop('checked'), $cb.attr('checked'));
    // false, 'checked'
</script>
```

### 4.4 Storing custom data on elements
1. Вопросы
- Какие данные можно сохранять в data-* атрибутах?
- Как jQuery сохраняет и достает данные с помощью .data()? Опишите алгоритм работы.
- Чем отличаются $.data и $.fn.data?
- Как удалить данные, сохраненные в элементе через .data()?
- Как проверить, имеет ли элемент данные, сохраненные через .data()?

2. Что будет и почему
```html
<input type="checkbox" data-url="http://ya.ru" id="myCheckBox">

<script>
    var $cb = $('#myCheckBox');

    $cb.data('url', 'http://google.com');

    // Что будет и почему?
    console.log($cb.data('url') == $cb.attr('data-url'));
    // false

    $cb.removeData('url');

    // Что будет и почему?
    console.log($cb.attr('data-url'));
    // 'http://ya.ru'
</script>
```
