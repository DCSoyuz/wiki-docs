---
id: mk-eclipse
title: Eclipse IDE
sidebar_label: Eclipse IDE
sidebar_position: 4
---

Установка и использование Eclipse IDE

## Установка и настройка Eclipse IDE

Программа для отладки разработана в виде набора плагинов для Eclipse. На текущий момент получить плагины можно только в составе сборки DCS-Eclipse.

В качестве компилятора для 5400TP105-003 предлагается использовать SDCC ([SDCC manual](https://sdcc.sourceforge.net/doc/sdccman.pdf)).

Среда разработана и протестирована на операционной системе «Ubuntu 22.04». Поддержка других операционных систем будет добавлена позднее.

## Настройка окружения

Предварительно требуется установить SDCC:

**Ubuntu 22.04**

- Загрузить архив eclipse_ubuntu с сайта в разделе «Программное обеспечение» и извлечь данные на персональный компьютер

- Установить java-17 командой <pre><code className="language-javascript">sudo apt install openjdk-17-jdk</code></pre>

- Установить компилятор для 8051 командой <pre><code className="language-javascript">sudo apt install sdcc</code></pre>

- Перейти в папку eclipse и из терминала запустить IDE командой <pre><code className="language-javascript">sudo ./eclipse</code></pre>

**Windows**

- Установить eclipse из архива eclipse_win32.
- Установить java-17 с сайта разработчика.<br/>
  https://download.oracle.com/java/17/archive/jdk-17.0.9_windows-x64_bin.msi или <br/>
  https://download.oracle.com/java/17/archive/jdk-17.0.9_windows-x64_bin.exe

- Установить SDCC. Скачать файл sdcc-winX, где X – разрядность операционной системы.
  https://sourceforge.net/projects/sdcc/files/
- Перейти в папку Eclipse и запустить eclipse.exe.

:::info Примечание
В случае, если на компьютере были установлены другие версии Java и у вас не запускается программа ниже представлены возможные пути решения проблемы.

1. Папка, в которую установлена Java-17 находится в системных переменных среды операционной системы. Путь к файлу java.exe должен находится в переменной Path. Для того, чтобы в этом убедиться нажмите ПКМ на `«Пуск»`, выберите `«Система» – «Дополнительные параметры системы»–«Переменные среды»`, выбрать переменную Path и нажать `«Изменить»`.
   Если в переменной Path находится одновременно несколько путей до java.exe, то рекомендуется удалить т.к может быть использована некорректная версия java для запуска программы.
2. Системная переменная JAVA_HOME должна ссылаться на папку с установленной java (например `C:\Program Files\Java\jdk-17\bin\` или `C:\Program Files\Common Files\Oracle\Java\javapath`). Если переменная отсутствует, то ее необходимо создать.

Если программа после всех действий не запускается и ваш путь к java содержит `C:\Program Files\Common Files\Oracle\Java\javapath`, то замените на явный путь к java `C:\Program Files\Java\jdk-17\bin\`

:::

## Создание проекта

Одновременно допускается использовать только один проект. Если требуется использовать другой проект, остальные необходимо закрыть.

Для создания первого проекта необходимо нажать на строку `«Create a new C or C++ project»` или `«Create new Project...» → «C Project»`

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/1.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Создание проекта</figcaption>
</figure>
</div>

В качестве категории проекта выбрать «C Project». Нажать «Next».

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/2.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Выбор категории проекта</figcaption>
</figure>
</div>

Выбрать тип проекта «Executable/5400TP105-003 C Project».

В окне «Toolchains» выбрать «SDCC Tool Chain», если вариантов более одного, и он не выбран по умолчанию.

Указать название проекта.

Убедиться, что проект создается в ожидаемой директории. При необходимости убрать галочку «Use default location» и изменить путь.

Нажать «Next».

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/3.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Выбор типа проекта</figcaption>
</figure>
</div>

При необходимости изменить свойства проекта.

Желательно не трогать поля «Source» и «Linker other options», если вы не знаете, что делаете.

Нажать «Next».

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/4.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Свойства проекта</figcaption>
</figure>
</div>

В следующем окне ничего не изменять. Нажать кнопку «Finish».

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/5.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Выбор конфигурации проекта</figcaption>
</figure>
</div>

Возможно, IDE предложит сменить перспективу. Необходимо согласиться нажатием кнопки «Open Perspective».

Перспективу также можно сменить в правом верхнем углу рабочего окна (кнопка «Open Perspective»).

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/6.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Открытие перспективы</figcaption>
</figure>
</div>

## Настройка проекта

Для первой сборки проекта нужно выполнить ряд действий:

- Настроить проект для использования компилятора. Для этого нужно нажать ПКМ на проект и выбрать «Properties» в появившемся контекстном меню.

- В категории С/C++ Build нажать кнопку «Manage Configurations», выбрать «Release» и нажать «Set Active».

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/8.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Окно настроек проекта</figcaption>
</figure>
</div>

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/7.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Меню управления конфигурацией</figcaption>
</figure>
</div>

- В «Configuration» выбрать «Release [ Active ]»

- В категории С/C++ Build выбрать «Builder type: Internal builder»

- Добавить генерацию hex-файла.

- Для этого перейти в подкатегорию «Settings», в окне «Build Artifact» выбрать «Artifact extension: hex».

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/9.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Установка генерации hex-файла</figcaption>
</figure>
</div>

- Подтвердить изменения нажав «Apply and Close».

- Выполнить сборку проекта нажав на молоток на панели инструментов или кнопку «Build all».

:::info Примечание
Если в консоли возникает ошибка `«Error: Program "sdcc" not found in PATH»`, то необходимо убедиться, что в системной переменной Path среды операционной системы указан путь к sdcc. Для этого, нажмите ПКМ на `«Пуск»`, выберите `«Система» – «Дополнительные параметры системы»–«Системные переменные»`, выбрать переменную Path и нажать `«Изменить»`. Если путь отсутствует, то необходимо нажать кнопку «Создать» и добавить путь (пример `C:\Program Files\SDCC\bin`).

:::

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/10.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Сборка проекта</figcaption>
</figure>
</div>

## Удаление/закрытие проекта

Для удаления/закрытия проекта необходимо нажать ПКМ по проекту и в выпадающем меню выбрать пункт «Delete».

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/17.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Удаление/закрытие проекта</figcaption>
</figure>
</div>

Для удаления нужно нажать на checkbox «Delete project contents on disk (connot be undone)». Для закрытия проекта галочку ставить не нужно. Подтвердить нажатием кнопки «OK».

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/18.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Подтверждение удаления/закрытия</figcaption>
</figure>
</div>

## Описание проекта

На рисунке ниже показано дерево проекта.

- **8051.h** — библиотека внутренних регистров ядра;
- **regs_map_C.h** — библиотека внешних регистров ядра;
- **lint.h** и **std.h** — файлы для более корректной работы системы проверки синтаксиса;
- **main.c** — функция main.

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/eclipse-debug/16.png" alt="" />
  <figcaption  className="doc-image-container__image-title">Дерево проекта</figcaption>
</figure>
</div>
