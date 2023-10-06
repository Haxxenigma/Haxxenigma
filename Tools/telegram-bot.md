# Telegram Bot (for sending alerts about changes in database)

```shell
apt install mysql-server mysql-client
```

```shell
mysql -u root -p
```

```sql
create database dbname;

create user username@localhost identified by 'password';

grant all privileges on dbname.* to username@localhost;

use dbname;

create table tablename (
    id int auto_increment primary key,
    username nvarchar(50) not null,
    password nvarchar(100) not null
);

insert into tablename(username, password)
values  ("newUser", "newPass"),
        ("anotherUser", "strongPass");

delete from tablename
where username like '%';

quit;
```

```shell
pip install pyTelegramBotAPI
```

```shell
pip install pymysql
```

```shell
pip install tabulate
```

```yaml
token: https://t.me/BotFather
chat: https://t.me/userinfobot
```

```python
import telebot
import pymysql
import time
from tabulate import tabulate
import threading

token = "6421311991:AAEb8Zp2xln3lzqaHRbA3cGNudp-eAvZdtM"
chat = "5006697590"

db_host = "localhost"
db_user = "username"
db_pass = "password"
db_name = "dbname"
db_table = "tablename"

interval = 5

bot = telebot.TeleBot(token)


@bot.message_handler(commands=["start", "hello"])
def start(message):
    bot.reply_to(
        message,
        f"Hello, {message.from_user.first_name}! Monitoring of records in the database {db_name} and table {db_table} is enabled!",
    )


def send_message(message):
    bot.send_message(chat, message)


def check_records_count():
    try:
        connection = pymysql.connect(
            host=db_host, user=db_user, password=db_pass, database=db_name
        )
        with connection:
            with connection.cursor() as cursor:
                cursor.execute(f"SELECT COUNT(*) FROM {db_table}")
                count = cursor.fetchone()[0]
                return count
    except Exception as e:
        send_message(f"Error occured (check_records_count): {e}")
        return None


def fetch_all_records():
    try:
        connection = pymysql.connect(
            host=db_host, user=db_user, password=db_pass, database=db_name
        )
        with connection:
            with connection.cursor() as cursor:
                cursor.execute(f"SELECT * FROM {db_table}")
                records = cursor.fetchall()
                if records:
                    headers = [i[0] for i in cursor.description]
                    table_records = tabulate(records, headers, tablefmt="fancy_grid")
                    return table_records
                else:
                    return None
    except Exception as e:
        send_message(f"Error occured (fetch_all_records): {e}")
        return None


def db_monitoring():
    prev_count = check_records_count()

    while True:
        time.sleep(interval)
        current_count = check_records_count()

        if current_count is not None and current_count != prev_count:
            count = current_count - prev_count
            if count > 0:
                message = (
                    f"Количество записей в таблице {db_table} увеличилось на {count}.\n"
                    f"Текущее количество записей: {current_count}\n\n"
                )
            elif count < 0:
                message = (
                    f"Количество записей в таблице {db_table} уменьшилось на {abs(count)}.\n"
                    f"Текущее количество записей: {current_count}\n\n"
                )

            table_records = fetch_all_records()
            if table_records:
                message += f"{table_records}"
            else:
                message += f"Table {db_table} is empty"
            send_message(message)

        prev_count = current_count


if __name__ == "__main__":
    bot_thread = threading.Thread(
        target=bot.polling, args=((),), kwargs={"none_stop": True}
    )
    db_monitoring_thread = threading.Thread(target=db_monitoring)

    bot_thread.start()
    db_monitoring_thread.start()
```