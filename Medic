import os
import streamlit as st
import google.generativeai as genai

# Load API key from environment variables (if using .env)
GOOGLE_API_KEY=os.env("googleapikey")
# Configure Gemini API
import time
import os
import joblib
import streamlit as st
import google.generativeai as genai
from dotenv import load_dotenv

# load_dotenv()
# GOOGLE_API_KEY = "AIzaSyCD8VvyqQlUQLkwFQerUPob7U_iswqEEus"
genai.configure(api_key=GOOGLE_API_KEY)

new_chat_id = f'{time.time()}'
MODEL_ROLE = 'AI'
AI_AVATAR_ICON = '🩺'

# Create a data/ folder if it doesn't already exist
try:
    os.mkdir('data/')
except FileExistsError:
    pass

# Load past chats (if available)
try:
    past_chats = joblib.load('data/past_chats_list')
except FileNotFoundError:
    past_chats = {}

# Sidebar allows a list of past chats
with st.sidebar:
    st.write('# Past Chats')
    if 'chat_id' not in st.session_state:
        st.session_state.chat_id = new_chat_id
    else:
        st.session_state.chat_id = st.selectbox(
            label='Pick a past chat',
            options=[new_chat_id] + list(past_chats.keys()),
            format_func=lambda x: past_chats.get(x, 'New Chat'),
            placeholder='_',
        )
    st.session_state.chat_title = f'ChatSession-{st.session_state.chat_id}'

st.title('Medical Chatbot')
st.write('## Chat with Medical AI')

# Chat history (allows to ask multiple questions)
try:
    st.session_state.messages = joblib.load(
        f'data/{st.session_state.chat_id}-st_messages'
    )
    st.session_state.gemini_history = joblib.load(
        f'data/{st.session_state.chat_id}-gemini_messages'
    )
except FileNotFoundError:
    st.session_state.messages = []
    st.session_state.gemini_history = []

st.session_state.model = genai.GenerativeModel('gemini-pro')
st.session_state.chat = st.session_state.model.start_chat(
    history=st.session_state.gemini_history,
)

# Display chat messages from history on app rerun
for message in st.session_state.messages:
    with st.container():
        if message['role'] == 'user':
            st.write('You:', message['content'])
        elif message['role'] == MODEL_ROLE:
            st.write('AI:', message['content'])

# React to user input
if prompt := st.text_input('Your message here...'):
    if st.button('Send'):
        if st.session_state.chat_id not in past_chats.keys():
            past_chats[st.session_state.chat_id] = st.session_state.chat_title
            joblib.dump(past_chats, 'data/past_chats_list')
        with st.container():
            st.write('You:', prompt)
        st.session_state.messages.append(
            dict(
                role='user',
                content=prompt,
            )
        )
        response = st.session_state.chat.send_message(
            prompt,
            stream=True,
        )
        with st.container():
            st.write('AI is typing...')
            message_placeholder = st.empty()
            full_response = ''
            assistant_response = response
            for chunk in response:
                for ch in chunk.text.split(' '):
                    full_response += ch + ' '
                    time.sleep(0.05)
                    message_placeholder.write(full_response + '▌')
            message_placeholder.write(full_response)

        st.session_state.messages.append(
            dict(
                role=MODEL_ROLE,
                content=st.session_state.chat.history[-1].parts[0].text,
            )
        )
        st.session_state.gemini_history = st.session_state.chat.history
        joblib.dump(
            st.session_state.messages,
            f'data/{st.session_state.chat_id}-st_messages',
        )
        joblib.dump(
            st.session_state.gemini_history,
            f'data/{st.session_state.chat_id}-gemini_messages',
        )
