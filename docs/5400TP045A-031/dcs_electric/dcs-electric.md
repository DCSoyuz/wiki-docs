---
id: pams-electric
title: Описание DCS Electric
sidebar_label: Описание DCS Electric
sidebar_position: 1
---

Для работы с микросхемой 5400TP0045А-031 (ПАМС) разработано программное обеспечение DCS Electric. Программное обеспечение используется для проектирования и моделирования электрических схем, а также создания конфигурационной последовательности для последующего программирования микросхемы.

## Установка и настройка ПО

**Рекомендуемые системные требования**

- операционная система: Windows 7, Windows 8, Windows 10;
- оперативная память 4 ГБ;
- 8 ГБ свободного места на жёстком диске.

Перед началом работы необходимо загрузить архив DCSElectric.zip с сайта компании https://dcsoyuz.ru раздел «Программное обеспечение» и извлечь на персональный компьютер. Доступ к авторизации на сайте предоставляется по запросу на электронную почту support@dcsoyuz.ru.

1. Установить Java (файл `jre-8u192-windows-x64.exe`) из папки Install на диск `C:\...`
2. Запустить файл `electric.bat` из папки с программой
3. Загрузить настройки (выполняется один раз при первом запуске программы):
   `File – Preferences – Import`. Путь к файлу `\electric\Prefs\Cadence_style_PAMS.xml`
4. Перезапустить программу

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/pref_import.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/pref_import.png" alt="Импорт настроек" title="Импорт настроек" />
  <figcaption  className="doc-image-container__image-title">Импорт настроек</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/pref_import.png" alt="Импорт настроек" />
  <figcaption  className="doc-image-container__image-title">Импорт настроек</figcaption>
</figure>
</div>

## Создание электрической схемы

1. Открыть библиотеку
   `File –> Open Library`, выбрать файл `simulation.jelib`, нажать кнопку Open.
   Путь к файлу `./DCSElectric/Projects/5400ТР045А_031/simulation.jelib`
2. Создать новую схему. Нажать ПКМ по библиотеке simulation и выбрать пункт `Create New Cell`. В открывшемся окне в поле Name ввести название схемы, в поле View выбрать schematic. Нажать кнопку ОК.

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/create_new_scheme.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/create_new_scheme.png" alt="Создание новой электрической схемы" title="Создание новой электрической схемы" />
  <figcaption  className="doc-image-container__image-title">Создание новой электрической схемы</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/create_new_scheme.png" alt="Создание новой электрической схемы" />
  <figcaption  className="doc-image-container__image-title">Создание новой электрической схемы</figcaption>
</figure>
</div>

3. Перенести схему 5400ТР045А_031 из библиотеки `symbol` в рабочее пространство. Для этого зажмите ЛКМ на строке 5400ТР045А_031 и не отпуская кнопку, перетащите в рабочее пространство.

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/library_031.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/library_031.png" alt="схема 5400ТР045А_031" title="схема 5400ТР045А_031" />
  <figcaption  className="doc-image-container__image-title">Расположение схемы 5400ТР045А_031 в библиотеке symbol</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/library_031.png" alt="Расположение схемы 5400ТР045А_031 в библиотеке symbol" />
  <figcaption  className="doc-image-container__image-title">Расположение схемы 5400ТР045А_031 в библиотеке symbol</figcaption>
</figure>
</div>

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/scheme_5400TP045A-031.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/scheme_5400TP045A-031.png" alt="Схема 5400ТР045А_031 в рабочем поле программы" title="Схема 5400ТР045А_031 в рабочем поле программы" />
  <figcaption  className="doc-image-container__image-title">Схема 5400ТР045А_031 в рабочем поле программы</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/scheme_5400TP045A-031.png" alt="Схема 5400ТР045А_031 в рабочем поле программы" />
  <figcaption  className="doc-image-container__image-title"></figcaption>
</figure>
</div>

4. Собрать схему, замыкая нужные ключи и выставляя необходимые параметры.

Более подробно о ключах, параметрах и блоках внешних воздействий см. в соответвующих разделах:

- <a href="/docs/5400TP045A-031/dcs_electric/pams-scheme-block">«Основные блоки схемы»</a>
- <a href="/docs/5400TP045A-031/dcs_electric/pams-library-block">«Основные блоки библиотеки»</a>

### Установка параметров

В схеме 5400ТР045А_031 нельзя реализовывать дополнительные связи или размещать блоки. Пользователям разрешается только замыкать ключи и выставлять необходимые параметры. Вне схемы 5400ТР045А_031 возможно объединять выводы с помощью линий связи и подключать блоки внешних воздействий.

Например, для размещения линии от вывода OUT необходимо нажать на контакт ЛКМ, а затем в свободное место на рабочем поле ПКМ. В процессе проектирования рекомендуется периодически нажимать кнопку F8 (исправление связей). При нажатии проверяются все связи в схеме и удаляются лишние соединительные линии.

Чтобы установить параметр у какого-либо блока схемы, необходимо зажать клавишу Ctrl и левой кнопкой мыши выделить данный параметр.

После того как параметр выделен, отпустите клавишу Ctrl и дважды нажмите ЛКМ по параметру. Введите необходимое значение и нажмите клавишу Enter.

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/param-input.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/param-input.png" alt="Пример выделенного параметра PR2" title="Пример выделенного параметра PR2" />
  <figcaption  className="doc-image-container__image-title">Пример выделенного параметра PR2</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/param-input.png" alt="Пример выделенного параметра PR2" />
  <figcaption  className="doc-image-container__image-title">Пример выделенного параметра PR2</figcaption>
