---
id: mk-analog-cfg
title: Конфигурационная память
sidebar_label: Конфигурационная память
sidebar_position: 3
---

В микросхеме реализована конфигурационная память (ANALOG_CFG), которая может работать как в «SOFT», так и в «HARD» режиме.

Регистры модуля ANALOG_CFG подключены к конфигурационному однократно программируемому ПЗУ.

Вывод TM (Test Mode) определяет режим работы следующих выводов микросхемы 9–12, 28, 39, 44, 45.

При TM = «1» выводы работают следующим образом:

<ul>
  <li>9-12 – JTAG</li>
  <li>28 – PGM</li>
  <li>39 – OUT_REF</li>
  <li>44 – H_S</li>
  <li>45 – RC</li>
</ul>

При TM = 0 конфигурационная память будет работать в режиме «HARD», а вывод GPIOB&lt;0&gt;/H_S как порт ввода-вывода.

В зависимости от вывода 44 – H_S источником данных конфигурационной памяти могут быть, либо регистры, либо ПЗУ («1» – «SOFT» режим, «0» – «HARD» режим соответственно).

В «SOFT» режиме при подаче 9,0 В на вывод VPP_9V конфигурационное ПЗУ прожигается.

## Регистры модуля ANALOG_CFG

<table className="table">
<tbody>

  <tr>
    <th >№</th>
    <th >Аббревиатура</th>
    <th >Доступ</th>
    <th >Описание</th>
  </tr>

  <tr>
    <td  >3300h </td>
    <td  >ANALOG_O_BUF</td>
    <td  >W</td>
    <td  >Регистр управления выходным буфером ЦАП, управления выходным масштабирующим операционным усилителем (МОУ) после ИОН (вывод VRP), настройки коэффициента усиления МОУ </td>
  </tr>
  
   <tr>
    <td  >3301h </td>
    <td  >ANALOG_O_PLL</td>
    <td  >W</td>
    <td  >Регистр настройки источника тактовой частоты микроконтроллера</td>
  </tr>
  
   <tr>
    <td  >3302h </td>
    <td  >ANALOG_O_RC</td>
    <td  >W</td>
    <td  >Регистр настройки емкости конденсатора RC-генератора </td>
  </tr>
  
   <tr>
    <td  >3303h </td>
    <td  >ANALOG_O_REF</td>
    <td  >W</td>
    <td >Регистр управления конденсаторами частотной коррекции МОУ и настройки выходного напряжения ИОН (вывод OUT_REF)</td>
  </tr>

   <tr>
    <td  >3306h </td>
    <td  >ANALOG_O_RC_R</td>
    <td  >W</td>
    <td  >Регистр настройки сопротивления резистора RC-генератора, выбора источника BOR, управления выводами GPIOB(1), OUT_REF и источниками тактовой частоты в тестовом режиме</td>
  </tr>
    
</tbody>
</table>

### ANALOG_O_BUF

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
    <td  >DAC_BUF_EN</td>
    <td  >OA_EN</td>
    <td  colSpan={3} >OA_GAIN_N</td>
    <td  colSpan={3} >OA_GAIN_M</td>
  </tr>
  
   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
  </tbody>
</table>

**DAC_BUF_EN** – включение выходного буфера ЦАП:

- 1 – выходной буфер включен;
- 0 – выходной буфер выключен.

**OA_EN** – включение выходного МОУ после ИОН (вывод VRP):

- 1 – МОУ включен;
- 0 – МОУ выключен (Z-состояние).

**OA_GAIN_N** – коэффициент масштабирования N для настройки коэффициента усиления МОУ.

**OA_GAIN_M** – коэффициент масштабирования M для настройки коэффициента усиления МОУ.

Блок МОУ состоит из ОУ общего назначения и потенциометра, используемого для подбора коэффициентов масштабирования. На вход блока подается выходное напряжение ИОН, которое усиливается в зависимости от масштабирующих коэффициентов.

Если блок выключен, то он находится в режиме ожидания и не потребляет ток. Имеется возможность отключения частотной коррекции.

#### Настройка коэффициентов масштабирования

<table className="table">
<tbody>

  <tr>
    <th  colSpan={9} >Коэффициент усиления МОУ</th>
  </tr>

<tr>
 <th >N|M</th>
    <th >000b</th>
    <th >001b</th>
    <th >010b</th>
    <th >011b</th>
    <th >100b</th>
    <th >101b</th>
    <th >110b</th>
    <th >111b</th>
