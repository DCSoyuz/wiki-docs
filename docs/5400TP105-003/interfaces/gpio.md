---
id: mk-gpio
title: GPIO
sidebar_label: GPIO
sidebar_position: 1
---

Интерфейс ввода/вывода общего назначения для связи между компонентами микроконтроллера и различными периферийными устройствами.

## Общая информация

Мультиплексор GPIO_MUX для каждого вывода микроконтроллера позволяет либо соединить его с портом P процессора (использовать как вывод общего назначения), либо соединить его с одним из периферийных устройств (использовать альтернативную функцию порта). Выбор альтернативной функции осуществляется записью в регистры GPIO_ALTF0 и GPIO_ALTF1.

Если вывод используется как вывод общего назначения, то блок GPIO позволяет настроить его на вход или на выход. Выбор направления для порта осуществляется записью в регистры GPIO_DIR_SET/GPIO_DIR_CLR.

Когда порт настроен как выход общего назначения, то передаваемое во вне значение определяется значением порта P процессора. Когда порт настроен как вход общего назначения, то считать значение порта можно также через порт P процессора. Порты процессора соединены с блоками GPIO следующим образом:

- Порт P0 соединен с GPIOA;
- Порт P2 соединен с GPIOB;
- Порт P3 соединен с GPIOC.

Блок GPIO может сформировать прерывание при определенном уровне или изменении уровня на порту микроконтроллера.

Блок GPIO может зафиксировать фронт сигнала на выводе микроконтроллера, даже когда система находится в режиме «Глубокого сна» (c помощью асинхронного детектора фронта), и вывести систему из режима «SLEEP».

## Структурная схема

<div className="doc-image-container">
<figure>
  <img src="/img/5400TP105-003/gpio/Структурная_схема_GPIO.svg" alt="" />
  <figcaption  className="doc-image-container__image-title">Структурная схема GPIO для одного из выводов микроконтроллера</figcaption>
</figure>
</div>

GPIO_MUX соединяет PAD (вывод микроконтроллера) либо с портом P процессора (CPU_PORT_P), либо с одной из альтернативных функций этого вывода. GPIO_MUX управляется регистрами ALTF. Если вывод соединен с портом процессора, то направление (вход/выход) определяется регистром DIR. Если вывод соединен с альтернативной функцией, то направление (вход/выход) определяется этой альтернативной функцией (периферийным устройством DEVICEx).

В блоке GPIO присутствуют два детектора, способных формировать прерывания - синхронный (SYNCH_EDGE_DETECTOR) и асинхронный (ASYNCH_EDGE_DETECTOR). Работа детекторов управляются регистрами INTEN, INTPOL и INTTYPE. Статус прерываний сохраняется в регистре INT.

## Статусы и прерывания

GPIO поддерживает два режима регистрации событий - синхронный и асинхронный. Синхронный детектор работает в рабочем режиме и в режиме «Сон процессора», но не работает в режиме «Глубокий сон». Асинхронный детектор, наоборот работает только в режиме «Глубокий сон» и предназначен для вывода системы из него по внешнему сигналу.

Прерывание для каждого из выводов разрешается и запрещается записью в регистры GPIO_INTEN_SET/ GPIO_INTEN_CLR.

Синхронное прерывание может быть сформировано как по фронту сигнала, так и по уровню, выбор типа прерывания осуществляется записью в регистры GPIO_INTTYPE_SET/GPIO_INTTYPE_CLR. Регистры GPIO_INTPOL_SET/GPIO_INTPOL_CLR определяют, какой уровень (низкий/высокий) или какой фронт (возрастающий/спадающий) вызовет прерывание.

Асинхронный детектор не использует системную частоту, поэтому может работать в режиме «Глубокого сна» микроконтроллера. Асинхронное прерывание выводит микроконтроллер из режима «SLEEP», таким образом блок GPIO можно использовать, чтобы выйти из режима «Глубокого сна» по внешнему событию. Асинхронный детектор фронта работает с несинхронизированным на системную частоту входным сигналом, поэтому даже короткий глитч входного сигнала будет гарантированно зарегистрирован как фронт.

