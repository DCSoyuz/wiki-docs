---
id: mk-int-ctrl
title: Контроллер прерываний
sidebar_label: Контроллер прерываний
sidebar_position: 15
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
    <td  >3100h </td>
    <td  >INT_FIX_CLR0</td>
    <td  >RW</td>
    <td  >Регистр зафиксированных прерываний, группа 0 </td>
  </tr>
  
   <tr>
    <td  >3101h </td>
    <td  >INT_FIX_CLR1</td>
    <td  >RW</td>
    <td  >Регистр зафиксированных прерываний, группа 1</td>
  </tr>
  
   <tr>
    <td  >3102h </td>
    <td  >INT_FIX_CLR2</td>
    <td  >RW</td>
    <td  >Регистр зафиксированных прерываний, группа 2</td>
  </tr>
  
   <tr>
    <td  >3103h </td>
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
    <td  >I2_FIX</td>
    <td  >Резерв</td>
    <td  >I0_FIX</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**I3_FIX** – прерывание CMM.

**I2_FIX** – прерывание WDT.

**I0_FIX** – прерывание WORK_FSM.

Запись в **Ix_FIX** регистра INT_FIX_CLR:

- 1 – сбросить прерывание;
- 0 – не менять текущую настройку.

Чтение **Ix_FIX** регистра INT_FIX_CLR:

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
    <td  colSpan={3} >Резерв</td>
    <td  >I4_FIX</td>
    <td  >I3_FIX</td>
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

**I4_FIX** – прерывание I2C.

**I3_FIX** – прерывание SPI0.

**I2_FIX** – прерывание UART0.

**I1_FIX** – прерывание TIMER0.

**I0_FIX** – прерывание GPIOA.

Запись в **Ix_FIX** регистра INT_FIX_CLR:

- 1 – сбросить прерывание;
- 0 – не меняет текущую настройку.

Чтение **Ix_FIX** регистра INT_FIX_CLR:

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
    <td  colSpan={3} >Резерв</td>
    <td  >I4_FIX</td>
    <td  >I3_FIX</td>
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

**I4_FIX** – прерывание OWI.

**I3_FIX** – прерывание SPI1.

**I2_FIX** – прерывание UART1.

**I1_FIX** – прерывание TIMER1.

**I0_FIX** – прерывание GPIOB.

Запись в **Ix_FIX** регистра INT_FIX_CLR:

- 1 – сбросить прерывание;
- 0 – не меняет текущую настройку.

Чтение **Ix_FIX** регистра INT_FIX_CLR:

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
    <td  colSpan={6} >Резерв</td>
    <td  >I1_FIX</td>
    <td  >I0_FIX</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**I1_FIX** – прерывание TIMER2.

**I0_FIX** – прерывание GPIOC.

Запись в **Ix_FIX** регистра INT_FIX_CLR:

- 1 – сбросить прерывание;
- 0 – не меняет текущую настройку.

Чтение **Ix_FIX** регистра INT_FIX_CLR:

- 1 – зафиксировано прерывание;
- 0 – прерывание отсутствует.
