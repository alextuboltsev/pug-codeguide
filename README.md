# Кодгайд по шаблонизатору Pug

## Синтаксис

* ### Для отступов используются 2 пробела
* ### Классы и id записываются через `.` и `#` соответственно, а не внутри скобок
  ```pug
    // Неверно:
    input(class="field" id="user-name" type="text)


    // Верно:
    input.field#user-name(type="text)
  ```
* ### Название тега `div` опускается, если у него есть статичный класс или id
  ```pug
  // Неверно:
  div.container

  // Верно:
  .container
  ```
* ### Для значений атрибутов и строковых переменных используются двойные кавычки
* ### Атрибуты разделяются запятыми
* ### Имена тегов и названия атрибутов записаны строчными буквами
  ```pug
  // Неверно:
  INPUT(Type="number")


  // Верно:
  input(type="number")
  ```
* ### Отсутствуют пробелы вокруг скобок атрибутов и знака `=`
  ```pug
  // Неверно:
  form( method = "POST" )


  // Верно:
  form(method="POST")
  ```

* ### Имена переменных и миксинов записываются в нотации camelCase
* ### Имена файлов записываются строчными буквами в нотации kebab-case
  __Например:__ `input-range.pug`
  
## Порядок атрибутов
* ### Статичные имена классов и id записываются перед блоком атрибутов, а не после
  ```pug
  // Неверно:
  input(type="text", maxlength="10").field#user-name


  // Верно:
  input.field#user-name(type="text", maxlength="10")
  ```
* ### При перечислении атрибутов первым пишется класс
  ```pug
  // Неверно:
  a(href="#", class=className)


  // Верно:
  a(class=className, href="#")
  ```

## Структура
* ### Переменные перечисляются в начале файла
* ### Для вывода повторяющихся блоков используется цикл `each`
  ```pug
  // Неверно:
  ul.menu
    li.menu__item
      a.menu__link(href="#") Главная
    li.menu__item
      a.menu__link(href="#") О компании
    li.menu__item
      a.menu__link(href="#") Контакты
    li.menu__item
      a.menu__link(href="#") Оформить заказ


  // Верно:
  -
    var menu = [
      "Главная",
      "О компании",
      "Контакты",
      "Оформить заказ"
    ]
      
  ul.menu
    each item in menu
      li.menu__item
        a.menu__link(href="#")= item
  ```
