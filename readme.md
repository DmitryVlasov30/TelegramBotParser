# Что это и зачем нужно:
Этот проект создан для преподавателей олимпиадных групп по программированию. Это бот в телеграмме, который собирает информацию с сайта [Codeforces](https://codeforces.com), а именно с приватных групп для того, чтобы информировать преподавателя о новых попытках решения задач своими учениками. Бот упростит работу преподавателя, потому что ему не придётся лишний раз отвлекаться от своих дел и заходить на сайт, а так же бот поможет преподавателю быстро отреагировать на ошибки своих учеников.

----
# Что использовал и с какими проблемами встретился:

В этом проекте я использовал Python с библиотеками:

* **[aiogram](https://docs.aiogram.dev/en/dev-3.x/)** 

* **[selenium](https://pypi.org/project/selenium/)**

* **[datetime](https://docs.python.org/3/library/datetime.html)**

* **[apscheduler](https://pypi.org/project/APScheduler/)** 

* **[asyncio](https://docs.python.org/3/library/asyncio.html)** 

Хотелось бы рассказать о проблеме, с которой я столкнулся при парсинге данных с сайта и почему я использовал `selenium`, а не например `request` в связке с `BeautifulSoup4`. Проблема в том, что для получения данных с приватных групп нужно с начала авторизоваться в аккаунте, где есть доступ к данным, а из-за того что на сайте во вкладке [API](https://codeforces.com/apiHelp) нет информации про то как получить данные через обращение на сервер, то я попытался авторизоваться на сайте через библиотеку request и вытащить данный из html с помощью BeautifulSoup4, но через обычное создание сессии сайт не позволял авторизоваться на нем, поэтому я решил отпарсить данные через библиотеку selenium и попытался по максимуму оптимизировать сборку данных по времени, используя явные ожидания. 

----
# Как запустить бота и его основные функции:

### Создание бота через [BotFather](https://t.me/BotFather)

1. Перейдите в [BotFather](https://t.me/BotFather)
2. Введите команду **/newbot**
3. Введите имя и адрес бота
4. После этого бот пришлет вам сообщение, содержащее токен для HTTP API

В дальнейшем вы сможете редактировать своего бота, введя **/mybots** в @BotFather

### Копирование данных

Вы можете скопировать данные любым из трех способов:
* Использовав функцию git clone с любым из трёх аргументов `HTTP`, `SSH`, `GitHub CLI` в инициализированном репозитории
* Скопировать все файлы на ваш компьютер
* Самый лёгкий способ - просто скачать ZIP архив

### Вставка значений переменных из файла [main.py](https://github.com/DmitryVlasov30/TelegramBotParser/blob/main/main.py)
1. В переменную `token` HTTP API токен из [BotFather](https://t.me/BotFather)
2. В переменную `chat_id` ваш chat_id объяснение как его получить есть [тут](https://pikabu.ru/story/kak_uznat_identifikator_telegram_kanalachatagruppyi_kak_uznat_chat_id_telegram_bez_botov_i_koda_11099278) 
3. В переменную `login` ваш логин с сайта [codeforces](https://codeforces.com/)
4. В переменную `password` ваш пароль с того же сайта
5. При отправке бота на сервер в переменную `number_proxy_server` нужно вставить прокси через, который будет работать бот, а так же убрать решетку в начале строки в переменной `session`, которая находится в функции main и убрать решетку под комментарием `надо для сервера`
6. В переменной `interval_requests` нужно поставить время в секундах - это интервал между, которым будет обновляться информация с сайта (рекомендую не менее 60 секунд, зависит от скорости интернета где будет работать бот и от загруженности сайта)



#### Так же хотелось бы сказать что сервер нужно выбирать с не менее чем 4cpu и 8ram

\
После запуска можно добавить группы, из которых бот будет собирать информацию это можно сделать так: `/add "точное название группы без кавычек"`, после этого бот добавит эту группу в список. Но что же будет если указать неправильную группу? Бот удалит эту группу из списка и сообщит, что этой группы нет в вашем аккаунте на codeforces. Так же группы можно удалять из списка с помощью сообщения: `/delete "точное название группы без кавычек"`. Так же если бот не сможет обратиться на сайт или произойдёт какая - либо другая ошибка, то бот проинформирует вас об этом, если же бот после этого смог обратиться на сайт без вашего вмешательства, то бот вас об этом так же проинформирует.

### Команды: 

* **/my_groups** -> возвращает список с вашими группами

* **/off** -> приостанавливает работу бота, а именно перестаёт вызывать функцию, которая парсит информацию с сайта

* **/on** -> возобновляет работу функции

* **/status** -> возвращает сообщение о работоспособности бота

* **/add (название группы)** -> добавляет группу в список отслеживаемых групп

* **/delete (название группы из списка, возвращаемого командой `/my_groups`)** -> удаляет группу из списка отслеживаемых групп
----
# Планы на продолжение проекта:
Я бы хотел добавить функцию для сбора данных и записи их в какую либо базу данных или Google Sheets, эту функцию можно было бы использовать например для подведения итогов какого либо промежутка времени, чтобы анализировать успехи учеников.