</figure>
</div>

### Навигация в графическом интерфейсе

Приближение и отдаление активного рабочего поля:

- Клавиша «E» – приближение;
- Клавиша «W» – отдаление;
- Клавиша «Z» – масштабирование области;
- Клавиша «Ctrl» + прокрутка колеса мыши;
- Клавиша «F» – масштабирование и центрирование всей схемы.

Перемещение по рабочему полю:

- Зажать колесо мыши и перемещаться по рабочему полю с помощью мыши;
- Нажать на значок «Toggle Pan» (клавиша P) в поле инструментов и, зажав левую кнопку мыши, перемещаться по полю
- «Num2» – перемещение по рабочей области вниз
- «Num4» – перемещение по рабочей области влево
- «Num6» – перемещение по рабочей области вправо
- «Num8» – перемещение по рабочей области вверх

Отмена действия:

- Сочетаний клавиш «Ctrl» и «Z»;
- Нажать на значок «Undo» в поле инструментов.

## Моделирование электрической схемы

1. Перенести из библиотеки `symbol` блок «5400ТР045A_031_core».

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/031_core.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/031_core.png" alt="Параметры моделирования по времени" title="Параметры моделирования по времени" />
  <figcaption  className="doc-image-container__image-title">Параметры моделирования по времени</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/031_core.png" alt="Параметры моделирования по времени" />
  <figcaption  className="doc-image-container__image-title">Параметры моделирования по времени</figcaption>
</figure>
</div>

2. Задать входные воздействия с помощью источников напряжения.

Перенести из библиотеки `symbol` необходимый источник. Для входных сигналов рекомендуется использовать источник прямоугольного сигнала (vpulse), источник постоянного напряжения (vsource) или источник синусоидальных импульсов (vsin).

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/vpulse.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/vpulse.png" alt="Источники в библиотеке symbol" title="Источники в библиотеке symbol" />
  <figcaption  className="doc-image-container__image-title">Источники в библиотеке symbol</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/vpulse.png" alt="Источники в библиотеке symbol" />
  <figcaption  className="doc-image-container__image-title">Источники в библиотеке symbol</figcaption>
</figure>
</div>

Соединить вывод источника напряжения с соответствующим входом схемы.

3. Указать названия выводам, которые необходимо контролировать (пример: «INP, INM, OUT…»).
   Для обозначения вывода необходимо зайти в его свойства (клавиша «q» или двойное нажатие ЛКМ по проводу) и в поле «Name» ввести название.

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/name_pins.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/name_pins.png" alt="Обозначение выводов после построения схемы" title="Обозначение выводов после построения схемы" />
  <figcaption  className="doc-image-container__image-title">Обозначение выводов после построения схемы</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/name_pins.png" alt="Обозначение выводов после построения схемы" />
  <figcaption  className="doc-image-container__image-title">Обозначение выводов после построения схемы</figcaption>
</figure>
</div>

4. Сохранить проект `File –> Save Library`

5. Запустить моделирование `Tools –> Simulation (Spice) –> Simulate`. Или кнопка на панели инструментов.

6. После завершения процесса моделирования откроется окно LTSpice IV.

Для вывода результатов на экран выбрать пункт `Plot Settings –> Add` (Ctrl+A) и в появившемся окне указать названия требуемых выводов (пример: «INP, INM, OUT, LDOOUT…»). Выбор проводника осуществляется при помощи поисковой строки «Only list traces matching», где вводятся названия выводов. Например, если необходимо посмотреть сигнал на выходе схемы, то в поисковой строке необходимо ввести out и нужный проводник будет обозначаться как «v(out)».

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/add_trace_to_plot.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/add_trace_to_plot.png" alt="Окно вывода результатов моделирования" title="Окно вывода результатов моделирования" />
  <figcaption  className="doc-image-container__image-title">Окно вывода результатов моделирования</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/add_trace_to_plot.png" alt="Окно вывода результатов моделирования" />
  <figcaption  className="doc-image-container__image-title">Окно вывода результатов моделирования</figcaption>
</figure>
</div>

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/electric/model_LTspice.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/electric/model_LTspice.png" alt="Результаты моделирования" title="Результаты моделирования" />
  <figcaption  className="doc-image-container__image-title">Результаты моделирования</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/electric/model_LTspice.png" alt="Результаты моделирования" />
  <figcaption  className="doc-image-container__image-title">Результаты моделирования</figcaption>
</figure>
</div>

### Инструменты моделирования LTspice IV

- Увеличение области – нажать ЛКМ, и не отпуская, выделить интересующую область.
- Возврат масштаба к начальному – нажать кнопку «Zoom full extents» на панели инструментов.
- Добавление координатной плоскости: Plot Settings –> Add Plot Pane.
- Вывод маркеров – нажать ЛКМ по названию проводника.
- Удаление маркера – нажать клавишу «Delete» и ЛКМ выбрать название проводника в верхней части окна.

## Создание конфигурационной последовательности

Для создания конфигурационной последовательности необходимо нажать кнопку на панели инструментов.
После завершения автотрассировки программа выдаст сообщение «Autotracing process completed». В папке config появится файл с конфигурационной последовательностью `analog_config.txt`. В файле указаны так называемые «ключи», которые отвечают за настройку различных блоков микросхемы.