</tr>

  <tr>
    <th >000b</th>
    <td  >2</td>
    <td  >1,5</td>
    <td  >1,333333</td>
    <td  >1,25</td>
    <td  >1,2</td>
    <td  >1,166667</td>
    <td  >1,142857</td>
    <td  >1,125</td>
  </tr>
  
<tr>
    <th >001b</th>
    <td  >3</td>
    <td  >2</td>
    <td  >1,666667</td>
    <td  >1,5</td>
    <td  >1,4</td>
    <td  >1,333333</td>
    <td  >1,285714</td>
    <td  >1,25</td>
  </tr>
  
<tr>
    <th >010b</th>
    <td  >4</td>
    <td  >2,5</td>
    <td  >2</td>
    <td  >1,75</td>
    <td  >1,6</td>
    <td  >1,5</td>
    <td  >1,428571</td>
    <td  >1,375</td>
  </tr>

<tr>
    <th >011b</th>
    <td  >5</td>
    <td  >3</td>
    <td  >2,333333</td>
    <td  >2</td>
    <td  >1,8</td>
    <td  >1,666667</td>
    <td  >1,571429</td>
    <td  >1,5</td>
  </tr>

<tr>
    <th >100b</th>
    <td  >6</td>
    <td  >3,5</td>
    <td  >2,666667</td>
    <td  >2,25</td>
    <td  >2</td>
    <td  >1,833333</td>
    <td  >1,714286</td>
    <td  >1,625</td>
  </tr>

<tr>
    <th >101b</th>
    <td  >7</td>
    <td  >4</td>
    <td  >3</td>
    <td  >2,5</td>
    <td  >2,2</td>
    <td  >2</td>
    <td  >1,857143</td>
    <td  >1,75</td>
  </tr>

<tr>
    <th >110b</th>
    <td  >8</td>
    <td  >4,5</td>
    <td  >3,333333</td>
    <td  >2,75</td>
    <td  >2,4</td>
    <td  >2,166667</td>
    <td  >2</td>
    <td  >1,875</td>
  </tr>

<tr>
    <th >111b</th>
    <td  >9</td>
    <td  >5</td>
    <td  >3,666667</td>
    <td  >3</td>
    <td  >2,6</td>
    <td  >2,333333</td>
    <td  >2,142857</td>
    <td  >2</td>
  </tr>
 
</tbody>
</table>

### ANALOG_O_PLL

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
    <td  colSpan={8} >PLL</td>
  </tr>
  
   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**PLL** – совместно с TM и TM_CLK_TYPE значения в данном регистре определяют и настраивают источник тактового сигнала микроконтроллера XTAL_CLK, а также совместно с RC_OUT_DISABLE определяют источник частоты в тестовом режиме на выводе GPIOB&lt;1&gt;/RC_CLK_OUT.

#### Определение и настройка источника тактовой частоты микроконтроллера.

<table className="table">
<tbody>

  <tr>
    <th rowSpan={2}>TM</th>
    <th  rowSpan={2}>TM_CLK_TYPE</th>
    <th  colSpan={8} >PLL</th>
    <th rowSpan={2}>RC_CLK</th>
    <th rowSpan={2}>XTAL_CLK</th>
  </tr>

<tr>
    <th>7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
</tr>

  <tr>
    <td  >1</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
    <td  >GEN1_QV</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >X</td>
    <td  >0</td>
    <td  >0</td>
    <td  >X</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
    <td  >GEN1_EXT</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >X</td>
    <td  >0</td>
    <td  >1</td>
    <td  >X</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
    <td  >GEN1_QV</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >X</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
    <td  >RC</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >0</td>
    <td  >0</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >RC</td>
    <td  >GEN1_EXT+PLL</td>
  </tr>

 <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >1</td>
    <td  >0</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >RC</td>
    <td  >GEN1_QV+PLL</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >1</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >RC</td>
    <td  >RC+PLL</td>
  </tr>

  <tr>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >0</td>
    <td  >0</td>
    <td  >X</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
    <td  >GEN1_EXT</td>
  </tr>
  
   <tr>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >0</td>
    <td  >1</td>
    <td  >X</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
    <td  >GEN1_QV</td>
  </tr>

   <tr>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
    <td  >RC</td>
  </tr>
    <tr>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >0</td>
    <td  >0</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >RC</td>
    <td  >GEN1_EXT+PLL</td>
  </tr> 
  <tr>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >1</td>
    <td  >0</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >RC</td>
    <td  >GEN1_QV+PLL</td>
  </tr>
    <tr>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >1</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >RC</td>
    <td  >RC+PLL</td>
  </tr>

