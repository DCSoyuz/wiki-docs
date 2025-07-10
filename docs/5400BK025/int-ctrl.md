---
id: mk025-int-ctrl
title: Контроллер прерываний
sidebar_label: Контроллер прерываний
sidebar_position: 14
---

При выполнении функции, вызванной прерыванием, необходимо произвести сброс данного прерывания.

## Регистры «Контроллера прерываний»

<table className="table">
<tbody>

  <tr>
    <th >№</th>
    <th >Аббревиатура</th>
    <th >Доступ</th>
    <th >Описание</th>
  </tr>

  <tr>
    <td  >2800h </td>
    <td  >INT_FIX_CLR0</td>
    <td  >RW</td>
    <td  >Регистр зафиксированных прерываний, группа 0 </td>
  </tr>
  
   <tr>
    <td  >2801h </td>
    <td  >INT_FIX_CLR1</td>
    <td  >RW</td>
    <td  >Регистр зафиксированных прерываний, группа 1</td>
  </tr>
  
   <tr>
    <td  >2802h </td>
    <td  >INT_FIX_CLR2</td>
    <td  >RW</td>
    <td  >Регистр зафиксированных прерываний, группа 2</td>
  </tr>
  
   <tr>
    <td  >2803h </td>
    <td  >INT_FIX_CLR3</td>
    <td  >RW</td>
    <td  >Регистр зафиксированных прерываний, группа 3</td>
  </tr>
     
</tbody>
</table>

### INT_FIX_CLR0

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
    <td  colSpan={4} >Резерв</td>
    <td  >I3_FIX</td>
    <td  >Резерв</td>
    <td  >I1_FIX</td>
    <td  >I0_FIX</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**I3_FIX** – прерывание CMM.

**I1_FIX** – прерывание WDT.

**I0_FIX** – прерывание WORK_FSM.

Запись в **Ix_FIX** регистра INT_FIX_CLR0:

- 1 – сбросить прерывание;
- 0 – не менять текущую настройку.

Чтение **Ix_FIX** регистра INT_FIX_CLR0:

- 1 – зафиксировано прерывание;
- 0 – прерывание отсутствует.

### INT_FIX_CLR1

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
    <td  colSpan={5} >Резерв</td>
    <td  >I2_FIX</td>
    <td  >I1_FIX</td>
    <td  >I0_FIX</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**I2_FIX** – прерывание UART.

**I1_FIX** – прерывание TIMER0.

**I0_FIX** – прерывание GPIO.

Запись в **Ix_FIX** регистра INT_FIX_CLR1:

- 1 – сбросить прерывание;
- 0 – не меняет текущую настройку.

Чтение **Ix_FIX** регистра INT_FIX_CLR1:

- 1 – зафиксировано прерывание;
- 0 – прерывание отсутствует.

### INT_FIX_CLR2

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
    <td  colSpan={7} >Резерв</td>
    <td  >I0_FIX</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**I0_FIX** – прерывание TIMER1.

Запись в **I0_FIX** регистра INT_FIX_CLR2:

- 1 – сбросить прерывание;
- 0 – не меняет текущую настройку.

Чтение **I0_FIX** регистра INT_FIX_CLR2:

- 1 – зафиксировано прерывание;
- 0 – прерывание отсутствует.

### INT_FIX_CLR3

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
    <td  colSpan={7} >Резерв</td>
    <td  >I0_FIX</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**I0_FIX** – прерывание TIMER2.

Запись в **I0_FIX** регистра INT_FIX_CLR3:

- 1 – сбросить прерывание;
- 0 – не меняет текущую настройку.

Чтение **I0_FIX** регистра INT_FIX_CLR3:

- 1 – зафиксировано прерывание;
- 0 – прерывание отсутствует.
