---
id: pams-library-block
title: Основные блоки библиотеки
sidebar_label: Основные блоки библиотеки
sidebar_position: 2
---

Описание основных блоков бибилиотеки `symbol` при работе с микросхемой 5400ТР045А-031.

## Блок параметров моделирования

Блок параметров моделирования «5400ТР045A_031_core» обязателен при построении любой схемы.

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

- **tstep** – шаг моделирования;
- **tstop** – время моделирования;
- **rshunt** – значение сопротивления резистора, добавленного между каждым выводом и «землей» для улучшения сходимости расчетов;
- **VDD** – напряжение питания микросхемы (допустимые значения от 3,0 до 5,0 В);
- **SAVE** – опция ngspice, которая обеспечивает сохранение только написанных цепей в процессе моделирования. Используется для уменьшения размера файла с результатами моделирования. Для стандартного моделирования поле требуется оставить пустым.
- **SAVE=all** - оция позволяет сохранить все внутренние и внешние цепи. Более подробную информацию можно посмотреть в ngspice manual «15.6.1. SAVE: Name vector(s) to be saved in raw file». Пример использования: «SAVE=inp inm out»

## vpulse – источник прямоугольных импульсов

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/library/vpulse-source.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/library/vpulse-source.png" alt="Источник vpulse" title="Источник vpulse" />
  <figcaption  className="doc-image-container__image-title">Источник vpulse</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/library/vpulse-source.png" alt="Источник vpulse" />
  <figcaption  className="doc-image-container__image-title">Источник vpulse</figcaption>
</figure>
</div>

- **V1** – значение напряжения нижнего уровня
- **V2** – значение напряжения верхнего уровня
- **TD** – время задержки
- **TR** – время фронта
- **TF** – время среза
- **PW** – ширина импульса
- **PER** – период

## vpwl – источник напряжения, задаваемый по точкам

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/library/vpwl-source.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/library/vpwl-source.png" alt="Источник vpwl" title="Источник vpwl" />
  <figcaption  className="doc-image-container__image-title">Источник vpwl</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/library/vpwl-source.png" alt="Источник vpwl" />
  <figcaption  className="doc-image-container__image-title">Источник vpwl</figcaption>
</figure>
</div>

VAL = T1 V1 T2 V2 T3 …

- **T1** – время T1
- **T2** – время T2
- **V1** – значение напряжения в точке T1
- **V2** – значение напряжения в точке T2

## vsin – источник синусоидальных импульсов

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/library/vsin-source.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/library/vsin-source.png" alt="Источник vsin" title="Источник vsin" />
  <figcaption  className="doc-image-container__image-title">Источник vsin</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/library/vsin-source.png" alt="Источник vsin" />
  <figcaption  className="doc-image-container__image-title">Источник vsin</figcaption>
</figure>
</div>

- **VO** – напряжение смещения
- **FREQ** – частота
- **VA** – амплитуда
- **TD** – время задержки
- **THETA** – коэффициент затухания

## vsource – источник постоянного напряжения

<!-- <div className="doc-image-container">
<a href="/img/5400ТР045А-031/library/vsource.png"  target="blank">
<figure>
    <img src="/img/5400ТР045А-031/library/vsource.png" alt="Источник vsource" title="Источник vsource" />
  <figcaption  className="doc-image-container__image-title">Источник vsource</figcaption>
</figure>
</a>
</div> -->

<div className="doc-image-container">
<figure>
  <img src="/img/5400ТР045А-031/library/vsource.png" alt="Источник vsource" />
  <figcaption  className="doc-image-container__image-title">Источник vsource</figcaption>
</figure>
</div>

VAL – значение постоянного напряжения

Для установки параметров источников напряжения необходимо дважды нажать на параметр ЛКМ
и вписать значение. Значения параметра вводится без указания единиц измерения. Чтобы ввести десятичную приставку, используются следующие обозначения:<sup></sup>

- 10<sup>-15</sup>фемто – f
- 10<sup>-9</sup> нано – n
- 10<sup>-3</sup> милли – m
- 10<sup>+6</sup> мега – Meg
- 10<sup>-12</sup> пико – p
- 10<sup>-6</sup> микро – u
- 10<sup>3</sup> кило – K
- 10<sup>9</sup> гига – G
