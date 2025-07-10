---
id: quick-start-pams
title: Быстрый старт
sidebar_label: Быстрый старт
sidebar_position: 6
---

## Список типовых проектов

Для демонстрации функциональных возможностей микросхемы разработаны девять типовых проектов.
Проекты расположены в ПО DCS Electric в библиотеке `simulation`.

- Example 1 – Сдвоенный операционный усилитель общего применения.
- Example 2 – Сдвоенный компаратор общего применения со встроенным источником опорного напряжения.
- Example 3 – Компаратор общего применения со встроенным гистерезисом, источником опорного напряжения и операционным усилителем.
- Example 4 – Сдвоенный прецизионный операционный усилитель и операционный усилитель общего применения.
- Example 5 – Источник опорного напряжения для АЦП и ЦАП.
- Example 6 – Инструментальный усилитель.
- Example 7 – Двухканальный прецизионный предусилитель.
- Example 8 – Парафазный предусилитель–драйвер АЦП (схема тестируется).
- Example 9 – 3-х канальный линейный регулятор (схема тестируется).

## Запуск Example в режиме «SOFT»

1. Запустить DCS Electric

2. Открыть библиотеку `File – Open Library` выбрать файл `simulation.jelib`, нажать кнопку Open.
   Путь к файлу `./DCSElectric/Projects/5400ТР045А_031/simulation.jelib`

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/quick-start/quick-start1.png" alt="Открытие библиотеки simulation.jelib" />
  <figcaption  className="doc-image-container__image-title">Открытие библиотеки simulation.jelib</figcaption>
</figure>
</div>

3. Выбрать необходимую схему в раскрывающемся списке simulation

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/quick-start/quick-start2.png" alt="Список с типовыми проектами" />
  <figcaption  className="doc-image-container__image-title">Список с типовыми проектами</figcaption>
</figure>
</div>

4. Запустить автотрассировку схемы. Кнопка Autotracing на верхней панели. После завершения автотрассировки в папке config появится файл с конфигурационной последовательностью `analog_config.txt`

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/quick-start/quick-start3.png" alt="Запуск автотрассировки" />
  <figcaption  className="doc-image-container__image-title">Запуск автотрассировки</figcaption>
</figure>
</div>

5. Собрать отладочный комплект

6. Установить микросхему

7. Подать напряжение питания на плату +12В±5% на вывод <a href="/docs/5400TP045A-031/pams-develop-kit#внешний-вид-отладочной-платы">«А»</a> с ограничением по току 300 мА

8. Открыть DCSProg-5 и загрузить файл с конфигурацией:
   `«Микросхема» – «Загрузить файл»`, выбрать файл `analog_config.txt` и нажать кнопку `«Открыть»`

9. Запрограммировать микросхему в «SOFT» `«Микросхема» – «Прошить»`
