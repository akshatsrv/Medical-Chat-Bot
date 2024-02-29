# 🩺 Medical Chatbot Interface with Streamlit

## Overview

Welcome to our **Medical Chatbot Interface**, powered by Streamlit! This project facilitates seamless conversations with an AI assistant tailored specifically for medical inquiries. The application stores chat history, enabling users to revisit and continue previous discussions.

![Medical Chatbot](docs/medical-chatbot.gif)

## 🚀 Getting Started

### Dependencies

This project relies on the following libraries:

- **streamlit**: for creating the user interface.
- **gemini**: for interacting with the chatbot.
- **Gemini API key**: Obtain it from [Google AI Studio](https://ai.google.dev/tutorials/setup?hl=en).

### Usage

To run the application, follow these steps:

1. **Create a virtual environment**:
    ```bash
    python3 -m venv my_env
    source my_env/bin/activate 
    ```

2. **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

3. **Launch the Streamlit server**:
    ```bash
    streamlit run app_chat.py
    ```

4. **Access the application**:
    Visit [http://localhost:8501](http://localhost:8501) in your browser.

5. **Start chatting with the medical assistant!**

## ℹ️ How it Works

Here's how the application functions:

1. **User Input**: Users can input medical queries in the chat interface.

2. **Processing**: The Gemini model, specialized in medical conversations, processes the chat messages.

3. **Response Generation**: Based on the chat history and user input, the chatbot generates informative responses.

4. **Knowledge Utilization**: Leveraging its medical knowledge, the chatbot provides helpful insights and recommendations.

5. **Chat History**: Chat messages and interactions with the chatbot are stored for later retrieval.

6. **Continued Interaction**: Users can initiate new chats or return to previous ones for continued engagement.

Explore our Medical Chatbot and experience the convenience of obtaining medical assistance through interactive conversations!
