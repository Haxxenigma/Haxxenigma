# [BotFather](https://t.me/BotFather "https://t.me/BotFather")

```
/start
/newbot
...
/token
```

## [pyTelegramBotAPI](https://pypi.org/project/pyTelegramBotAPI/ "https://pypi.org/project/pyTelegramBotAPI/")

```shell
pip install pyTelegramBotAPI
```

```python
import telebot
from telebot import types

bot = telebot.TeleBot(TOKEN)


@bot.message_handler(commands=["start", "hello"])
def startMessageHandler(message):
    markup = types.InlineKeyboardMarkup()
    btn1 = types.InlineKeyboardButton("About me", callback_data="aboutme")
    btn2 = types.InlineKeyboardButton("What I can do?", callback_data="features")
    btn3 = types.InlineKeyboardButton("Visit Website", url="https://pypi.org/project/pyTelegramBotAPI/")
    markup.row(btn1)
    markup.row(btn2, btn3)
    bot.send_message(
        message.chat.id, f"Hello, {message.from_user.first_name}!", reply_markup=markup
    )


@bot.callback_query_handler(func=lambda call: call.data == "aboutme")
def aboutMeCallback(call):
    bot.send_message(call.message.chat.id, "Here is some information about me...")


@bot.callback_query_handler(func=lambda call: call.data == "features")
def featuresCallback(call):
    message = (
        "*List of my Features:\n*"
        "\- _Feature 1_\n"
        "\- _Feature 2_\n"
        "\- _Feature 3_\n"
    )
    bot.send_message(call.message.chat.id, message, parse_mode="MarkdownV2")


@bot.message_handler(content_types=["photo", "video", "audio"])
def unsupportedMessageHandler(message):
    bot.reply_to(message, "Sorry, but now I don't support this type of messages")


@bot.message_handler(content_types=["text"])
def unrecognizedMessageHandler(message):
    bot.reply_to(message, "Sorry, but now I can't understand this message")


bot.infinity_polling()
```

## [aiogram](https://aiogram.dev/ "https://aiogram.dev/")

```shell
pip install aiogram
```

```python
import asyncio
from aiogram import Bot, Dispatcher, types, F
from aiogram.filters.command import Command
from aiogram.utils.keyboard import InlineKeyboardBuilder

bot = Bot(token=TOKEN)
dp = Dispatcher()


@dp.message(Command("start"))
async def startMessageHandler(message: types.Message):
    builder = InlineKeyboardBuilder()
    btn1 = types.InlineKeyboardButton(text="About me", callback_data="aboutme")
    btn2 = types.InlineKeyboardButton(text="What I can do?", callback_data="features")
    btn3 = types.InlineKeyboardButton(
        text="Learn aiogram", url="https://mastergroosha.github.io/aiogram-3-guide/"
    )
    builder.row(btn1)
    builder.row(btn2, btn3)
    await message.answer("Hello", reply_markup=builder.as_markup())


@dp.callback_query(F.data == "aboutme")
async def aboutMeCallback(callback: types.CallbackQuery):
    await callback.message.answer("Here is some information about me...")


@dp.callback_query(F.data == "features")
async def featuresCallback(callback: types.CallbackQuery):
    message = (
        "*List of my Features:\n*"
        "\- _Feature 1_\n"
        "\- _Feature 2_\n"
        "\- _Feature 3_\n"
    )
    await callback.message.answer(message, parse_mode="MarkdownV2")


@dp.message(F.animation | F.sticker)
async def animationHandler(message: types.Message):
    if message.content_type == types.ContentType.ANIMATION:
        await message.reply_animation(message.animation.file_id)
    elif message.content_type == types.ContentType.STICKER:
        await message.reply_sticker(message.sticker.file_id)


@dp.message(
    F.content_type.in_(
        {
            "video",
            "audio",
            "photo",
            "document",
            "voice",
            "location",
            "contact",
            "album",
            "poll",
        }
    )
)
async def unsupportedMessageHandler(message: types.Message):
    await message.reply("Sorry, but now I don't support this type of messages")


@dp.message(F.text)
async def unrecognizedMessageHandler(message: types.Message):
    await message.reply("Sorry, but now I can't understand this message")


async def main():
    await dp.start_polling(bot)


if __name__ == "__main__":
    asyncio.run(main())
```