</tbody>
</table>

#### Определение источника GPIOB&lt;1&gt;/RC_CLK_OUT

<table className="table">
<tbody>

  <tr>
    <th rowSpan={2}>TM</th>
    <th  rowSpan={2}>TM_CLK_TYPE</th>
    <th rowSpan={2}>RC_OUT_DISABLE</th>
    <th  colSpan={8} >PLL</th>
    <th rowSpan={2}>GPIOB_1>/RC_CLK_OUT</th>
  </tr>

<tr>
    <th>7</th>
    <th >6</th>
    <th >5</th>
    <th >4</th>
    <th >3</th>
    <th >2</th>
    <th >1</th>
    <th >0</th>
</tr>

  <tr>
    <td  >1</td>
    <td  >X</td>
    <td  >0</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >X</td>
    <td  >0</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >1</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >0</td>
    <td  >1</td>
    <td  >X</td>
    <td  >0</td>
    <td  >0</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >GEN1_EXT+PLL</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >0</td>
    <td  >1</td>
    <td  >X</td>
    <td  >1</td>
    <td  >0</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >GEN1_QV+PLL</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >0</td>
    <td  >0</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >0</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >GEN1_QV+PLL</td>
  </tr>

 <tr>
    <td  >1</td>
    <td  >X</td>
    <td  >0</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >1</td>
    <td  >1</td>
    <td  >K2</td>
    <td  >K1</td>
    <td  >K0</td>
    <td  >RC+PLL</td>
  </tr>

  <tr>
    <td  >1</td>
    <td  >X</td>
    <td  >1</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >RC</td>
  </tr>

  <tr>
    <td  >0</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >X</td>
    <td  >GPIOB_1</td>
  </tr>
</tbody>
</table>

**x** – биты, которые не имеют значения;

**GEN1_EXT** – внешняя тактовая частота с вывода GEN1 (источник – внешний генератор);

**GEN1_QV** – тактовая частота с вывода GEN1 (источник – встроенный генератор на основе внешнего кварцевого резонатора). Возможно тактирование от внешнего генератора с размахом цифровых уровней от 0 В до 5,0 В. При использовании внешнего генератора, вывод GEN2 (7) необходимо оставить в обрыве. Частота задается на вывод GEN1 (6) без внешних компонентов.

**GEN1_EXT+PLL** – внешняя тактовая частота, пропущенная через ФАПЧ;

**GEN1_QV+PLL** – частота с кварцевого генератора, пропущенная через ФАПЧ;

**RC+PLL** – частота с RC-генератора, пропущенная через ФАПЧ;

**RC** – тактовая частота с выхода встроенного RC-генератора;

**K2, K1, K0** – коэффициент умножения ФАПЧ.

<table className="table">
<tbody>

  <tr>
    <th >K2</th>
    <th >K1</th>
    <th >K0</th>
    <th >Коэффициент умножения блока PLL</th>
    
  </tr>

  <tr>
    <td  >0</td>
    <td  >0</td>
    <td  >0</td>
    <td  >2</td>
  </tr>
    <tr>
    <td  >0</td>
    <td  >0</td>
    <td  >1</td>
    <td  >4</td>
  </tr>
    <tr>
    <td  >0</td>
    <td  >1</td>
    <td  >0</td>
    <td  >8</td>
  </tr>
    <tr>
    <td  >0</td>
    <td  >1</td>
    <td  >1</td>
    <td  >16</td>
  </tr>
    <tr>
    <td  >1</td>
    <td  >0</td>
    <td  >0</td>
    <td  >32</td>
  </tr>
    <tr>
    <td  >1</td>
    <td  >0</td>
    <td  >1</td>
    <td  >64</td>
  </tr>
    <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >0</td>
    <td  >128</td>
  </tr>
    <tr>
    <td  >1</td>
    <td  >1</td>
    <td  >1</td>
    <td  >256</td>
  </tr>
 
</tbody>
</table>
При умножении частоты с помощью блока PLL стоит учитывать, что итоговая частота не должна превышать 8 МГц.

При записи в биты RC_C регистра ANALOG_O_RC максимального значения 7Fh, а в биты RC_R регистра ANALOG_O_RC_R минимального значения 0 – частота RC-генератора будет не более 90 кГц.