Асинхронное прерывание может быть сформировано только по фронту. При переходе в режим «Глубокого сна» (где работает асинхронный детектор) значение в регистрах GPIO_INTTYPE_SET/ GPIO_INTTYPE_CLR игнорируется, прерывание срабатывает по фронту сигнала (возрастающему или спадающему, в зависимости от GPIO_INTPOL_SET/GPIO_INTPOL_CLR).

Какой именно вывод вызвал прерывание можно выяснить, прочитав регистр статуса прерываний GPIO_INT. Соответствующий бит в регистре GPIO_INT выставляется в «1», только если прерывание по этому выводу разрешено.

## Регистры GPIO

<table className="table">
<tbody>
 
  <tr>
    <th >№</th>
    <th >Аббревиатура</th>
    <th >Доступ</th>
    <th >Описание</th>
  </tr>

  <tr>
    <th colSpan={4}>GIOA</th>
  </tr>

  <tr>
    <td >2300h</td>
    <td >GPIOA_DIR_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Установка режима работы выходного буфера</td>
  </tr>
  <tr>
    <td >2301h</td>
    <td >GPIOA_DIR_CLR</td>
    <td >RW</td>
    
  </tr>
  <tr>
    <td >2304h</td>
    <td >GPIOA_ALTF0</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор альтернативной функции</td>
  </tr>
  <tr>
    <td >2305h</td>
    <td >GPIOA_ALTF1</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2306h</td>
    <td >GPIOA_INTEN_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Разрешение прерываний</td>
  </tr>
  <tr>
    <td >2307h</td>
    <td >GPIOA_INTEN_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2308h</td>
    <td >GPIOA_INTTYPE_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор типа прерывания (фронт/уровень)</td>
  </tr>
  <tr>
    <td >2309h</td>
    <td >GPIOA_INTTYPE_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >230Ah</td>
    <td >GPIOA_INTPOL_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор полярности входного сигнала, при которой формируются прерывания</td>
  </tr>
  <tr>
    <td >230Bh</td>
    <td >GPIOA_INTPOL_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >230Ch</td>
    <td >GPIOA_INT</td>
    <td >R</td>
    <td >Статус прерываний</td>
  </tr>
  <tr>
    <th colSpan={4}>GPIOB</th>
  </tr>

  <tr>
    <td >2400h</td>
    <td >GPIOB_DIR_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Установка режима работы выходного буфера</td>
  </tr>
  <tr>
    <td >2401h</td>
    <td >GPIOB_DIR_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2404h</td>
    <td >GPIOB_ALTF0</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор альтернативной функции</td>
  </tr>
  <tr>
    <td >2405h</td>
    <td >GPIOB_ALTF1</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2406h</td>
    <td >GPIOB_INTEN_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Разрешение прерываний</td>
  </tr>
  <tr>
    <td >2407h</td>
    <td >GPIOB_INTEN_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2408h</td>
    <td >GPIOB_INTTYPE_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор типа прерывания (фронт/уровень)</td>
  </tr>
  <tr>
    <td >2409h</td>
    <td >GPIOB_INTTYPE_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >240Ah</td>
    <td >GPIOB_INTPOL_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор полярности входного сигнала, при которой формируются прерывания</td>
  </tr>
  <tr>
    <td >240Bh</td>
    <td >GPIOB_INTPOL_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >240Сh</td>
    <td >GPIOB_INT</td>
    <td >R</td>
    <td >Статус прерываний</td>
  </tr>

  <tr>
    <th colSpan={4}>GPIOC</th>
  </tr>

  <tr>
    <td >2500h</td>
    <td >GPIOC_DIR_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Установка режима работы выходного буфера</td>
  </tr>
  <tr>
    <td >2501h</td>
    <td >GPIOC_DIR_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2504h</td>
    <td >GPIOC_ALTF0</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор альтернативной функции</td>
  </tr>
  <tr>
    <td >2505h</td>
    <td >GPIOC_ALTF1</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2506h</td>
    <td >GPIOC_INTEN_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Разрешение прерываний</td>
  </tr>
  <tr>
    <td >2507h</td>
    <td >GPIOC_INTEN_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2508h</td>
    <td >GPIOC_INTTYPE_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор типа прерывания (фронт/уровень)</td>
  </tr>
  <tr>
    <td >2509h</td>
    <td >GPIOC_INTTYPE_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >250Ah</td>
    <td >GPIOC_INTPOL_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор полярности входного сигнала, при которой формируются прерывания</td>
  </tr>
  <tr>
    <td >250Bh</td>
    <td >GPIOC_INTPOL_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >250Сh</td>
    <td >GPIOC_INT</td>
    <td >R</td>
    <td >Статус прерываний</td>
  </tr>

