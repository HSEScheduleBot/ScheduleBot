
## Requirements
* Python >= 3.6
* PostgreSQL


```

## Usage


```bash
    python run.py -h
    # or
    python run.py init.db  # create tables
    python run.py update_schedules
    python run.py run
```




1) HSE Schedule Bot
2) Бот для Telegram, который поможет студентам НИУ ВШЭ следить за своим расписанием на неделю
3) https://github.com/HSEScheduleBotTeam/ScheduleBot
4) Рамзан Султыгов 164 - Main Logic, Юлия Полынова 142 - Main Logic, Артем Кашенко 164 - Main Logic
5)

====================================

models

Используемая база данных - PostgreSql

------------------------------------
models.py
Архитектура базы данных

Users - объект записи в бд из таблицы users
    check_email - проверка строки на валидность email
    is_student_email - является ли email студенческим или преподским
    set_city - добавляет в объект записи город
    set_status - добавляет в объект записи статус
    set_email - добавляет в объект записи email

Lessons - объект записи в бд из таблицы lessons
Lecturers - объект записи в бд из таблицы lecturers

------------------------------------

tools.py
Работа с таблицами 

create_tables - создать объявленные таблицы
drop_tables - удалить объявленные таблицы

------------------------------------

update_schedules.py
Обновление расписания

main - запуск
get_users - получить всех пользователей
fetch_schedule - получить расписание для переданного email
format_lessons - преобразовать данные в нужный текстовый формат
format_day_schedule - отформатировать данные по дням
update_schedules - обновить данные в бд
get_and_save - запуск цепочки обновления


====================================


schedule
Работа с расписанием

------------------------------------

commons.py
Общие утилиты

get_lessons - получить уроки по telegram_id

------------------------------------

day.py
Раписание на сегодня и на завтра

log - декоратор логгера
typing - декоратор, посылающий статус "печатает" перед каждым сообщением от бота
on_day - расписание на сегодня
on_tomorrow - расписание на завтра (on_day с флагом)

------------------------------------

start.py
FSM расписания

on_schedule - отдает пользователю клавиатуру 
on_spam - ответ на сообщение, которое не ожидается
on_back - обработчик сообщения Назад
register - регистрирует в диспетчере входные точки FSM

------------------------------------

week.py
Расписание на неделю

on_week - отдает пользователю клавиатуру с днями недели
choose_dow - отдает пользователю расписание на выбранный день недели

====================================

service
Сервисные хэндлеры

------------------------------------
common_handlers.py

ask_email - спрашивает email пользователя
ask_city - спрашивает город пользователя
send_cancel - сбрасывает стейт
get_email - сохраняет email для дальнейшей обработки и проверки
get_city - сохраняет город для дальнейшей обработки и проверки
add_user - добавляет пользователя в базу данных
show_about - показывать информацию о боте
start - показывает приветственное сообщение

------------------------------------

mailing.py
Рассылка сообщений пользователям

send_message_from_bot - посылает сооющение от бота
do_mailing - начать рассылку
whom_to_send - выбрать кому рассылать
recipients - полусчить реципиентов
prepare_mailing - предобработка полученного текста

------------------------------------

settings.py
Заполнение второстепенных данных

on_settings - входная точка, выдает клавиатуру
choose_menu - соответсвующее меню для выбранного варианта
send_current - отправить текущие настройки


====================================

utils
Утилиты

functions.py

Булевы, проверяют подходит ли сообщение под паттерн
is_cancelled
is_stopped
is_back 

------------------------------------

keyboards - хранятся клавиатуры бота
messages - хранятся реплики бота
schema - хранятся маппинги
states - состояния FSM

====================================

tools.py

load_data - Загружает сохраненные стейты
save_data - сохраняет текущие стейты
save_state - сохраняет стейты раз в минуту в фоне
init_db - инициализация бд
run - запуск бота

====================================

run.py

Менеджер запусков
