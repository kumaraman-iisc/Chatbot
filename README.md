# Chatbot
A chabot having response, analytics and feedback mechanism

# **LLM Chatbot with Phoenix Observability**  

## **Project Overview**  
This project implements a **multi-turn chatbot with memory** using a Large Language Model (**LLM**) in **Google Colab**, integrated with **Arize Phoenix** for observability and performance monitoring.  

The chatbot allows users to:  
- Engage in natural conversations with AI  
- Provide feedback on responses  
- Analyze chatbot performance through analytics  

The **Gradio-based UI** provides an **interactive and user-friendly experience**.  

---

## **Features**  

 **Conversational AI**  Handles **multi-turn** dialogue with **memory**.  
 **Phoenix Tracing & Observability**  Logs **LLM interactions** and tracks **latency & performance**.  
 **User Feedback System**  Allows **rating (1-5)** and **text-based feedback** on responses.  
 **LLM-as-a-Judge Evaluation**  Automated evaluation of chatbot responses.  
 **Analytics Dashboard**  Provides chatbot **performance insights** and **rating distribution**.  
 **Interactive UI**  Built using **Gradio** for an intuitive user experience.  

---

##  **Setup & Installation**  

### ** Install Dependencies**  
Run the following command in **Google Colab** to install required libraries:  

```python
!pip install transformers gradio phoenix torch pandas matplotlib
```

---

### ** Load Pre-trained LLM Model**  
This chatbot uses **Hugging Face Transformers**. Load the model with:  

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
import torch

model_name = "facebook/opt-1.3b"  # Change to a different model if needed
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name).to("cuda")
```

---

### ** Run the Chatbot UI**  
The chatbot UI is built with **Gradio**. Run the following command to launch it:  

```python
import gradio as gr

with gr.Blocks() as chatbot_ui:
    gr.Markdown("# AI Chatbot with Phoenix Integration")

    with gr.Tab("Chatbot"):
        chat_history_ui = gr.Chatbot(type="messages")
        user_input = gr.Textbox(label="Type your message here...")
        send_button = gr.Button("Send")

    with gr.Tab("Feedback"):
        gr.Markdown("### Rate Chatbot Responses")
        index_slider = gr.Slider(0, 10, step=1, label="Select Response")
        rating_slider = gr.Slider(1, 5, step=1, label="Rate (1 = Poor, 5 = Excellent)")
        feedback_textbox = gr.Textbox(label="Feedback", placeholder="Write your feedback here...")
        save_button = gr.Button(" Save Feedback")
        feedback_status = gr.Text()

    with gr.Tab("Analytics"):
        gr.Markdown("### Feedback Analytics")
        analytics_display = gr.Textbox("Loading analytics...", interactive=False)
        rating_chart = gr.Image(value="rating_chart.png")

    send_button.click(fn=chatbot_response, inputs=[user_input, chat_history_ui], outputs=chat_history_ui)
    save_button.click(fn=save_feedback, inputs=[index_slider, rating_slider, feedback_textbox], outputs=feedback_status)

chatbot_ui.launch()
```

---

## **How to Run**
1. **Clone this repository** (if applicable):  
   ```bash
   git clone https://github.com/your-repo/chatbot-phoenix.git
   cd chatbot-phoenix
   ```
2. **Install dependencies**  
   ```python
   !pip install transformers gradio phoenix torch pandas matplotlib
   ```
3. **Run the chatbot in Google Colab or Jupyter Notebook.**  
4. **Provide feedback and analyze performance using Phoenix.**  

---

## **Future Improvements**
-  **Integrate more LLM models** (e.g., GPT-4, Llama)  
-  **Improve response generation** (fine-tuning & prompt engineering)  
-  **Enhance UI/UX** with better feedback collection  
-  **Better and more use of LLM as a Judge**
-  **RAG implementation**
-  **Reduced time for response**
---

## **Contributors**
**Kumar Aman**   

---  