</tbody>
</table>

### GPIOx_DIR_SET/CLR

GPIO_DIR_SET/GPIO_DIR_CLR – парные регистры управления режимом работы выходных буферов порта.

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
    <td >IO7_DIR</td>
    <td >IO6_DIR</td>
    <td >IO5_DIR</td>
    <td >IO4_DIR</td>
    <td >IO3_DIR</td>
    <td >IO2_DIR</td>
    <td >IO1_DIR</td>
    <td >IO0_DIR</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

Запись в **IOx_DIR** регистра GPIO_DIR_SET:

- 1 – включить выходной буфер на передачу;
- 0 – не меняет текущую настройку.

Запись в **IOx_DIR** регистра GPIO_DIR_CLR:

- 1 – выключить выходной буфер;
- 0 – не меняет текущую настройку.

Чтение **IOx_DIR** регистров GPIO_DIR_SET/GPIO_DIR_CLR:

- 1 – выходной буфер включен на передачу;
- 0 – выходной буфер выключен.

### GPIOx_ALTF0

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
    <td colSpan={2}>IO3_ALTF</td>
    <td colSpan={2}>IO2_ALTF</td>
    <td colSpan={2}>IO1_ALTF</td>
    <td colSpan={2}>IO0_ALTF</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

**IOx_ALTF** – альтернативная функция:

- 11b – включена альтернативная функция ALTF2;
- 10b – включена альтернативная функция ALTF1;
- 01b – включена альтернативная функция ALTF0;
- 00b – альтернативные функции выключены, выходным буфером управляет GPIO.

### GPIOx_ALTF1

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
    <td colSpan={2}>IO7_ALTF</td>
    <td colSpan={2}>IO6_ALTF</td>
    <td colSpan={2}>IO5_ALTF</td>
    <td colSpan={2}>IO4_ALTF</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

**IOx_ALTF** – альтернативная функция:

- 11b – включена альтернативная функция ALTF2;
- 10b – включена альтернативная функция ALTF1;
- 01b – включена альтернативная функция ALTF0;
- 00b – альтернативные функции выключены, выходным буфером управляет GPIO.

### GPIOx_INTEN_SET/CLR

GPIO_INTEN_SET/GPIO_INTEN_CLR – парные регистры установки разрешения генерации прерываний по событиям на входах GPIO.

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
    <td >IO7_IE</td>
    <td >IO6_IE</td>
    <td >IO5_IE</td>
    <td >IO4_IE</td>
    <td >IO3_IE</td>
    <td >IO2_IE</td>
    <td >IO1_IE</td>
    <td >IO0_IE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

Запись в **IOx_IE** регистра GPIO_INTEN_SET:

- 1 – разрешить генерацию прерывания по событиям на данном входе;
- 0 – не меняет текущую настройку.

Запись в **IOx_IE** регистра GPIO_INTEN_CLR:

- 1 – запретить генерацию прерывания по событиям на данном входе;
- 0 – не меняет текущую настройку.

Чтение **IOx_IE** регистров GPIO_INTEN_SET/GPIO_INTEN_CLR:

- 1 – разрешена генерация прерывания по событиям на данном входе;
- 0 – запрещена генерация прерывания по событиям на данном входе.

### GPIOx_INTTYPE_SET/CLR

GPIO_INTTYPE_SET/GPIO_INTTYPE_CLR – парные регистры установки типа прерывания (по фронту/уровню) генерируемого GPIO.

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
    <td >IO7_ITYPE</td>
    <td >IO6_ITYPE</td>
    <td >IO5_ITYPE</td>
    <td >IO4_ITYPE</td>
    <td >IO3_ITYPE</td>
    <td >IO2_ITYPE</td>
    <td >IO1_ITYPE</td>
    <td >IO0_ITYPE</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

Запись в **IOx_ITYPE** регистра GPIO_INTTYPE_SET:

- 1 – установить генерацию прерывания по фронту;
- 0 – не меняет текущую настройку.

Запись в **IOx_ITYPE** регистра GPIO_INTTYPE_CLR:

