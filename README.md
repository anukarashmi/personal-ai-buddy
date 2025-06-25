A simple LLM-powered personal chatbot built with Python, Streamlit, and OpenAI’s GPT model. Users can choose a custom persona and have natural conversations through a clean web interface. Designed for beginners to explore AI chat capabilities locally or online.
Features -Choose from multiple assistant personas
         -Chat with GPT-3.5 through a Streamlit UI
         -Clean and responsive web interface
         -Easy to run locally
  Built With Python, Streamlit, OpenAI API, dotenv      
  git clone https://github.com/anukarashmi/personal-ai-buddy.git 
  cd personal-ai-buddy 
  pip install -r requirements.txt
  "OPENAI_API_KEY=your-api-key-here" > .env && streamlit run app.py
code: 
import streamlit as st
from openai import OpenAI
import os
from dotenv import load_dotenv

load_dotenv()
api_key = os.getenv("OPENAI_API_KEY")

client = OpenAI(api_key=api_key)

st.set_page_config(page_title="AI Buddy", layout="centered")
st.title("💬 Your AI Buddy")

persona = st.selectbox("Choose your assistant", ["Friendly", "Professional", "Funny"])
user_input = st.text_input("Ask me anything:")

if user_input:
messages = [
{"role": "system", "content": f"You are a {persona.lower()} assistant."},
{"role": "user", "content": user_input}
]
with st.spinner("Thinking..."):
    response = client.chat.completions.create(
        model="gpt-3.5-turbo",
        messages=messages
    )

st.markdown("**Response:**")
st.write(response.choices[0].message.content)
