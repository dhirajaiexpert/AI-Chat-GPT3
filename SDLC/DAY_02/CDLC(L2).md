'''
# Docs Created by : Dhiraj Kumar
# Email : dhiraj.aiexpert@gmail.com
# Linkedin : https://www.linkedin.com/in/dhirajaiexpert/
# Kaggle : @dhirajaiexpert
'''

## Create a simple chatbot using Python with OpenAI's Python package and Flask, you can follow these steps:

### Step 1: Install the OpenAI Python Package

First, install the OpenAI Python package using pip:

```bash
pip install openai
```

### Step 2: Obtain an OpenAI API Key

Sign up for an account on the OpenAI platform and obtain an API key.

### Step 3: Create a Python Script for the Chatbot

Here's an example Python script for the chatbot:

```python
# chatbot.py
from flask import Flask, request, jsonify
import openai

app = Flask(__name__)

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

@app.route('/ask', methods=['POST'])
def ask():
    question = request.json['question']
    answer = ask_question(question)
    return jsonify({'answer': answer})

if __name__ == '__main__':
    app.run(debug=True)
```

Replace `'your_api_key_here'` with your actual OpenAI API key.

### Step 4: Create a Web Interface Using Flask

To create a web interface for your chatbot, you can use Flask:

```python
# app.py
from flask import Flask, render_template, request, jsonify
import requests

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/ask', methods=['POST'])
def ask():
    question = request.form['question']
    response = requests.post('http://localhost:5000/ask', json={'question': question})
    answer = response.json()['answer']
    return render_template('index.html', question=question, answer=answer)

if __name__ == '__main__':
    app.run(debug=True)
```

### Step 5: Create HTML Templates

Create an `index.html` file in a `templates` folder in your project directory:

```html
<!-- templates/index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Chatbot</title>
</head>
<body>
    <h1>Chatbot</h1>
    <form action="/ask" method="post">
        <label for="question">Ask a question:</label><br>
        <input type="text" id="question" name="question" value="{{ question }}"><br><br>
        <input type="submit" value="Submit">
    </form>
    {% if answer %}
    <h2>Answer:</h2>
    <p>{{ answer }}</p>
    {% endif %}
</body>
</html>
```

### Step 6: Run Your Flask Application

Run your Flask application:

```bash
python app.py
```

You can now access your chatbot's web interface by visiting `http://localhost:5000` in your web browser. Enter a question and submit it to see the chatbot's response.

### Step 7: Deploy Your Chatbot (Optional)

If you want to deploy your chatbot to a server, you can use platforms like Heroku, AWS, or Google Cloud Platform. Remember to set your API key as an environment variable instead of hardcoding it in your code for security reasons.