При записи в биты RC_C регистра ANALOG_O_RC минимального значения 0, а в биты RC_R регистра ANALOG_O_RC_R максимального значения 7 – частота RC-генератора будет не менее 400 кГц

### ANALOG_O_RC

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
    <td  >Резерв</td>
    <td  colSpan={7} >RC_C</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**RC_C** – настройка емкости конденсатора RC-генератора.

### ANALOG_O_REF

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
    <td  colSpan={2} >Резерв</td>
    <td  >OA_C_EN</td>
    <td  colSpan={5} >V_REF</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**OA_C_EN** – включение конденсаторов частотной коррекции МОУ:

- 1 – конденсаторы частотной коррекции включены;
- 0 – конденсаторы частотной коррекции выключены.

**V_REF** – настройка выходного напряжения ИОН (вывод A0).

Перед работой с данным регистром рекомендуется ознакомится с пунктом <a href="/docs/5400TP105-003/mk-main#важные-замечания-при-работе-с-микросхемой">важные замечания при работе с микросхемой</a>.

### ANALOG_O_RC_R

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
    <td  >BOR</td>
    <td  >RC_OUT_DISABLE</td>
    <td  >REF_OUT_DISABLE</td>
    <td  >TM_CLK_TYPE</td>
    <td  >Резерв</td>
    <td  colSpan={3} >RC_R</td>
  </tr>

   <tr>
    <th >Начальное значение</th>
    <td  colSpan={8} >0</td>
  </tr>
  
</tbody>
</table>

**BOR** – супервизор питания:

- 1 – внешний (вывод BOR_EXT/PGM при TM = 0);
- 0 – внутренний.

**RC_OUT_DISABLE** – определение источника тактового сигнала на выводе GPIOB&lt;1&gt;/RC_CLK_OUT при активном тестовом режиме.

**REF_OUT_DISABLE** – отключение подачи напряжения с ИОН на вывод A0/OUT_REF при активном тестовом режиме:

- 1 – напряжение не подается на вывод;
- 0 – напряжение подается на вывод.

**TM_CLK_TYPE** – определение источника тактового сигнала при активном тестовом режиме.

**RC_R** – настройка сопротивления резистора RC-генератора.

Перед работой с данным регистром рекомендуется ознакомится с пунктом <a href="/docs/5400TP105-003/mk-main#важные-замечания-при-работе-с-микросхемой">важные замечания при работе с микросхемой</a>.

### Типовое значение частоты генератора

<table className="table">
<tbody>

  <tr>
    <th rowSpan={2} >Биты RC_R регистра ANALOG_O_RC_R</th>
    <th colSpan={3}>Биты RC_C регистра ANALOG_O_RC</th>
  </tr>

   <tr>
    <td >000 000</td>
    <td  >. . .</td>
    <td  >111 111</td>
  </tr>

   <tr>
    <th >000</th>
    <td >~900 кГц</td>
    <td >. . .</td>
    <td >~45 кГц</td>
  </tr>
  <tr>
    <th >001</th>
    <td >~1280 кГц</td>
    <td >. . .</td>
    <td >~85 кГц</td>
  </tr>
  <tr>
    <th >010</th>
    <td >~1500 кГц</td>
    <td >. . .</td>
    <td >~120 кГц</td>
  </tr>
  <tr>
    <th >011</th>
    <td >~1650 кГц</td>
    <td >. . .</td>
    <td >~150 кГц</td>
  </tr>
   <tr>
    <th >100</th>
    <td >~1750 кГц</td>
    <td >. . .</td>
    <td >~190 кГц</td>
  </tr>
  <tr>
    <th >101</th>
    <td >~1850 кГц</td>
    <td >. . .</td>
    <td >~220 кГц</td>
  </tr>
  <tr>
    <th >110</th>
    <td >~1940 кГц</td>
    <td >. . .</td>
    <td >~250 кГц</td>
  </tr>
  <tr>
    <th >111</th>
    <td >~2000 кГц</td>
    <td >. . .</td>
    <td >~280 кГц</td>
  </tr>
</tbody>
</table>

Указанные диапазоны типовые и могут отличаться в конкретной микросхеме и климатических условиях. При необходимости, если требуемая частота не подобрана в текущем диапазоне настройки R, рекомендуется подбирать максимально близкую к требуемой в других диапазонах.
