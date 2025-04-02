# Language Learning Chatbot

## Overview
This chatbot assists users in learning a new language by engaging in interactive conversations. It corrects users' mistakes in real-time, maintains a record of errors, and provides a review feature to help users track their progress.

## Features
- Supports interactive language learning through conversations.
- Identifies and corrects grammatical and spelling mistakes.
- Stores mistakes in a MySQL database.
- Maintains session memory using LangChain to enhance user interaction.
- Allows users to review their past mistakes during the conversation.

## Setup

### Database Configuration
The chatbot connects to a MySQL database to store users' mistakes. The database setup includes:

A `mistakes` table to log user errors and their corrections:

```sql
CREATE TABLE IF NOT EXISTS mistakes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id VARCHAR(255),
    mistake TEXT,
    correction TEXT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### OpenAI API Configuration
The chatbot utilizes OpenAI's GPT-3.5 model to generate responses. The API key must be set correctly before running the chatbot:

```python
OPENAI_API_KEY = "Enter Your Token Key"
openai.api_key = OPENAI_API_KEY
```

## Key Functions

### `get_session_memory(session_id)`
- Uses LangChain's `ConversationBufferMemory` to retain past messages for a more context-aware conversation.
- Creates a new session memory if the user is new.

### `invoke_chatbot(user_input, session_id)`
- Sends the user’s input to OpenAI’s GPT-3.5 model.
- The model responds as a language tutor, engaging in a natural conversation while correcting mistakes.
- Saves the interaction context to session memory.

### `find_differences(original, corrected)`
- Compares the original user input with the corrected response from the AI.
- Identifies incorrect words and their corrected forms.

### `save_mistake(user_id, mistake, correction)`
- Logs mistakes and their corrections in the MySQL database.

### `get_mistakes_summary(user_id)`
- Retrieves the list of mistakes made by the user along with corrections for review.

### `chatbot()`
- Initiates a language learning session.
- Prompts the user to enter their known and target languages.
- Engages in a conversation, correcting mistakes while storing them.
- Supports commands:
  - `exit`: Ends the chat session.
  - `review`: Displays the user's mistakes and corrections.

## Usage
1. Run the script.
2. Enter user details (user ID, known language, target language, proficiency level).
3. Start chatting in the target language.
4. View corrections in real-time.
5. Type `review` anytime to see past mistakes.
6. Type `exit` to end the session.

## Conclusion
This chatbot effectively simulates a human-like tutor, making language learning interactive and engaging. By tracking user mistakes, it offers personalized feedback, helping learners improve over time.
