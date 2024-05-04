# ChatBot
'''
# Docs Created by : Dhiraj Kumar
# Email : dhiraj.aiexpert@gmail.com
# Linkedin : https://www.linkedin.com/in/dhirajaiexpert/
# Kaggle : @dhirajaiexpert
'''

### 1. Create a simple chatbot using Python with OpenAI's Python package.

1. **Install the OpenAI Python Package:**
   ```bash
   pip install openai
   ```

2. **Obtain an OpenAI API Key:**
   Sign up for an account on the OpenAI platform and obtain an API key.

3. **Create a Python Script for the Chatbot:**
   Here's a example using the OpenAI Python package:

   ```python
   import openai

   # Set your API key
   api_key = 'your_api_key_here'
   openai.api_key = api_key

   def ask_question(question):
       response = openai.ChatCompletion.create(
           model="gpt-3.5-turbo",
           messages=[
               {"role": "system", "content": "You are a helpful assistant."},
               {"role": "user", "content": question},
           ]
       )
       return response["choices"][0]["message"]["content"]

   # Example usage
   question = "What is the capital of France?"
   answer = ask_question(question)
   print(answer)
   ```

   Replace `'your_api_key_here'` with your actual OpenAI API key.
