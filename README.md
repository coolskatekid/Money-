import os
from anthropic import Anthropic

# Initialize the Anthropic client (requires ANTHROPIC_API_KEY set in your environment)
client = Anthropic()

SYSTEM_PROMPT = """
You are an expert AI marketing assistant for a modern software company. 
Your goal is to greet visitors, explain our product benefits, answer questions, 
and politely ask for their email address to send them a free guide.
Keep responses concise, friendly, and persuasive.
"""

def run_marketing_bot():
    print("Marketing Bot is active! Type 'quit' to exit.\n")
    messages = []

    while True:
        user_input = input("User: ")
        if user_input.lower() == 'quit':
            break

        messages.append({"role": "user", "content": user_input})

        response = client.messages.create(
            model="claude-3-5-haiku-latest",
            max_tokens=300,
            system=SYSTEM_PROMPT,
            messages=messages
        )

        bot_reply = response.content[0].text
        print(f"Bot: {bot_reply}\n")
        messages.append({"role": "assistant", "content": bot_reply})

if __name__ == "__main__":
    run_marketing_bot()

