# Telegram Бот для Составления Расписания

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Этот Telegram бот предназначен для составления и управления расписанием. Он позволяет создавать расписание для учебных корпусов.

## Особенности

*   **Удобный интерфейс:** Простой и интуитивно понятный интерфейс на основе Telegram-кнопок.
*   **Коректность:** В систему заранее загружены стандарты САНПиН.
*   **Сохранение данных:** Данные о расписании хранятся в  базе данных SQLite.
*   **Простота настройки:** Легко установить и настроить бота под свои нужды.

## Предварительные требования

*   **Python 3.7+**
*   **Установленный Telegram:** У вас должен быть установлен Telegram и аккаунт.
*   **Полученный токен Telegram бота:**  Вы должны создать бота в Telegram через BotFather и получить его токен.

## Установка

1.  **Клонирование репозитория:**

    ```bash
    git clone [ссылка на ваш репозиторий]
    cd [имя папки репозитория]
    ```

2.  **Создание и активация виртуального окружения (рекомендуется):**

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # Linux/macOS
    venv\Scripts\activate.bat # Windows
    ```

3.  **Установка зависимостей:**

    ```bash
    pip install -r requirements.txt
    ```

    Файл `requirements.txt` должен содержать следующие зависимости (пример):

    ```
    python-telegram-bot==20.7
    python-dotenv==1.0.0
    # Добавьте здесь другие необходимые библиотеки
    # Например:
    # sqlalchemy==2.0.23
    # ...
    ```

4.  **Настройка конфигурации:**

    *   **Создайте файл `.env` в корневой директории проекта.**

        Содержимое файла `.env` должно быть примерно таким:

        ```
        TELEGRAM_BOT_TOKEN=YOUR_TELEGRAM_BOT_TOKEN
        DATABASE_URL=sqlite:///schedule.db  # Пример для SQLite
        # Другие переменные окружения, если необходимы
        ```

    *   **Замените `YOUR_TELEGRAM_BOT_TOKEN` на токен вашего Telegram бота.**  Как получить токен:

        1.  Откройте Telegram и найдите пользователя `@BotFather`.
        2.  Начните с ним чат, отправив команду `/start`.
        3.  Отправьте команду `/newbot` и следуйте инструкциям BotFather, чтобы создать нового бота.
        4.  BotFather предоставит вам токен вашего бота.  **Сохраните его в безопасном месте!**

    *   **Настройте `DATABASE_URL` в соответствии с используемой базой данных.** 

        *   `sqlite:///schedule.db`:  Создаст файл `schedule.db` в корне проекта для хранения данных SQLite.
        *   `postgresql://user:password@host:port/database`: Пример подключения к PostgreSQL.
        *   и т.д.

        **Важно:** Если вы используете другую базу данных, убедитесь, что у вас установлены необходимые драйверы (`psycopg2` для PostgreSQL, `pymysql` для MySQL и т.д.).  Добавьте их в `requirements.txt`.

5.  **Запуск бота:**

    ```bash
    python bot.py  
    ```

    Убедитесь, что в вашем основном файле `bot.py` (или как он у вас называется) происходит чтение токена из файла `.env`:

    ```python
    import os
    from dotenv import load_dotenv
    from telegram import Update
    from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes

    load_dotenv()
    TELEGRAM_BOT_TOKEN = os.getenv("TELEGRAM_BOT_TOKEN")

    async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
        await context.bot.send_message(chat_id=update.effective_chat.id, text="Привет! Я бот для расписания.")

    if __name__ == '__main__':
        application = ApplicationBuilder().token(TELEGRAM_BOT_TOKEN).build()

        start_handler = CommandHandler('start', start)
        application.add_handler(start_handler)

        application.run_polling()
    ```

## Использование

После запуска бота, найдите его в Telegram по имени пользователя, которое вы указали при создании бота через BotFather.  Начните с ним чат и используйте доступные команды.

*   `/start`:  Запускает бота и отображает приветственное сообщение.
*   `/setup`:  Начинает процесс получения данных.
*   `/schedule`: публикует расписание.
*   `/test`: создаёт тестовое расписание.
*   `/help`:  Отображает список доступных команд. 


## Поддержка

Если у вас возникли вопросы или проблемы, пожалуйста, свяжитесь с нами в телеграмме @Pluss_pr.

## Благодарности

*   ГАОУ Школе 1518.
*   Корнееву Георгию Алексеевичу (Учитель физики в школе 1518).

