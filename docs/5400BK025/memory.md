---
id: mk025-memory
title: Постоянная память данных
sidebar_label: Постоянная память данных
sidebar_position: 11
---

Постоянная память данных представляет собой однократно программируемую память ёмкостью 64Б. Данные записываются побайтно. Требуемое время записи одного байта 200 мс.

Область памяти размещена в старших 64 байтах ПЗУ OTP, но доступна программно по адресам 0x2500. Поскольку память расположена физически в памяти программ, то после команды записи в нее CPU переходит в режим ожидания на интервал, заданный в регистрах OTP_PRESC (номинально 200 мс).

## Алгоритм записи данных

- Задать в регистрах OTP_PRESC (L / M / H) интервал, соответствующий не менее 200 мс в тактах частоты системы;
- В регистры OTP_PRE (L / M / H) и OTP_POST (L / M / H) задать защитные интервалы не менее 100 мс для включения напряжения программирования;
- Записать байт данных по адресам 0x2500 – 0x253F.

## Алгоритм чтения данных

- Данные доступны для чтения по адресам 0x2500 – 0x253F.
- Данные доступны в области программ по старшим 64 адресам ПЗУ OTP.

## Регистры модуля управления OTP ПЗУ 64Б

| №     | Аббревиатура | Доступ | Описание                             |
| ----- | ------------ | ------ | ------------------------------------ |
| 2500h | OTP_ROM_DATA | RW     | Регистр для записи/считывания данных |
| 2540h | OTP_PRESCL   | RW     | Интервал программирования 1          |
| 2544h | OTP_PRESCM   | RW     | Интервал программирования 2          |
| 2548h | OTP_PRESCH   | RW     | Интервал программирования 3          |
| 2550h | OTP_PREL     | RW     | Начальный защитный интервал 1        |
| 2554h | OTP_PREM     | RW     | Начальный защитный интервал 2        |
| 2558h | OTP_PREH     | RW     | Начальный защитный интервал 3        |
| 2560h | OTP_POSTL    | RW     | Конечный защитный интервал 1         |
| 2564h | OTP_POSTM    | RW     | Конечный защитный интервал 2         |
| 2568h | OTP_POSTH    | RW     | Конечный защитный интервал 3         |

### OTP_ROM_DATA

<table className="table">
<tbody>
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={8} >Данные на запись или чтение [7:0]</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

Данный регистр предназначен для записи и чтения данных. При записи в регистр инициализируется процесс записи в ПЗУ по соответствующему адресу.

### OTP_PRESCL

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={8} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – интервал программирования, младшая часть.VALUE – интервал программирования, младшая часть.

### OTP_PRESCM

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={8} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – интервал программирования, биты &lt;15:8&gt;.

### OTP_PRESCH

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={8} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – интервал программирования, старшая часть.

### OTP_PREL

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={8} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – начальный защитный интервал, младшая часть.

### OTP_PREM

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={8} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – начальный защитный интервал, биты &lt;15:8&gt;.

### OTP_PREH

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={2} >Резерв</td>
    <td colSpan={6} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – начальный защитный интервал, старшая часть.

### OTP_POSTL

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={8} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – конечный защитный интервал, младшая часть.

### OTP_POSTM

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={8} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – конечный защитный интервал, биты &lt;15:8&gt;.

### OTP_POSTH

<table className="table">
<tbody>
 
  <tr>
    <th >Бит</th>
    <th >7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
  </tr>

  <tr>
    <th >Назначение</th>
    <td colSpan={2} >Резерв</td>
    <td colSpan={6} >VALUE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

VALUE – конечный защитный интервал, старшая часть.

Диаграмма записи имеет следующий вид. Команда записи в ROM_DATA (WR) приводит к переводу процессора в режим ожидания (READY) и началу отсчета интервала до включения напряжения программирования (VPP_CTRL). Диаграмма напряжения программирования состоит из 3 фаз – PRE, PRESC, POST.

<div className="doc-image-container">
<figure>
  <img src="/img/5400ВК025/memory/Временная_диаграмма_записи.svg" alt="" />
  <figcaption  className="doc-image-container__image-title">Временная диаграмма записи</figcaption>
</figure>
</div>
