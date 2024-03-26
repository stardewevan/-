# -
智能客服利用大语言模型和生成式 AI,为企业提供全天候的智能客户服务,提高客户满意度,减轻人工客服的工作负担。
import openai
from flask import Flask, request, jsonify

# Initialize Flask app
app = Flask(__name__)

# Mock function to simulate GPT-3 response
def get_gpt3_response(message):
    # In a real scenario, this function would use OpenAI's API to get a response
    # For demonstration purposes, we return a predefined response
    responses = {
        "shipping": "Your order will be shipped within 2-3 business days.",
        "return policy": "You can return your product within 30 days of receipt.",
        "payment options": "We accept all major credit cards, PayPal, and Google Pay."
    }
    for keyword, response in responses.items():
        if keyword in message.lower():
            return response
    return "I'm sorry, I didn't understand your question. Can you provide more details?"

@app.route('/ask', methods=['POST'])
def ask():
    data = request.json
    question = data.get('question', '')
    
    # Here, you would call the actual OpenAI API with the question.
    # response = openai.ChatCompletion.create(model="gpt-3.5-turbo", messages=[{"role": "system", "content": "You are a helpful assistant."}, {"role": "user", "content": question}])
    # answer = response.choices[0].message['content']
    
    # Simulating GPT-3 response
    answer = get_gpt3_response(question)
    
    return jsonify({"response": answer})

if __name__ == '__main__':
    app.run(debug=True, port=5000)