- 1 – установить генерацию прерывания по уровню;
- 0 – не меняет текущую настройку.

Чтение **IOx_ITYPE** регистров GPIO_INTTYPE_SET/GPIO_INTTYPE_CLR:

- 1 – генерация прерывания осуществляется по фронту;
- 0 – генерация прерывания осуществляется по уровню.

### GPIOx_INTPOL_SET/CLR

GPIO_INTPOL_SET/GPIO_INTPOL_CLR – парные регистры установки полярности события GPIO, по которому генерируется прерывание.

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
    <td >IO7_IPOL</td>
    <td >IO6_IPOL</td>
    <td >IO5_IPOL</td>
    <td >IO4_IPOL</td>
    <td >IO3_IPOL</td>
    <td >IO2_IPOL</td>
    <td >IO1_IPOL</td>
    <td >IO0_IPOL</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

Запись в **IOx_IPOL** регистра GPIO_INTPOL_SET:

- 1 – установить генерацию прерывания по положительному фронту или высокому уровню (зависит от GPIO_INTTYPE_SET/CLR);
- 0 – не меняет текущую настройку.

Запись в **IOx_IPOL** регистра GPIO_INTPOL_CLR:

- 1 – установить генерацию прерывания по отрицательному фронту или низкому уровню (зависит от GPIO_INTTYPE_SET/CLR);
- 0 – не меняет текущую настройку.

Чтение **IOx_IPOL** регистров GPIO_INTPOL_SET/GPIO_INTPOL_CLR:

- 1 – генерация прерывания осуществляется по положительному фронту или высокому уровню;
- 0 – генерация прерывания осуществляется по отрицательному фронту или низкому уровню.

### GPIOx_INT

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
    <td >IO7_INT</td>
    <td >IO6_INT</td>
    <td >IO5_INT</td>
    <td >IO4_INT</td>
    <td >IO3_INT</td>
    <td >IO2_INT</td>
    <td >IO1_INT</td>
    <td >IO0_INT</td>
  </tr>
    <tr>
    <th >Тип статуса</th>
    <td colSpan={8} >EVENT</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

**IOx_INT** – статус прерывания соответствующего вывода GPIO:

- 1 – был зафиксирован фронт или уровень (согласно заданным в регистрах GPIO_INTPOL_SET/CLR и GPIO_INTTYPE_SET/CLR условиям) на данном выводе;
- 0 – фронт или уровень не был зафиксирован.

## Альтернативные функции выводов GPIO

