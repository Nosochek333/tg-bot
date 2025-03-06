from aiogram import Bot, Dispatcher, F
from aiogram.filters import CommandStart
from aiogram.types import Message, InlineKeyboardMarkup, InlineKeyboardButton, CallbackQuery
import asyncio

# Вставьте сюда ваш токен
TOKEN = '7911992853:AAFdaWviiMzKPOzuJBgFbMlPOj_QVLGWJPs'

# Инициализация бота и диспетчера
bot = Bot(token=TOKEN)
dp = Dispatcher()

# Главная клавиатура с кнопками
def get_main_keyboard():
    keyboard = InlineKeyboardMarkup(inline_keyboard=[ 
        [InlineKeyboardButton(text="Ссылки", url="https://linktr.ee/Nosochek?utm_source=linktree_admin_share")],
        [InlineKeyboardButton(text="Донат", callback_data="support_nosochek")],
        [InlineKeyboardButton(text="Магазин", callback_data="shop_menu")],
        [InlineKeyboardButton(text="Настоящие носочки :)", callback_data="real_nosochki_menu")],
        [InlineKeyboardButton(text="Прочее", callback_data="other_menu")],
        [InlineKeyboardButton(text="Сотрудничество", callback_data="collaboration")]
    ])
    return keyboard

# Клавиатура для подменю "Донат"
def get_support_nosochek_keyboard():
    keyboard = InlineKeyboardMarkup(inline_keyboard=[ 
        [InlineKeyboardButton(text="Donationalerts", url="https://www.donationalerts.com/r/n0sochek")],
        [InlineKeyboardButton(text="Boosty", url="https://boosty.to/nosochek333")],
        [InlineKeyboardButton(text="По номеру карты", callback_data="card_number")],
        [InlineKeyboardButton(text="Назад", callback_data="back_to_main")]
    ])
    return keyboard

# Клавиатура для меню "Настоящие носочки :)"
def get_real_nosochki_keyboard():
    keyboard = InlineKeyboardMarkup(inline_keyboard=[ 
        [InlineKeyboardButton(text="Топ донатеров", callback_data="top_donators")],
        [InlineKeyboardButton(text="Помощники", callback_data="assistants")],
        [InlineKeyboardButton(text="Донатеры", callback_data="donators")],
        [InlineKeyboardButton(text="Первые покупатели", callback_data="first_buyers")],
        [InlineKeyboardButton(text="Назад", callback_data="back_to_main")]
    ])
    return keyboard

# Клавиатура для меню "Прочее"
def get_other_menu_keyboard():
    keyboard = InlineKeyboardMarkup(inline_keyboard=[ 
        [InlineKeyboardButton(text="Стать членом поддержки", callback_data="join_support")],
        [InlineKeyboardButton(text="Идеи", callback_data="ideas")],
        [InlineKeyboardButton(text="Сообщить о баге", callback_data="report_bug")],
        [InlineKeyboardButton(text="Поддержка", callback_data="support_request")],
        [InlineKeyboardButton(text="Назад", callback_data="back_to_main")]
    ])
    return keyboard

# Клавиатура для меню "Сотрудничество"
def get_collaboration_keyboard():
    keyboard = InlineKeyboardMarkup(inline_keyboard=[ 
        [InlineKeyboardButton(text="Участие в ролике", callback_data="participation")],
        [InlineKeyboardButton(text="Реклама", callback_data="advertisement")],
        [InlineKeyboardButton(text="Назад", callback_data="back_to_main")]
    ])
    return keyboard

# Клавиатура для меню "Магазин"
def get_shop_menu_keyboard():
    keyboard = InlineKeyboardMarkup(inline_keyboard=[ 
        [InlineKeyboardButton(text="Исходный код бота - 250 руб", callback_data="buy_bot_code")],
        [InlineKeyboardButton(text="Назад", callback_data="back_to_main")]
    ])
    return keyboard

# Обработчик команды /start
@dp.message(CommandStart)
async def on_start_command(message: Message):
    await message.answer(
        "Добро пожаловать в скромного бота от мега программиста Nosochek :)",
        reply_markup=get_main_keyboard()
    )

# Обработчик для кнопки "Донат"
@dp.callback_query(F.data == "support_nosochek")
async def on_support_nosochek(callback: CallbackQuery):
    await callback.message.edit_text(
        "Выберите удобный для вас способ поддержки:",
        reply_markup=get_support_nosochek_keyboard()
    )
    await callback.answer()
# Обработчик для кнопки "Топ донатеров"
@dp.callback_query(F.data == "top_donators")
async def on_top_donators(callback: CallbackQuery):
    await callback.message.answer(
        "Пока нету донатеров :("
    )
    await callback.answer()

# Обработчик для кнопки "Помощники"
@dp.callback_query(F.data == "assistants")
async def on_assistants(callback: CallbackQuery):
    await callback.message.answer(
        "Напиши нам свои идеи о развитии данного бота, и твой ник обязательно окажется здесь."
    )
    await callback.answer()

# Обработчик для кнопки "Донатеры"
@dp.callback_query(F.data == "donators")
async def on_donators(callback: CallbackQuery):
    await callback.message.answer(
        "Ты можешь помочь материально Nosochek, и твой ник окажется тут!\n"
        "Если его здесь не появилось, то обратись в поддержку."
    )
    await callback.answer()

