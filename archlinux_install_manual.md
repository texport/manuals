## ArchLinux + btrfs с шифрованием + Gnome, инструкция по установке 2023

Ну вот накопилось у меня, особенно как я опробовал Windows 11. После установки любой версии Windows я всегда вычищал весь шлак который компания Microsoft туда напихала, меня всегда раздражало, что мне не дают выбора какой софт мне нужен, а какой нет. Но почти принудительно обязывать меня создать себе учетную запись для использования операционной системы, а еще после этого толкать мне рекламу приложений в меню пуск, это прям мощно!

Прежде чем написать эту инструкцию, я перепробовал большинство дистрибутивов(о да, про дистрибутивы это кончено же другая история) Linux из [distrowatch](https://distrowatch.com/dwres.php?resource=popularity "distrowatch"). Если идти по порядку, почему вообще Linux, я конечно понимаю что об этой ОС рассказали все кому не лень, но я перечислю то что важно для меня:
* Открытый исходный код
* Полный контроль над системой
* Бесплатный

Теперь конкретно почему мне зашел дистрибутив ArchLinux:
* Ничего лишнего, только то что тебе нужно
* Свежий софт(драйвера, ядро), я использую относительно новое железо
* Сообщество, оно огромное, всегда можно найти то что тебе нужно

Первым решил перевести свой рабочий ноут, кстати, ноут от компании Lenovo линейка ThinkPad модель T480. Обзор на него напишу в следующих постах. Ну и пойдем по порядку, что я делал. Инструкция для удобства будет разбита на этапы в порядке очередности.

### **Этап 1. Подготовка флешки**

Флешку готовил из под Windows 11.

Готовим флешку, я использовал актуальную на текущий момент версию [Rufus](https://rufus.ie/ru/), ну и конечно же сам дистрибутив [ArchLinux](https://archlinux.org/download/). В самом Rufus все стандартно, выбрал образ, остальное все оставил по умолчанию.

Как только флешка готова и образ был записан, подключаем ее в комп и грузимся с флешки.

### **Этап 2. Подключаем интернет**

Так как у меня ноутбук, я буду использовать WiFi.

Нам нужно запустить утилиту управления беспроводными сетями

```iwctl```

Смотрим какие у нас беспроводные интерфейсы есть в системе

```device list```

Сканируем WiFi сети

```station wlan0 scan``` (имя у моего интерфейса wlan0, у вас может быть по другому, вам нужно заменить на свой)

Получаем список доступных беспроводных сетей

```station wlan0 get-networks```

Выбираем беспроводную сеть, к которой мы хотим подключиться

```station wlan0 connect Internet-19``` (имя моей беспроводной сети Internet-19, вам нужно заменить на свое имя)

Вводим пароль для подключения к выбранной сети, если это требуется.

Выходим из утилиты управления беспроводными сетями

```exit```

Проверяем есть ли подключение к интернету

```ping -c2 archlinux.org```

### **Этап 3. Предварительная настройка**

Разработчика дистрибутива давно облегчили процесс установки дистрибутива ArchLinux с помощью утилиты archinstall. Для этого нам нужно ее запустить

```archinstall```

Далее я расскажу про каждый пункт в этой утилите.

Язык Archinstall - выбор языка, используемого при установке. Можно выбрать из списка доступных языков. Язык установки я меняю на Русский, можно оставить по умолчанию Английский.

```Язык Archinstall -> Русский```

Раскладка клавиатуры - выбор раскладки клавиатуры. Утилита предлагает автоматически определить раскладку или выбрать из списка. Обратите внимание, что если вы выберете неправильную раскладку, то это может привести к тому, что некоторые клавиши не будут работать во время установки, что может затруднить установку. Раскладку клавиатуры при установке я всегда оставляю us, дополнительную раскладку ru я добавляю уже после установки.

```Раскладка клавиатуры -> us```

Регион зеркала - параметр позволяет выбрать зеркало для загрузки пакетов из интернета. Вы можете выбрать любое зеркало из списка поддерживаемых зеркал. Обычно рекомендуется выбирать ближайшее зеркало, чтобы ускорить загрузку пакетов. В моем случае это Казахстан.

```Регион зеркала -> Kazakhstan```

Язык локали - параметр определяет язык и формат вывода информации в системе.

```Язык локали -> ru_RU.UTF-8```

Диск - параметр позволяет выбрать диск, на который будет установлена система. Вы можете выбрать любой диск из списка доступных дисков.

```Диск -> Выбрать диск```

Разметка диска - параметр позволяет выбрать схему разделов для диска. Вы можете выбрать одну из предварительно настроенных схем разделов или настроить свою собственную.

```Разметка диска -> Стереть все выбранные диски -> btrfs -> да -> да```

Пароль шифрования - при выборе данного пункта пользователь должен указать пароль, который будет использоваться для шифрования диска, на котором будет установлена система. Важно отметить, что данный пункт является обязательным при установке Arch Linux с шифрованием диска. Шифрование диска позволяет защитить данные на нем в случае утери или кражи устройства.

```Пароль шифрования -> 'вводим пароль пользователя' -> 'вводим пароль еще раз'```

Загрузчик - параметр позволяет выбрать загрузчик для системы. Вы можете выбрать любой загрузчик из списка поддерживаемых загрузчиков.

```Загрузчик -> нет```

Подкачка - это раздел на диске, который используется системой как дополнительная память при нехватке оперативной памяти. Когда системе не хватает оперативной памяти, она начинает использовать раздел подкачки, чтобы сохранить временно неиспользуемые данные и освободить оперативную память для более важных задач.

```Подкачка -> да```

Имя хоста - это уникальное имя, которое идентифицирует ваш компьютер в сети. Имя хоста должно быть уникальным в пределах сети, к которой вы подключены, и содержать только латинские буквы, цифры и дефисы.

```Имя хоста -> введите свое имя хоста```

Пароль root - это параметр пароля для учетной записи root. Учетная запись root - это суперпользователь в системе Linux, который имеет полный доступ ко всему компьютеру.

Я пропустил этот пункт установки. Но если вам нужно отдельно использовать root

```Пароль root -> 'вводим пароль пользователя' -> 'вводим пароль еще раз'```

Учетная запись пользователя - параметр позволяет создать учетную запись пользователя и задать ее параметры. Вы можете настроить имя пользователя, пароль и дополнительные параметры, такие как домашний каталог и права доступа.

```Учетная запись пользователя -> Добавить пользователя -> 'вводим имя своего пользователя без пробелов' -> 'вводим пароль пользователя' -> 'вводим пароль еще раз' -> да -> Подтвердить и выйти```

Профиль - позволяет выбрать готовый набор настроек и программ, которые будут установлены в вашей системе. Это удобно, когда вы хотите установить Arch Linux с уже предустановленными настройками и программами, соответствующими определенной цели использования вашего компьютера.

```Профиль -> desktop -> gnome -> All open-source```

Звуковой сервер - звуковой сервер обеспечивает управление звуковыми устройствами в вашей системе и позволяет различным приложениям использовать звуковые ресурсы.

PulseAudio - является более стабильной и широко используемой звуковой системой
PipeWire является более современной и мощной звуковой системой с большей гибкостью и расширяемостью.

```Звуковой сервер -> pipewire```

Ядра - какое ядро Linux будет установлено на систему. В качестве параметра можно указать один из следующих вариантов:

linux - устанавливает стандартное ядро Linux
linux-lts - устанавливает ядро Linux с долгосрочной поддержкой (Long-Term Support)
linux-hardened - устанавливает ядро Linux, которое содержит дополнительные функции безопасности

```Ядра -> linux-lts```

Дополнительные пакеты - могут включать в себя программное обеспечение, которое не входит в стандартный набор пакетов Arch Linux. Например, это может быть графический интерфейс для управления сетью, дополнительные инструменты разработки или пакеты для работы с определенными форматами файлов. При выборе дополнительных пакетов пользователю следует учитывать свои потребности и требования к системе.

```Дополнительные пакеты -> base-devel git neofetch```

Настройка сети - какая конфигурация сети будет использоваться. Выбрав NetworkManager вам не нужно будет ручным образом настраивать сетевые соединения в файле конфигурации. NetworkManager будет автоматически обнаруживать и настраивать доступные сетевые устройства, а также устанавливать и настраивать соединения согласно вашим настройкам.

```Настройка сети -> Использовать NetworkManager```

Часовой пояс - можно выбрать нужный часовой пояс для вашей системы. Вы можете прокручивать список вверх и вниз, чтобы найти нужный часовой пояс, или воспользоваться поиском по ключевым словам.

```Часовой пояс -> выберите свой часовой пояс```

Автоматическая синхронизация времени - включение автоматической синхронизации времени важно для правильной работы системы и установки корректных временных меток на файлы и события. 

```Автоматическая синхронизация времени -> да```

Дополнительные репозитории - позволяет добавить дополнительные репозитории в вашу систему Arch Linux. Я ничего не выбирал, оставил пустым.

```Дополнительные репозитории -> выберите нужные репозитории```

### **Этап 4. Установка**

После того как в каждом пункте утилиты archinstall выбрали необходимые параметры нажимаем

```Установить```

На вопрос какой раздел зашифровать нажимаем Enter и ждем пока установка завершится.

После завершения установки archistall спросит у вас о том хотите ли вы прямо сейчас перейти в режим chroot, выбираем

```нет```

Перезагружаем компьютер

```reboot```

Не забываем ввести пароль от зашифрованного диска.

Поздравляю, вы завершили процесс установки. В следующей инструкции расскажу о том как настройки в ArchLinux я делаю под себя.



