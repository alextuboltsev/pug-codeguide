# Кодгайд по шаблонизатору Pug

## Синтаксис

* ### Для отступов используются 2 пробела
* ### Статичные классы и id записываются через `.` и `#` соответственно, а не внутри скобок
  Ориентироваться в разметке легче, когда классы отделены от других атрибутов.\
  __Исключение__: атрибуты с вычисляемым значением
  ```pug
  // Неверно:
  div(class="container")
    div(class="content")
      form(class="form" method="POST" action="/")
        input(class="field" id="user-name" type="text)


  // Верно:
  .container
    .content
      form.form(method="POST" action="/")
        input.field#user-name(type="text)


  // Верно:
  // В значении конкатенируется строка и переменная, вынести атрибут за скобки не получится
  input(id="filter-color-" + index)    
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
  Атрибуты с явным разделителем легче считывать, особенно если в значениях использованы тернарные операторы или конкатенация.
  ```pug
  // Неверно:
  input(id="filter-option" + index type="checkbox" name="filter-option" value="one")

  // Верно:
  input(id="filter-option" + index, type="checkbox", name="filter-option", value="one")
  ```
* ### Имена тегов и названия атрибутов записаны строчными буквами
  ```pug
  // Неверно:
  INPUT(Type="number")


  // Верно:
  input(type="number")
  ```
* ### Атрибуты не отделяются пробелами от скобок. Также нет пробелов вокруг `=` в атрибутах 
  ```pug
  // Неверно:
  form( method = "POST" )


  // Верно:
  form(method="POST")
  ```

* ### Имена переменных и миксинов записываются в нотации camelCase
* ### Имена файлов записываются строчными буквами в нотации kebab-case
  __Например:__ `input-range.pug`
* ### При объявлении переменных всегда используется ключевое слово `var`. `var` и знак `=` отделяются пробелами с обеих сторон
  ```pug
  // Неверно:
  - className = "my-class
  -var className="my-class"

  // Верно:
  - var classNeme = "my-class"
  ```
 
## Порядок атрибутов
* ### Статичные имена классов и id записываются перед блоком атрибутов, а не после
  Ориентироваться в классах легче, когда они расположены в начале строки
  
  ```pug
  // Неверно:
  input(type="text", maxlength="10").field#user-name


  // Верно:
  input.field#user-name(type="text", maxlength="10")
  ```
* ### При перечислении атрибутов первым пишется класс
  ```pug
  // Неверно:
  p#unique-link.link-wrapper
   a(href="#", class=className)


  // Верно:
  p.link-wrapper#unique-link
    a(class=className, href="#")
  ```

## Структура
* ### Переменные перечисляются в начале файла
  __Исключение:__ Переменные, значение которых вычисляется внутри циклов или миксинов
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
