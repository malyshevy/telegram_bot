# telegram_bot
Телеграм бот поднимающий настроение
https://t.me/my_1_test_1_bot
@my_1_test_1_bot

'''
import telebot
import requests
from datetime import datetime

# Подключение к боту в ТГ
tg_api='6909377387:AAE-z7XCzU1d-yLv2JGx8Hmzzqs8SiZh538'
bot=telebot.TeleBot(tg_api)

# URL доступа к боту wiki
api_url='https://7012.deeppavlov.ai/model'

# Вывод сообщения и времени / описание синтаксиса запроса
@bot.message_handler(commands=['start'])
def start(message):
    time=datetime.now()
    te=int(time.strftime('%H'))
    tim=time.strftime("%H:%M:%S")
    if te<=6:
        bot.send_message(message.chat.id, 'Спи уже а не с ботами разговаривай в ')
        bot.send_message(message.chat.id, tim)
    elif (te>6)&(te<=8):
        bot.send_message(message.chat.id, 'Пей быстрей свой кофе и на работу !!! Уже : ')
        bot.send_message(message.chat.id, tim)
    elif te==18:
        bot.send_message(message.chat.id, 'Ускорься !!! Тебе уже домой пора ')
        bot.send_message(message.chat.id, tim)
    else:
        bot.send_message(message.chat.id, 'Вот теперь пообщаемся ')
        bot.send_message(message.chat.id, tim)
    bot.send_message(message.chat.id, 'Напиши запрос в виде: </wiki твой запрос>')

# Обращение к wiki
@bot.message_handler(commands=['wiki'])
def wiki(message):
    quest = message.text.split()[1:]
    qq=" ".join(quest)
    data = { 'question_raw': [qq]}
    try:
        res = requests.post(api_url, json=data, verify=False).json()
        bot.send_message(message.chat.id, res)
    except:
        bot.send_message(message.chat.id, "Я ничего не нашел")

bot.polling()
'''
