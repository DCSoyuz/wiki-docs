---
id: mk-keil
title: Keil IDE
sidebar_label: Keil IDE
sidebar_position: 3
---

Установка и использование Keil IDE

## Установка и настройка Keil IDE

Перед началом работы необходимо загрузить архивы DCSProg6 и projects_keil с сайта компании ([https://dcsoyuz.ru](https://dcsoyuz.ru) раздел «Программное обеспечение») и извлечь данные на персональный компьютер. Доступ к разделу «Программное обеспечение» предоставляется по запросу на электронную почту (support@dcsoyuz.ru).

Для программирования микросхемы 5400ТР105-003 потребуется программа DCSProg6. Создание конфигурационной последовательности выполняется в ПО Keil MVision C51.

Скачать IDE Keil MVision C51 можно с официального сайта разработчика [https://www.keil.com/download/product/](https://www.keil.com/download/product/)

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/programming/1.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Утилита Keil MVision C51</figcaption>
</figure>
</div>

1. Установить скачанную программу, используя настройки по умолчанию.
2. Открыть проект Example.uvproj.

Для открытия проекта в Keil MVision C51 необходимо выбрать меню `«Project» –> «Open Project»`.

Путь к файлу проекта в архиве projects_keil `«…\Projects\Example\Example.uvproj»`.

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/programming/2.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Выбор проекта в MVision</figcaption>
</figure>
</div>

3. В настройках проекта («Alt+F7») во вкладке «Target» установить размеры памяти ОЗУ и ПЗУ:

- Off-chip Code memory: Start – 0x0000; Size – 0x1000;
- Off-chip Xdata memory: Start – 0x0000; Size – 0x1100.

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/programming/3.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Установка размеров памяти ОЗУ и ПЗУ в настройках проекта</figcaption>
</figure>
</div>

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/programming/4.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Настройка проекта для создания файла с расширением hex</figcaption>
</figure>
</div>

4. В настройках проекта во вкладке «Output» установить галочку «Create HEX File» для создания файла с расширением hex. Нажать «OK».

Установка и настройка ПО для работы с микросхемой 5400ТР105-003 завершена.

В демонстрационной версии проекта Example.uvproj реализована программа с примером работы светодиодов и выводов микросхемы GPIOA_4 – GPIOA_7.

## Создание и обновление файла конфигурации (hex-файл)

Для компиляции тестового проекта выполните команду `«Project» –> «Build Target»` или клавиша F7. Ошибки компиляции будут выведены в окне Build Output.

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/programming/5.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Компиляция проекта</figcaption>
</figure>
</div>

Для создания или обновления существующего hex-файла выполните команду `«Project» –> «Rebuild all target files»`.

В результате выполнения команды будет сформирован файл с расширением hex.

Путь к hex-файлу `«…\Projects\Example\Objects\Example.hex»`.

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/programming/6.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Команда для формирования и обновления hex-файла</figcaption>
</figure>
</div>
