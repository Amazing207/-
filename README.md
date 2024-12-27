import telebot
from telebot.types import InlineKeyboardMarkup, InlineKeyboardButton, WebAppInfo

# Токен бота
ARI_TOKEN = '6957931158:AAEWOTMJzKxvKoMEudWlO24cWtUF3_qlw1Q'

# Ініціалізація бота
bot = telebot.TeleBot(ARI_TOKEN)

# Шлях до фото (веб-посилання)
photo_url = "https://i.pinimg.com/736x/34/1d/72/341d72a981067f5599a7dc83bc2004fb.jpg"

# Створення кнопки WebApp
def create_webapp_button():
    markup = InlineKeyboardMarkup()
    game_button = InlineKeyboardButton(
        "Play",
        web_app=WebAppInfo(url="https://bald-psychedelic-ornament.glitch.me")  # Вкажіть своє посилання на гру
    )
    markup.add(game_button)
    return markup


# Команда /start
@bot.message_handler(commands=['start'])
def on_start(message):
    # Надсилаємо текстове повідомлення з WebApp кнопкою
    bot.send_photo(
        message.chat.id,
        photo_url,
        caption="Welcome to Jumping Block! Press the button 'Play', to start the game:",
        reply_markup=create_webapp_button()
    )


# Запуск бота
if __name__ == '__main__':
    bot.infinity_polling()
