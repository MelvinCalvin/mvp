import openai
import random
from typing import List

openai.api_key = "your_openai_api_key_here"

class Chatbot:
    def __init__(self):
        self.conversation_history: List[str] = []

    def send_message(self, message: str) -> str:
        self.conversation_history.append(f"User: {message}")
        response = self.ask_gpt3_5_turbo(self.conversation_history)
        self.conversation_history.append(f"Chatbot: {response}")
        return response

    
@staticmethod

    def ask_gpt3_5_turbo(conversation_history: List[str]) -> str:
        prompt = "The following is a conversation with an AI chatbot. The chatbot is helpful, friendly, and knowledgeable.\n\n"
        prompt += "\n".join(conversation_history) + "\n"

        response = openai.Completion.create(
            engine="text-davinci-002",
            prompt=prompt,
            max_tokens=150,
            n=1,
            stop=None,
            temperature=0.8,
            top_p=1,
            frequency_penalty=0,
            presence_penalty=0,
        )

        return response.choices[0].text.strip()

def generate_random_icon() -> str:
    icons = ["😀", "😃", "😄", "😁", "😆", "😅"]
    return random.choice(icons)

def main():
    chatbot =
