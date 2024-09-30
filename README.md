# Chain-of-Thought Chatbot using Semantic Kernel and Azure OpenAI

This project implements a chatbot capable of **chain-of-thought reasoning** by orchestrating multiple AI agents using Microsoft's [Semantic Kernel](https://github.com/microsoft/semantic-kernel) and Azure OpenAI services. The chatbot interacts with users through a web interface powered by [Gradio](https://gradio.app/), providing detailed and well-thought-out answers to complex questions.

## Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Install Dependencies](#2-install-dependencies)
  - [3. Set Up Azure OpenAI Credentials](#3-set-up-azure-openai-credentials)
  - [4. Configure Deployment Name](#4-configure-deployment-name)
- [Running the Chatbot](#running-the-chatbot)
- [Usage](#usage)
- [Example Interaction](#example-interaction)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Chain-of-Thought Reasoning**: Breaks down user queries into a series of reasoning steps for comprehensive answers.
- **Multiple AI Agents**: Utilizes three specialized agents to simulate a thoughtful conversation.
- **Semantic Kernel Integration**: Manages AI agents and their interactions efficiently.
- **Gradio Web Interface**: Offers an easy-to-use web interface for seamless user interaction.

## Architecture

The chatbot employs three distinct AI agents:

1. **Initial Agent** (`Initial`):
   - **Role**: Serves as the first point of contact, interpreting the user's question and setting the stage for deeper analysis.
   - **Instructions**: Guides the Thinker agent to begin the reasoning process based on the user's input.

2. **Thinker Agent** (`Thinker`):
   - **Role**: Performs iterative, step-by-step reasoning to explore different aspects of the question.
   - **Instructions**: Continues thinking until it determines that it has sufficiently explored the topic.

3. **Answerer Agent** (`Answerer`):
   - **Role**: Provides the final, comprehensive answer by synthesizing the Thinker's reasoning.
   - **Instructions**: Delivers an accurate and complete response to the user's query.

The agents interact within a conversational framework managed by Semantic Kernel, utilizing strategies for function selection and termination to ensure coherent and efficient dialogue.

## Prerequisites

- **Python**: Version 3.10 or higher.
- **Azure OpenAI Account**: Access to Azure OpenAI services with a deployed model (e.g., gpt-4o).
- **API Credentials**: Your Azure OpenAI API key and endpoint URL.

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/manwithaplandy/llm-reasoning-agent.git
cd llm-reasoning-agent
```

### 2. Install Dependencies

Install the required Python packages:

```bash
pip install -r requirements.txt
```

### 3. Set Up Azure OpenAI Credentials

Obtain your **Azure OpenAI API Key** and **Endpoint** from the Azure portal.

Set the following environment variables in your shell:

```bash
export AZURE_OPENAI_API_KEY='your-api-key'
export AZURE_OPENAI_ENDPOINT='https://your-resource-name.openai.azure.com/'
```

### 4. Configure Deployment Name

Make sure you have a deployment in Azure OpenAI called "gpt-4o". 

Alternatively, you can change the deployment name with an environment variable

In the `app.py` script, update the `deployment_name` variable with the name of your Azure OpenAI deployment:

```bash
export DEPLOYMENT_NAME="gpt-4-turbo"  # Replace with your actual deployment name
```

Ensure that the deployment name matches the model you have deployed on Azure (e.g., "gpt-4").

## Running the Chatbot

Start the Gradio application:

```bash
gradio app.py
```

Upon running, Gradio will launch a local web server. Look for a URL in the terminal output similar to `http://127.0.0.1:7860/` and open it in your web browser to interact with the chatbot.

## Usage

- **Input**: Type your question or prompt into the text box provided.
- **Process**: The chatbot will display the thought process step-by-step as it formulates an answer.
- **Output**: Receive a detailed and comprehensive answer to your query.

## Example Interaction

**User Input**:

```
Can you explain how photosynthesis works in plants?
```

**Chatbot Response**:

```
# USER: 
Can you explain how photosynthesis works in plants?

# assistant - Initial: 
Please begin thinking about how to explain the process of photosynthesis in plants to the user.

# assistant - Thinker: 
First, consider the role of chlorophyll in capturing sunlight.

# assistant - Thinker: 
Next, think about how plants convert carbon dioxide and water into glucose and oxygen.

# assistant - Thinker: 
Also, reflect on the importance of photosynthesis in the global ecosystem.

# assistant - Thinker: 
I am done thinking.

# assistant - Answerer: 
Photosynthesis in plants is a process where chlorophyll in the leaves captures sunlight to convert carbon dioxide from the air and water from the soil into glucose, a type of sugar that provides energy for the plant. Oxygen is released as a byproduct. This process is fundamental to life on Earth as it produces the oxygen we breathe and forms the base of the food chain.
```

## Project Structure

- **app.py**: The main script containing the chatbot implementation.
- **README.md**: Documentation and instructions.
- **requirements.txt**: List of Python dependencies (if provided).

## Troubleshooting

- **Environment Variables Not Set**: Ensure `AZURE_OPENAI_API_KEY` and `AZURE_OPENAI_ENDPOINT` are correctly set in your environment.
- **Incorrect Deployment Name**: Verify that the `deployment_name` in the script matches your Azure OpenAI deployment name.
- **Dependency Issues**: Make sure all required packages are installed. If you encounter issues with `semantic-kernel`, check their [official repository](https://github.com/microsoft/semantic-kernel) for installation guidance.
- **API Version Mismatch**: If you encounter API version errors, adjust the `api_version` parameter in the `AzureChatCompletion` service initialization to match the version supported by your Azure OpenAI deployment.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or suggestions.

## License

This project is licensed under the [MIT License](LICENSE).

---

**Note**: Replace placeholders like `yourusername`, `your-api-key`, `your-resource-name`, and `your-deployment-name` with your actual information.
