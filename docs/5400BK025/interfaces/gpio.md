---
id: mk025-gpio
title: GPIO
sidebar_label: GPIO
sidebar_position: 1
---

## Общая информация

Мультиплексор GPIO_MUX для каждого вывода микроконтроллера позволяет либо соединить его с портом P процессора (использовать как вывод общего назначения), либо соединить его с одним из периферийных устройств (использовать альтернативную функцию порта). Выбор альтернативной функции осуществляется записью в регистр GPIO_ALTFL.

Если вывод используется как вывод общего назначения, то блок GPIO позволяет настроить его на вход или на выход. Выбор направления для порта осуществляется записью в регистры GPIO_DIR_SET / GPIO_DIR_CLR.

Когда порт настроен как выход общего назначения, то передаваемое во вне значение определяется значением порта P процессора. Когда порт настроен как вход общего назначения, то считать значение порта можно также через порт P процессора. Порт P0 процессора соединён с блоками GPIO.

Блок GPIO может сформировать прерывание при определенном уровне или изменении уровня на порту микроконтроллера.

Блок GPIO может зафиксировать фронт сигнала на выводе микроконтроллера, даже когда система находится в режиме «Глубокого сна» (c помощью асинхронного детектора фронта), и вывести систему из режима «SLEEP».

Аналогичным и единственным способом вывода системы из режима «COLD_SLEEP» является подача положительного фронта на вход любого GPIO. Через такт системной частоты система продолжит работать с той инструкцией, на которой остановилась.

## Структурная схема

<div className="doc-image-container">
<figure>
  <img src="/img/5400ВК025/gpio/Структурная_схема_GPIO.svg" alt="" />
  <figcaption  className="doc-image-container__image-title">Структурная схема GPIO для одного из выводов микроконтроллера</figcaption>
</figure>
</div>

GPIO_MUX соединяет PAD (вывод микроконтроллера) всегда соединенный с портом P процессора (CPU_PORT_P), с одной из альтернативных функций этого вывода. GPIO_MUX управляется регистрами GPIO_ALTFL. Если вывод соединен с портом процессора, то направление (вход/выход) определяется регистром GPIO_DIR_SET / GPIO_DIR_CLR. Если вывод соединен с альтернативной функцией, то направление (вход/выход) определяется этой альтернативной функцией (периферийным устройством DEVICEx).

В блоке GPIO присутствуют два детектора, способных формировать прерывания – синхронный (SYNCH_EDGE_DETECTOR) и асинхронный (ASYNCH_EDGE_DETECTOR). Работа детекторов управляются регистрами GPIO_INTEN_SET / GPIO_INTEN_CLR, GPIO_INTTYPE_SET / GPIO_INTTYPE_CLR и GPIO_INTPOL_SET / GPIO_INTPOL_CLR. Статус прерываний сохраняется
в регистре GPIO_INT.

## Статусы и прерывания

GPIO поддерживает два режима регистрации событий – синхронный и асинхронный. Синхронный детектор работает в рабочем режиме и в режиме «Сон процессора», но не работает в режиме «Глубокий сон». Асинхронный детектор, наоборот работает только в режиме «Глубокий сон»
и предназначен для вывода системы из него по внешнему сигналу.

Прерывание для каждого из выводов разрешается и запрещается записью в регистры GPIO_INTEN_SET / GPIO_INTEN_CLR.
Синхронное прерывание может быть сформировано как по фронту сигнала, так и по уровню, выбор типа прерывания осуществляется записью в регистры GPIO_INTTYPE_SET / GPIO_INTTYPE_CLR. Регистры GPIO_INTPOL_SET / GPIO_INTPOL_CLR определяют, какой уровень (низкий/высокий) или какой фронт (возрастающий/спадающий) вызовет прерывание.

Асинхронный детектор не использует системную частоту, поэтому может работать в режиме «Глубокого сна» микроконтроллера. Асинхронное прерывание выводит микроконтроллер из режима «SLEEP», таким образом блок GPIO можно использовать, чтобы выйти из режима «Глубокого сна» по внешнему событию. Асинхронный детектор фронта работает с несинхронизированным на системную частоту входным сигналом, поэтому даже короткий глитч входного сигнала будет гарантированно зарегистрирован как фронт.

Асинхронное прерывание может быть сформировано только по фронту. При переходе в режим «Глубокого сна» (где работает асинхронный детектор) значение в регистрах GPIO_INTTYPE_SET / GPIO_INTTYPE_CLR игнорируется, прерывание срабатывает по фронту сигнала (возрастающему или спадающему, в зависимости от GPIO_INTPOL_SET / GPIO_INTPOL_CLR).

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
    <td >2300h</td>
    <td >GPIO_DIR_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Установка режима работы выходного буфера</td>
  </tr>
  <tr>
    <td >2301h</td>
    <td >GPIO_DIR_CLR</td>
    <td >RW</td>
    
  </tr>
  <tr>
    <td >2304h</td>
    <td >GPIO_ALTFL</td>
    <td >RW</td>
    <td >Выбор альтернативной функции</td>
  </tr>

  <tr>
    <td >2305h</td>
    <td >GPIO_INTEN_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Разрешение прерываний</td>
  </tr>
  <tr>
    <td >2306h</td>
    <td >GPIO_INTEN_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2307h</td>
    <td >GPIO_INTTYPE_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор типа прерывания (фронт/уровень)</td>
  </tr>
  <tr>
    <td >2308h</td>
    <td >GPIO_INTTYPE_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >2309h</td>
    <td >GPIO_INTPOL_SET</td>
    <td >RW</td>
    <td rowSpan={2}>Выбор полярности входного сигнала, при которой формируются прерывания</td>
  </tr>
  <tr>
    <td >230Ah</td>
    <td >GPIO_INTPOL_CLR</td>
    <td >RW</td>
  </tr>
  <tr>
    <td >230Bh</td>
    <td >GPIO_INT</td>
    <td >R</td>
    <td >Статус прерываний</td>
  </tr>

</tbody>
</table>

### GPIO_DIR_SET/CLR

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

### GPIO_ALTFL

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
    <td >IO7_ALTF</td>
    <td >IO6_ALTF</td>
    <td >IO5_ALTF</td>
    <td >IO4_ALTF</td>
    <td >IO3_ALTF</td>
    <td >IO2_ALTF</td>
    <td >IO1_ALTF</td>
    <td >IO0_ALTF</td>
  </tr>
  <tr>
    <th >Назначение</th>
    <td colSpan={2} >IO3_ALTF</td>
    <td colSpan={2} >IO2_ALTF</td>
    <td colSpan={2} >IO1_ALTF</td>
    <td colSpan={2} >IO0_ALTF</td>
  </tr>

  <tr>
    <th >Начальное значение</th>
    <td colSpan={8} >0</td>
  </tr>
</tbody>
</table>

**IOx_ALTF** – альтернативная функция:

- 1 – включена альтернативная функция ALTFL;
- 0 – альтернативные функции выключены, выходным буфером управляет GPIO.

### GPIO_INTEN_SET/CLR

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

### GPIO_INTTYPE_SET/CLR

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

### GPIO_INTPOL_SET/CLR

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

### GPIO_INT

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
