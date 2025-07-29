# AI Voice Interviewer with n8n

This project is a fully functional AI-powered voice interviewer. It takes a user's resume text and a job description, and then conducts a voice-based interview, asking relevant questions based on the provided context.

## Features

- **Voice-to-Text & Text-to-Speech:** Uses browser-native APIs for a real-time voice conversation.
- **Context-Aware:** The AI (powered by Google Gemini) analyzes the user's resume against the job description to ask intelligent, relevant questions.
- **Self-Hosted:** Runs on a local n8n instance powered by Docker.
- **Simple Frontend:** A single HTML file acts as the user interface.

## Prerequisites

Before you begin, you will need:
- [Docker](https://www.docker.com/products/docker-desktop/) installed on your machine.
- A Large Language Model (LLM) API key. This project is configured for **Google Gemini**, but can be adapted for OpenAI.
- Basic knowledge of how to use the command line.

## Setup Instructions

### 1. Clone the Repository

First, get the project files onto your computer.
```bash
git clone [https://github.com/sarry000/ai-voice-interviewer.git](https://github.com/sarry000/ai-voice-interviewer.git)
cd ai-voice-interviewer
```

### 2. Configure the Environment

The n8n server is configured using a `.env` file.

- Navigate into the `n8n_setup` directory.
- Rename the `.env.example` file to `.env`.
- Open the `.env` file and set your desired `N8N_BASIC_AUTH_USER` and `N8N_BASIC_AUTH_PASSWORD`.

### 3. Start the n8n Server

Run the following command from inside the `n8n_setup` directory to start the n8n Docker container.
```bash
docker-compose up -d
```
This will download the n8n image and start the server in the background.

### 4. Configure n8n

- Open your web browser and go to `http://localhost:5678`.
- Log in with the username and password you set in the `.env` file.
- Create a new, empty workflow.
- In the workflow editor, go to **File -> Import from File** and select the `Interviewer-Workflow.json` file from the `n8n_workflow` directory.
- **Important:** Inside the workflow, click on the **Google Gemini Chat Model** node and connect your own Google Gemini API credential.
- **Save** and **Activate** the workflow.

### 5. Use the Interviewer

- Click on the **Webhook** node in your n8n workflow and copy the **Production URL**.
- Open the `voice-interview.html` file (from the `frontend` folder) in your web browser.
- Paste the Production URL into the first box.
- Fill out the rest of the form and click "Start Interview"!
