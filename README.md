# LM Studio — Run an LLM Locally

Welcome! This beginner-friendly guide will walk you through setting up **LM Studio**, downloading an open-source Large Language Model (LLM), and running it entirely on your own computer. You will also learn how to turn that model into a local API server and call it using a simple Python script.

By the end of this guide, you will know how to:
1. **Install LM Studio** on your machine.
2. **Find a model** suited for your computer.
3. **Download the model** using the application.
4. **Load the model** into your computer's memory.
5. **Chat with it locally** without an internet connection.
6. **Start the LM Studio local API server** to expose your model.
7. **Call the model** programmatically from a Python application.

---

### How It Works (Architecture Diagram)

Here is a simple look at how the data flows on your machine once everything is set up. Everything stays safely on your hardware!

```text
+---------------------------------------------------------------------------------+
|                                  YOUR COMPUTER                                  |
|                                                                                 |
|  +---------------+     +---------------+     +-------------------------------+  |
|  |  Python App   | --> | localhost:1234| --> |    LM Studio Local Server     |  |
|  | (Your Script) |     |  (Local Port) |     | (Translates API Requests)     |  |
|  +---------------+     +---------------+     +-------------------------------+  |
|                                                              |                  |
|                                                              v                  |
|                                                      +---------------+          |
|                                                      |   Local LLM   |          |
|                                                      | (The AI Model)|          |
|                                                      +---------------+          |
+---------------------------------------------------------------------------------+
```

---

## 1. Install LM Studio

**LM Studio** is a desktop application that lets you run open-source AI models locally on your computer. It handles the complex math and hardware configuration behind the scenes, giving you a clean visual interface to chat with your AI.

1. Go to the official [LM Studio Website](https://lmstudio.ai/).
2. Download the installer compatible with your operating system (Mac, Windows, or Linux).
3. Open the installer and follow the standard on-screen setup prompts.

---

## 2. Find a Model

Once LM Studio is open, you can search for thousands of open-source models available on the internet. Some popular beginner-friendly model families include:

*   **Qwen:** Highly efficient models created by Alibaba, excellent for multiple languages and general coding.
*   **Llama:** Meta's flagship open-source models, widely used across the AI community.
*   **Gemma:** Light, fast, and capable models developed by Google.
*   **Mistral:** High-performing models designed by a leading AI team in France.

> **Beginner Tip:** Start small! AI models require a lot of computer memory (RAM or VRAM). If you are testing things out on a standard laptop, look for models labeled around **1.5B, 3B, or 7B** (the "B" stands for billions of parameters, which tells you how large the AI's "brain" is). Smaller numbers run much faster on regular hardware.

<img width="1026" height="616" alt="image" src="https://github.com/user-attachments/assets/d4710c3a-8c27-499d-93c1-4c6374a96725" />


---

## 3. Download the Model

When you click on a model, you will notice different versions available for download, often starting with the letter **Q** (like `Q4`, `Q5`, or `Q8`). 

These letters refer to **Quantization**. Think of quantization as compressing a large video file so it takes up less space. A quantized model shrinks the AI's file size so it fits inside a normal computer's memory, while keeping almost all of its original intelligence.

Choose a `Q4` or `Q5` version of your selected model and click **Download**.

<img width="639" height="583" alt="image" src="https://github.com/user-attachments/assets/66feec86-83db-413c-96d9-14fd71cbe866" />

---

## 4. Load the Model

Downloading a model saves it to your hard drive, but to actually use it, you must **load it** into your computer's temporary memory (RAM/VRAM).

1. Click on the **Chat** icon (the speech bubble) on the left sidebar.
2. At the very top of the window, click the dropdown menu that says **"Select a model to load"**.
3. Choose the model you just downloaded.
4. Wait a few moments for the progress bar to finish. Once loaded, the model is active and ready to think!

<img width="1338" height="825" alt="Screenshot 2026-09-29 at 9 17 42 PM" src="https://github.com/user-attachments/assets/20c010e2-319f-4ba6-b1ac-007f4e3fa5d8" />

<img width="1338" height="825" alt="Screenshot 2026-09-29 at 9 18 03 PM" src="https://github.com/user-attachments/assets/668456f2-5fb3-4835-8dfb-2163c46d9729" />


---

## 5. Chat with it Locally

With the model loaded, you can type a message in the bottom chat bar just like you would with any online AI assistant. 

Because the model lives on your hardware, you can disconnect your computer from the internet entirely, and the AI will still reply. Your conversations never leave your device, ensuring complete privacy.

<img width="1338" height="825" alt="Screenshot 2026-09-29 at 9 18 48 PM" src="https://github.com/user-attachments/assets/af56fef0-699b-4fb4-b5f9-d0d58ca85746" />


---

## 6. Start the LM Studio Local API Server

One of the coolest features of LM Studio is its ability to mimic developer platforms like OpenAI. It lets you turn your computer into a local server so other programs on your machine can talk to your AI model.

1. Click the **Local Server** icon (the multi-directional arrows or developer icon) on the left sidebar.
2. Choose the model you want to serve from the dropdown menu at the top.
3. Turn on the green **Status** button.
4. By default, your server will host itself at `http://localhost:1234`. This acts as an internal pipeline on your computer that only your local scripts can access.

<img width="1338" height="825" alt="Screenshot 2026-09-29 at 9 19 26 PM" src="https://github.com/user-attachments/assets/92d470f0-d2f9-4981-8065-cfbba24e99f5" />


---

## 7. Call the Model from Python

Now that your server is running, you can interact with your local AI using code! Here is a simple Python example using the official `openai` library (since LM Studio mimics its structure perfectly).

### Prerequisites
First, install the OpenAI library in your terminal:
```bash
pip install openai
```

### Python Script
Create a file named `test_api.py` and paste the following code:

```python
from openai import OpenAI

# Point the client to your local LM Studio server
client = OpenAI(base_url="http://localhost:1234/v1", api_key="lm-studio")

completion = client.chat.completions.create(
    model="YOUR_MODEL_NAME", # LM Studio automatically defaults to your loaded model
    messages=[
        {"role": "system", "content": "You are a helpful, brief AI assistant."},
        {"role": "user", "content": "Explain what a local LLM is in one short sentence."}
    ],
    temperature=0.7,
)

print(completion.choices[0].message.content)
```

Run your script, and watch your Python code get an answer instantly from your own machine!

---

## License

This project is open-source and available under the [MIT License](LICENSE).
