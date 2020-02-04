# Что такое операционная система и как она работает?

> Основа конспекта, лекция - https://www.youtube.com/watch?v=hb9CTGSJm88&list=PLlb7e2G7aSpRgsZVTYYbpqiFrIcIpf8kp

Операционные системы окружают нас повсюду – персональные компьютеры, серверы, мобильные устройства (телефон, планшет), сетевые устройства (роутеры, коммутаторы) и даже современные автомобили (борт-компьютер), телевизоры и прочее. Перечислять можно очень долго, ведь они требуются практически в каждой компьютерной системе.
<br>

## Введение <br>
Любой компьютер представляет собой связанную совокупность: **процессора, памяти и устройств ввода-вывода**.

<img src="img\basic_architecture.png" width="450px" hidth="450px">
<details> <summary>Более подробная структура ПК</summary>
    <img src="img\Motherboard_diagram_ru.jpg" width="575px" hidth="300px">
</details>

Сама по себе, аппаратура умеет делать только очень простые, базовые операции, и получается, что непосредственное *создание, выполнение и управление* сложными процессами (приложениями) на аппаратуре становится крайне неэффективным и неудобным.

Например, **процессор** может выполнять только три базовых типа инструкции: 

- *Чтение инструкций/данных из памяти (read)*
- *Выполнение интрукции (execute)*
- *Запись результата в память (write)*

### *Немного истории*
> На заре компьютерной эпохи, первые компьютеры представляли собой огромные блоки (занимавшие большие комнаты), в которых размещались основные его компоненты: **процессор, память и устройства ввода-вывода**. <br>
> Любое взаимодействие с компьютером подразумевало **ручное изменение или считывание** состояния памяти (непосредственно или с помощью перфокарт). <br>
> И всего можно было выделить два состояния, в котором, в реальном времени находится компьютерная система:
> - Ввод/Вывод
> - Вычисление
>
>
> **Важная идея!**<br>
> Так как **вычисления производятся быстрее**, чем непосредственный ввод-вывод данных, разработчикам пришла идея о том, что к ресурсам можно допускать не одного пользователя (**процесс**), а множество, предоставляя им способ независимо друг от друга загружать (ввод) и получать (вывод) данные, чтобы более эффективно использовать ресурсы компьютера и вычислительные модули не простаивали в ожидании.
>
> Эта идея положила начало созданию такой системы, которую мы теперь называем *операционной* - программной системы, которая осуществляет доступ к ресурсам компьютера и, следовательно, управляет **процессами**.

Идея *многопользовательского режима* в использовании ресурсов компьютера нашла свою реализацию в понятии **процесс**. То есть, **каждый процесс - это пользователь ресурсов компьютера**.

> Далее, термины: *процесс, приложение* идут как синонимы термину *пользователь ресурсов*.

## Зачем нужна Операционная Система?<br>

Чтобы управлять доступом пользователей (процессов) к ресурсам компьютера и осуществлять другие *системные функции*, и были разработаны **операционные системы**.

***Фунции ОС:***
- Абстракция оборудования для удобства и переносимости
    - то есть реализация единого интерфейса для разного, но схожего по функциям оборудования.
- Совместное использование процессоров группой приложений (многопользовательский доступ)
- Изоляция ошибок приложений друг от друга (и от ядра ОС)
- Переносимость данных между приложениями (процессами)
    - файлы и файловая система, Inter Process Communication (IPC)

***Основные абстракции ОС***
- Процессы и потоки
- Файлы и файловые системы
- Адресное пространство и память
- Сокеты, протоколы, устройства

## Положение ОС в уровневой иерархии организации компьютера

<img src="img\GeneralizedLayeredComputerStructure_OS.png" width="650px" hidth="1150px">

Современный компьютер можно представить в виде **иерархии уровней** (от двух и более), где на каждом уровне выделяются свои абстракции и набор возможных функций.

Операционная система является одним из таких уровней и представляет собой **интерфейс** ("прослойку") между пользователем ресурсов компьютера и самими ресурсами, обеспечивающий управление взаимодействием между *пользователь-ресурс*, так и взаимодействием *пользователь-пользователь* и *устройство-устройство*.

В целом, наиболее *общей схемой* это можно отобразить так:<br>
<img src="img\OS-OS_1.png" width="325px" hidth="150px">

## Как приложения взаимодействуют с ОС?
Взаимодействие процессов с ОС осуществляется с помощью **системных вызовов**.<br>
**Системные вызовы** — это интерфейс, который предоставляет ядро ОС (**kernel space**) пользовательским процессам (**user space**).

> **Интерфейс** — способ взаимодействия, некий набор правил и средств.
> **Kernel space** — адресное пространство ядра ОС, в котором процессы имеют привилегированный доступ к ресурсам компьютера и другим процессам.<br>
> **User space** — адресное пространство, отведённое для пользовательских процессов (программ).

Например, чтобы выполнить обычное действие, с точки зрения прикладного программиста, – вывод строки в консоль, необходимо загрузить исполнимый код в память компьютера и передать его процессору. С помощью *системных вызовов*, всё это делает **запускающий** процесс (уже запущенный процесс, из которого вызывается новый процесс; одни процессы порождают другие) и передаёт управление. 

То есть **системные вызовы** выполняют те рутинные действия, которые раньше осуществлялись вручную, — загрузка кода программы в память, передача его на исполнение процессору и прочее.

*Схема организации ОС расширяется следующим образом:*<br>
<img src="img\OS-OS_2.png" width="325px" hidth="150px">

## Как оборудование (hardware) взаимодействует с ОС?

Одной из функций ОС является — **абстрагирование оборудования**.

*Что это значит?*<br>
У каждого оборудования есть свой фиксированный интерфейс. Например, операции с флешкой, жестким диском и сетевой платой будут похожи по своему типу - "записать/считать данные". Но у каждого устройства для этого, тем не менее, будет свой интерфейс.

ОС должка выполнять одни и те же операции над разными типами устройств. И чтобы она выполняла их *однообразно* — нужно чтобы был **общий интерфейс**. Реализацией этого *общего интерфейса* занимаются специальные программы - **драйверы устройств**. То есть, ОС обращается к *драйверам устройств* используя однотипные команды *"отправить команду/считать/записать"*, а *драйвера* уже превращает эти команды в то, что понимает конкретное устройство.

*Схема организации ОС расширяется следующим образом:*<br>
<img src="img\OS-OS_3.png" width="325px" hidth="150px">

## Что делает ядро ОС?

**Ядро ОС** – центральная часть операционной системы. Причём, это **реакционный механизм**, то есть его работа заключается исключительно в *реакции* на какие-либо события для их последующей обработке.

*Что именно?*
- Обрабывает запросы приложений
    - *системные вызовы*
- Обрабывает запросы оборудования
    - *прерывания*
- Обеспечивает диспетчеризацию процессов (scheduling)
    - реализация *многопользовательского режима* доступа к ресурсам
    - **время работы процессора делится на фрагменты и они распределяются по процессам**
- Обрабатывает исключительные ситуации