from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters, ContextTypes
import requests
import json
import os

# Your bot token from BotFather
TOKEN = '7635474576:AAFc4wC9CUGX9_01RQ13rOwsQI243SZR580'

# File to store user preferences
PREFS_FILE = 'user_prefs.json'

# Function to load user preferences
def load_prefs():
    if os.path.exists(PREFS_FILE):
        with open(PREFS_FILE, 'r') as file:
            return json.load(file)
    return {}

# Function to save user preferences
def save_prefs(prefs):
    with open(PREFS_FILE, 'w') as file:
        json.dump(prefs, file)

# Start command handler
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    await update.message.reply_text("Hello! Send me any text, and I’ll echo it back to you.")

# Help command handler
async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    await update.message.reply_text("Commands:\n/start - Greet the user\n/help - Show help\n/weather - Get weather data\n/setresponse <response> - Set custom response")

# Echo message handler
async def echo(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    prefs = load_prefs()
    user_id = str(update.message.from_user.id)
    custom_response = prefs.get(user_id, {}).get('custom_response')
    user_text = update.message.text
    
    if custom_response:
        await update.message.reply_text(custom_response)
    else:
        await update.message.reply_text(f"You said: {user_text}")

# Weather command handler
async def weather(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    # You can allow users to input a city or set a default one
    city = 'Phnom Penh'  # Default city
    if context.args:
        city = ' '.join(context.args)  # If a city is provided by the user

    api_key = '7f59948b973042e8bfd22815241211'  # Your WeatherAPI key
    url = f"https://api.weatherapi.com/v1/current.json?key={api_key}&q={city}"
    
    response = requests.get(url)
    data = response.json()
    
    # Check if the request was successful
    if 'error' not in data:
        weather_data = f"Weather in {city}:\nTemperature: {data['current']['temp_c']}°C\nDescription: {data['current']['condition']['text']}"
    else:
        weather_data = "Sorry, I couldn't fetch the weather data."
    
    await update.message.reply_text(weather_data)


# Set custom response command handler
# Set custom response command handler
async def set_response(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    prefs = load_prefs()
    user_id = str(update.message.from_user.id)
    custom_response = ' '.join(context.args)
    
    if user_id not in prefs:
        prefs[user_id] = {}
    
    prefs[user_id]['custom_response'] = custom_response
    save_prefs(prefs)
    
    await update.message.reply_text(f"Custom response set to: {custom_response}")

# Echo message handler with custom response
 
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    await update.message.reply_text("Hello! I’m here to answer your questions. Ask me anything!")

# Message handler for responding to specific questions
# Handle specific messages with a custom response
async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    user_text = update.message.text.lower()  # Get the user's text in lowercase for easier matching

    # Define specific responses based on common questions
    if "how to reduce stress" in user_text:
        response = (
            "To reduce stress, try the following techniques:\n"
            "- Practice deep breathing exercises.\n"
            "- Engage in physical activities like walking or yoga.\n"
            "- Take short breaks and relax.\n"
            "- Make time for hobbies you enjoy.\n"
            "Let me know if you want more tips!"
        )
    elif "hello" in user_text:
        response = "Hello! How can I assist you today?"
    elif "price" in user_text:
        response = "Our product prices vary. Could you specify which product you're interested in?"
    elif "who are you" in user_text or "what are you" in user_text:
        response = "I’m a bot created to answer your questions and help you with useful information."
    elif "weather" in user_text:
        response = "I don't have weather updates, but you can check your local weather app or website."
    elif "thank you" in user_text:
        response = "You're welcome! Let me know if you need any further assistance."
    elif "how are you" in user_text:
        response = "I'm just a bot, but I'm doing great! How can I help you?"
    elif "tell me a joke" in user_text:
        response = "Why don’t skeletons fight each other? They don’t have the guts!"
    elif "how to improve sleep" in user_text:
        response = (
            "Here are some tips to improve your sleep:\n"
            "- Stick to a consistent sleep schedule.\n"
            "- Create a relaxing bedtime routine.\n"
            "- Limit screen time before bed.\n"
            "- Keep your bedroom cool and quiet.\n"
            "- Avoid caffeine late in the day.\n"
            "I hope these tips help!"
        )
    elif "motivation" in user_text:
        response = "Stay positive! Remember, progress is progress, no matter how small. Keep going!"
    elif "exercise" in user_text:
        response = (
            "Exercise is great for your health! Some ideas include:\n"
            "- Cardio (running, cycling, etc.)\n"
            "- Strength training (weights or bodyweight exercises)\n"
            "- Flexibility exercises (yoga or stretching)\n"
            "It's important to find something you enjoy!"
        )
    elif "how to stay motivated" in user_text:
        response = (
            "Staying motivated can be challenging, but here are some tips:\n"
            "- Set clear, achievable goals and break them into smaller tasks.\n"
            "- Celebrate your small wins along the way.\n"
            "- Stay positive and remind yourself of your ‘why’.\n"
            "- Surround yourself with positive influences and people.\n"
            "- Don't be afraid to take breaks when needed."
        )
    elif "how to build self-confidence" in user_text:
        response = (
            "Building self-confidence takes time, but you can start with:\n"
            "- Focus on your strengths and remind yourself of past successes.\n"
            "- Challenge negative thoughts and replace them with positive ones.\n"
            "- Set small, achievable goals and accomplish them.\n"
            "- Take care of your physical and mental health.\n"
            "- Practice self-compassion and be patient with yourself."
        )
    elif "how to get better at studying" in user_text:
        response = (
            "Improving your studying habits is key to success. Here are some tips:\n"
            "- Organize your study materials and create a study schedule.\n"
            "- Break study sessions into focused intervals with short breaks (Pomodoro Technique).\n"
            "- Review notes regularly to reinforce concepts.\n"
            "- Minimize distractions by studying in a quiet, organized space.\n"
            "- Stay positive and remember that consistency is key."
        )
    elif "how to focus better" in user_text:
        response = (
            "Improving focus can make studying or working much more efficient. Try these strategies:\n"
            "- Eliminate distractions (turn off notifications, stay away from social media).\n"
            "- Set specific, short-term goals for each study session.\n"
            "- Take regular breaks to avoid burnout.\n"
            "- Practice mindfulness or meditation to train your brain to focus.\n"
            "- Get enough sleep and eat well to keep your mind sharp."
        )
    elif "how to deal with failure" in user_text:
        response = (
            "Failure is a part of growth. Here’s how you can handle it:\n"
            "- Accept failure as a learning opportunity, not a setback.\n"
            "- Analyze what went wrong and what you can improve next time.\n"
            "- Don’t be afraid to ask for feedback or help.\n"
            "- Take a break and come back stronger with a fresh perspective.\n"
            "- Keep a positive mindset and remember that persistence is key."
        )
    elif "how to stay productive" in user_text:
        response = (
            "Staying productive can be tough, but these tips might help:\n"
            "- Prioritize tasks based on importance and deadlines.\n"
            "- Set small, achievable goals for each day.\n"
            "- Eliminate distractions and focus on one task at a time.\n"
            "- Take regular breaks to avoid burnout.\n"
            "- Keep a positive mindset and reward yourself after completing tasks."
        )
    else:
        # Default response if no specific keywords match
        response = "I didn't quite get that. Could you please clarify?"

    # Send the response to the user
    await update.message.reply_text(response)

def main():
    # Set up the bot with the token
    application = ApplicationBuilder().token(TOKEN).build()

    # Add handlers for commands and messages
    application.add_handler(CommandHandler("start", start))
    application.add_handler(CommandHandler("help", help_command))
    application.add_handler(CommandHandler("weather", weather))
    application.add_handler(CommandHandler("setresponse", set_response))
    application.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

    # Start the bot
    application.run_polling()

if __name__ == '__main__':
    main()