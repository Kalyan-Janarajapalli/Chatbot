# Chatbot
import re

responses = {
    "hi": "Hello! How can I assist you today?",
    "hello": "Hi there! How can I help you?",
    "how are you": "I'm doing great, thank you! How can I help you?",
    "bye": "Goodbye! Have a great day!",
    "help": "I can assist you with answering questions like 'hi', 'what's your name', or 'tell me a joke'.",
    "what is your name": "I’m Ai, your friendly chatbot! How can I assist you today?",
    "who are you": "I am Ai, your personal chatbot assistant, here to help you with anything you need.",
    "what can you do": "I can chat with you, answer basic questions, provide suggestions, and even tell jokes!",
    "tell me a joke": "Why don't skeletons fight each other? Because they don't have the guts!",
    "thank you": "You're welcome! Let me know if you need anything else.",
    "how old are you": "I’m as old as the moment I was created! I live in the digital world.",
    "tell me a fact": "Did you know? Honey never spoils. Archaeologists have found pots of honey in ancient tombs that are over 3,000 years old!",
}

suggestions = {
    "default": [
        "You can ask me about my name.",
        "Want to hear a joke? Just ask 'Tell me a joke.'",
        "Need help? Type 'help' for guidance.",
    ],
    "helpful": [
        "Try asking, 'What's your name?'",
        "You can say, 'Tell me something interesting.'",
    ],
}

def suggest_responses(category="default"):
    """Suggest responses based on the situation."""
    return "Here are some things you can try: " + ", ".join(suggestions.get(category, []))

def normalize_input(user_input):
    """Normalize user input to handle shortcuts and variations."""
    # Remove any unwanted characters and convert to lowercase
    user_input = re.sub(r'[^\w\s]', '', user_input).lower()

    # Handle common shortcuts and variations
    shortcuts = {
        "hii": "hi",
        "hey": "hi",
        "howdy": "hi",
        "sup": "how are you",
        "yo": "hi",
        "tq": "thank you",
        "thx": "thank you",
        "thanks": "thank you",
        "brb": "bye",
    }

    return shortcuts.get(user_input, user_input)

def chatbot():
    print("Ai: Hi! I’m Ai, your personal chatbot assistant. Type 'bye' anytime to exit.")
    
    while True:
        user_input = input("You: ")

        # Normalize the user input to handle shortcuts
        normalized_input = normalize_input(user_input)

        if normalized_input == "bye":
            print("Ai: Goodbye! Have a wonderful day!")
            break
        elif normalized_input in responses:
            print(f"Ai: {responses[normalized_input]}")
        else:
            print("Ai: I'm sorry, I don't understand that.")
            print(suggest_responses())

if __name__ == "__main__":
    chatbot()