# Обработчик для кнопки "Первые покупатели"
@dp.callback_query(F.data == "first_buyers")
async def on_first_buyers(callback: CallbackQuery):
    await callback.message.answer(
        "К сожалению, пока нету покупателей("
    )
    await callback.answer()

# Обработчик для кнопки "По номеру карты"
@dp.callback_query(F.data == "card_number")
async def on_card_number(callback: CallbackQuery):
    await callback.message.answer(
        "Номер карты: 2202 2069 4121 8831"
    )
    await callback.answer()

# Обработчик для кнопки "Сотрудничество"
@dp.callback_query(F.data == "collaboration")
async def on_collaboration(callback: CallbackQuery):
    await callback.message.edit_text(
        "Выберите интересующий вас вариант:",
        reply_markup=get_collaboration_keyboard()
    )
    await callback.answer()

# Обработчик для кнопки "Участие в ролике"
@dp.callback_query(F.data == "participation")
async def on_participation(callback: CallbackQuery):
    await callback.message.answer(
        "Вижу вы хотите поучаствовать в ролике. В таком случае напишите @n0sochek333 и обязательно скажите с какой целью вы пишете, иначе вас могу просто проигнорировать."
    )
    await callback.answer()

# Обработчик для кнопки "Реклама"
@dp.callback_query(F.data == "advertisement")
async def on_advertisement(callback: CallbackQuery):
    await callback.message.answer(
        "Вижу вы хотите стать рекламодателем. В таком случае напишите @n0sochek333 и обязательно скажите с какой целью вы пишете, иначе вас могу просто проигнорировать."
    )
    await callback.answer()

# Обработчик для кнопки "Магазин"
@dp.callback_query(F.data == "shop_menu")
async def on_shop_menu(callback: CallbackQuery):
    await callback.message.edit_text(
        "Выберите товар:",
        reply_markup=get_shop_menu_keyboard()
    )
    await callback.answer()

# Обработчик для покупки исходного кода бота
@dp.callback_query(F.data == "buy_bot_code")
async def on_buy_bot_code(callback: CallbackQuery):
    await callback.message.answer(
        "Ого, видимо вас заинтересовал этот товар :)\n\n"
        "В таком случае перечислите деньги на карту 2202 2069 4121 8831 и отправьте чек @n0sochek333.\n\n"
        "⚠️ Учитывайте: если вы решите подделать чек, то вас просто забанят."
    )
    await callback.answer()

# Обработчик для кнопки "Настоящие носочки :)"
@dp.callback_query(F.data == "real_nosochki_menu")
async def on_real_nosochki_menu(callback: CallbackQuery):
    await callback.message.edit_text(
        "Вот самые настоящие носочки :)",
        reply_markup=get_real_nosochki_keyboard()
    )
    await callback.answer()

# Обработчик для кнопки "Прочее"
@dp.callback_query(F.data == "other_menu")
async def on_other_menu(callback: CallbackQuery):
    await callback.message.edit_text(
        "Выберите интересующий вас вариант:",
        reply_markup=get_other_menu_keyboard()
    )
    await callback.answer()
# Обработчик для кнопки "Стать членом поддержки"
@dp.callback_query(F.data == "join_support")
async def on_join_support(callback: CallbackQuery):
    await callback.message.answer(
        "Похоже что хоже вы реши стать членом нашей команды :)\n"
        "В таком случае напишите @n0sochek333 и объясните с какой целью вы ему пишете."
    )
    await callback.answer()

# Обработчик для кнопки "Идеи"
@dp.callback_query(F.data == "ideas")
async def on_ideas(callback: CallbackQuery):
    await callback.message.answer(
        "Похоже у вас появилась хорошая идея для улучшения бота. В таком случае напишите @n0sochek333 и объясните с какой целью ты ему пишешь и мы обязательно рассмотрим твою анкету."
    )
    await callback.answer()

# Обработчик для кнопки "Сообщить о баге"
@dp.callback_query(F.data == "report_bug")
async def on_report_bug(callback: CallbackQuery):
    await callback.message.answer(
        "Похоже вы нашли какую-то поломку в нашем боте :( В таком случае напишите @n0sochek333 и объясните с какой проблемой ты столкнулся."
    )
    await callback.answer()

# Обработчик для кнопки "Поддержка"
@dp.callback_query(F.data == "support_request")
async def on_support_request(callback: CallbackQuery):
    await callback.message.answer(
        "Похоже у вас что-то случилось и вы решили обратиться в нашу поддержку. В таком случае напишите @n0sochek333, но сначала укажите, что вам нужна помощь, а затем опишите проблему."
    )
    await callback.answer()

# Обработчик для кнопки "Назад"
@dp.callback_query(F.data == "back_to_main")
async def on_back_to_main(callback: CallbackQuery):
    await callback.message.edit_text(
        "Вы вернулись в главное меню.",
        reply_markup=get_main_keyboard()
    )
    await callback.answer()

# Запуск бота
if name == "main":
    # Запускаем диспетчер
    asyncio.run(dp.start_polling(bot))