<table className="table">
<tbody>
 
  <tr>
    <th rowSpan={2}>№</th>
    <th rowSpan={2}>Вывод</th>
    <th colSpan={3}>Альтернативная функция</th>
    <th rowSpan={2}>Пяснение</th>
  </tr>

  <tr>
    <th >АФ1</th>
    <th >АФ2</th>
    <th >АФ3</th>
  </tr>

  <tr>
    <td colSpan={6}><b>Порт А</b></td>
    
  </tr>
  <tr>
    <td >20</td>
    <td >GPIOA_0</td>
    <td >SPI0_MOSI</td>
    <td >SPI1_MOSI</td>
    <td >I_TIMER0_EXT</td>
    <td >
    <ul >
        <li>SPI0/1 – MOSI (направление определяется режимом работы «ведущий»/«ведомый»)</li>
        <li>TIMER0 – I_TIMER0_EXT (вход)</li>
    </ul>
    </td>
  </tr>
    <tr>
    <td >21</td>
    <td >GPIOA_1</td>
    <td >SPI0_MISO</td>
    <td >SPI1_MISO</td>
    <td >I_TIMER1_EXT</td>
    <td >
    <ul >
        <li>SPI0/1 – MISO (направление определяется режимом работы «ведущий»/«ведомый»);</li>
        <li>TIMER1 – I_TIMER1_EXT (вход).</li>
    </ul>
    </td>
  </tr>
    <tr>
    <td >22</td>
    <td >GPIOA_2</td>
    <td >SPI0_SCK</td>
    <td >SPI1_SCK</td>
    <td >O_SLEEP</td>
    <td >
    <ul >
        <li>SPI0/1 – SCK (направление определяется режимом работы «ведущий»/«ведомый»);</li>
        <li>режим «Глубокий сон» – O_SLEEP (выход).</li>
    </ul>
    </td>
  </tr>
      <tr>
    <td >23</td>
    <td >GPIOA_3</td>
    <td >SPI0_I_CS</td>
    <td >SPI1_I_CS</td>
    <td >SPI0_O_CS</td>
    <td >
    <ul >
        <li>SPI0/1 – I_CS (вход);</li>
        <li>SPI0 – O_CS (выход).</li>
    </ul>
    </td>
  </tr>
      <tr>
    <td >24</td>
    <td >GPIOA_4</td>
    <td >UART0_TX</td>
    <td >UART1_TX</td>
    <td >SPI1_O_CS</td>
    <td >
    <ul >
        <li>UART0/1 – TX (выход);</li>
        <li>SPI1 – O_CS (выход).</li>
    </ul>
    </td>
  </tr>
      <tr>
    <td >25</td>
    <td >GPIOA_5</td>
    <td >UART0_RX</td>
    <td >UART1_RX</td>
    <td >«0»</td>
    <td >
    <ul >
        <li>UART0/1 – RX (вход);</li>
        <li>лог. «0» (выход).</li>
    </ul>
    </td>
  </tr>
      <tr>
    <td >26</td>
    <td >GPIOA_6</td>
    <td >I2C_SCL</td>
    <td >UART0_CTS</td>
    <td >UART1_CTS</td>
    <td >
    <ul >
        <li>I2C – SCL (направление определяется режимом работы «ведущий»/«ведомый»);</li>
        <li>UART0/1 – CTS (вход).</li>
    </ul>
    </td>
  </tr>
      <tr>
    <td >27</td>
    <td >GPIOA_7</td>
    <td >I2C_SDA</td>
    <td >UART0_RTS</td>
    <td >UART1_RTS</td>
    <td >
    <ul >
        <li>I2C – SDA (направление определяется протоколом);</li>
        <li>UART0/1 – RTS (выход).</li>
    </ul>
    </td>
  </tr>
      <tr>
    <td colSpan={6}>Порт В</td>
  </tr>
    <tr>
        <td >44</td>
        <td >GPIOB_0>/H_S</td>
        <td >SPI0_MOSI</td>
        <td >SPI1_MOSI</td>
        <td >I_TIMER0_EXT</td>
        <td >
        <ul >
            <li>при TM = 1 вывод принудительно работает как H/S (вход)</li>
            <li>во время обращения к внешним регистрам этот вывод работает как DATA_0 (направление определяется командой)</li>
        </ul>
        </td>
    </tr>
        <tr>
        <td >45</td>
        <td >GPIOB_1/RC_CLKOUT</td>
        <td >SPI0_MISO</td>
        <td >SPI1_MISO</td>
        <td >I_TIMER2_EXT</td>
        <td >
        <ul >
            <li>при TM = 1 вывод принудительно работает как RC_CLKOUT (выход);</li>
            <li>во время обращения к внешним регистрам этот вывод работает как DATA_1 (направление определяется командой)</li>
        </ul>
        </td>
    </tr>
        <tr>
        <td >46</td>
        <td >GPIOB_2</td>
        <td >SPI0_SCK</td>
        <td >SPI1_SCK</td>
        <td >O_SLEEP</td>
        <td >
        Во время обращения к внешним регистрам этот вывод работает как DATA_2 (направление определяется командой)
        </td>
    </tr>
        <tr>
        <td >47</td>
        <td >GPIOB_3</td>
        <td >SPI0_I_CS</td>
        <td >SPI1_I_CS</td>
        <td >SPI0_O_CS</td>
        <td >
        Во время обращения к внешним регистрам этот вывод работает как DATA_3 (направление определяется командой)
        </td>
    </tr>
        <tr>
        <td >48</td>
        <td >GPIOB_4</td>
        <td >UART0_TX</td>
        <td >UART1_TX</td>
        <td >SPI1_O_CS</td>
        <td >
        Во время обращения к внешним регистрам этот вывод работает как DATA_4 (направление определяется командой)
        </td>
    </tr>
        <tr>
        <td >1</td>
        <td >GPIOB_5</td>
        <td >UART0_RX</td>
        <td >UART1_RX</td>
        <td >«0»</td>
        <td >
        Во время обращения к внешним регистрам этот вывод работает как DATA_5 (направление определяется командой)
        </td>
    </tr>
        <tr>
        <td >2</td>
        <td >GPIOB_6</td>
        <td >I2C_SCL</td>
        <td >UART0_CTS</td>
        <td >UART1_CTS</td>
        <td >
        Во время обращения к внешним регистрам этот вывод работает как DATA_6 (направление определяется командой)
        </td>
    </tr>
        <tr>
            <td >3</td>
            <td >GPIOB_7</td>
            <td >I2C_SDA</td>
            <td >UART0_RTS</td>
            <td >UART1_RTS</td>
            <td >
                Во время обращения к внешним регистрам этот вывод работает как DATA_7 (направление определяется командой)
            </td>
    </tr>
    <tr>
        <td colSpan={6}><b>Порт С</b></td>
    </tr>
    <tr>
        <td >9</td>
        <td >GPIOC_0/TCK</td>
        <td >SPI0_MOSI</td>
        <td >SPI1_MOSI</td>
        <td >I_TIMER1_EXT</td>
        <td >
            <ul >
                <li>При TM = 1 вывод принудительно работает как TCK (вход) интерфейса JTAG</li>
                <li>Во время обращения к внешним регистрам этот вывод работает как WR/RD (выход)</li>
            </ul>
        </td>
    </tr>
        <tr>
        <td >10</td>
        <td >GPIOC_1/TMS</td>
        <td >SPI0_MISO</td>
        <td >SPI1_MISO</td>
        <td >I_TIMER2_EXT</td>
        <td >
            <ul >
                <li>При TM = 1 вывод принудительно работает как TMS (вход) интерфейса JTAG</li>
                <li>Во время обращения к внешним регистрам этот вывод работает как EN (выход)</li>
            </ul>
        </td>
    </tr>
        <tr>
        <td >11</td>
        <td >GPIOC_2/TDI</td>
        <td >SPI0_SCK</td>
        <td >SPI1_SCK</td>
        <td >O_SLEEP</td>
        <td >
            <ul >
                <li>При TM = 1 вывод принудительно работает как TDI (вход) интерфейса JTAG</li>
                <li>Во время обращения к внешним регистрам этот вывод работает как SEL_0 (выход)</li>
            </ul>
        </td>
    </tr>
        <tr>
        <td >12</td>
        <td >GPIOC_3/TDO</td>
        <td >SPI0_I_CS</td>
        <td >SPI1_I_CS</td>
        <td >SPI0_O_CS</td>
        <td >
            <ul >
                <li>При TM = 1 вывод принудительно работает как TDO (выход) интерфейса JTAG</li>
                <li>Во время обращения к внешним регистрам этот вывод работает как SEL_1 (выход)</li>
            </ul>
        </td>
    </tr>
        <tr>
        <td >13</td>
        <td >GPIOC_4</td>
        <td >UART0_TX</td>
        <td >UART1_TX</td>
        <td >SPI1_O_CS</td>
        <td >
        Порт ввода-вывода микроконтроллера, разряд №4 группы C
        </td>
    </tr>
        <tr>
        <td >14</td>
        <td >GPIOC_5</td>
        <td >UART0_RX</td>
        <td >UART1_RX</td>
        <td >«0»</td>
        <td >
        Порт ввода-вывода микроконтроллера, разряд №5 группы C
        </td>
    </tr>
        <tr>
        <td >15</td>
        <td >I2C_SCL</td>
        <td >UART0_CTS</td>
        <td >UART1_CTS</td>
        <td >«0»</td>
        <td >
        Во время обращения к внешним регистрам этот вывод работает как SEL_2 (выход)
        </td>
    </tr>
    <tr>
        <td >16</td>
        <td >GPIOC_7</td>
        <td >I2C_SDA</td>
        <td >UART0_RTS</td>
        <td >UART1_RTS</td>
        <td >
        Во время обращения к внешним регистрам этот вывод работает как SEL_3 (выход)
        </td>
    </tr>
</tbody>
</table>

Порты JTAG (TCK, TDI, TMS, TDO) мультиплексированы с портами GPIOC. Выбор назначения выводов (GPIOC или JTAG) осуществляется выводом TM.

Порты интерфейсов (SPI, UART и т.д.) также мультиплексированы с портами GPIO. Выбор назначения выводов осуществляется с помощью альтернативных функций во время работы микроконтроллера.
