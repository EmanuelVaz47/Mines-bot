import telebot
import time
import threading
import random

# Configurações do bot
TOKEN = "7966837339:AAHVEIi-MSf8v6_yrLPpxngMeNJQaHh0kz4"
GRUPO_ID = "-6862221570"  # ID do grupo (negativo para grupos)

bot = telebot.TeleBot(TOKEN)

# Lista de emojis para os sinais
EMOJIS = ["🎰", "💣", "🔥", "💎", "🎲", "✨", "🤑"]

def gerar_sinal():
    """Gera sinais automaticamente a cada 2 minutos."""
    while True:
        # Escolhendo 3 posições para as minas
        casas = list(range(1, 25))
        minas = random.sample(casas, 3)

        # Criando a mensagem do sinal
        emoji = random.choice(EMOJIS)
        mensagem = (
            f"🎰 **NOVO SINAL DO MINES!** 🎰\n\n"
            f"💣 **Minas:** 3\n"
            f"🔄 **Tentativas:** 2\n"
            f"🕒 **Próximo sinal em 2 minutos**\n\n"
            f"⚡ **Jogue agora e boa sorte!** {emoji}{emoji}{emoji}"
        )

        # Enviando para o grupo
        bot.send_message(GRUPO_ID, mensagem, parse_mode="Markdown")

        # Espera 2 minutos antes de gerar o próximo sinal
        time.sleep(120)

# Inicia o bot e os sinais automáticos
threading.Thread(target=gerar_sinal).start()
bot.polling()
pyTelegramBotAPI
