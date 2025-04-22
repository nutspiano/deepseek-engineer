# DeepSeek Engineer 🐋

## Overview

This repository contains a powerful coding assistant application that integrates with the DeepSeek API to process user conversations and generate structured JSON responses. Through an intuitive command-line interface, it can read local file contents, create new files, and apply diff edits to existing files in real time.

## Key Features

1. DeepSeek Client Configuration
   - Automatically configures an API client to use the DeepSeek service with a valid DEEPSEEK_API_KEY. 
   - Connects to the DeepSeek endpoint specified in the environment variable to stream GPT-like completions. 

2. Data Models
   - Leverages Pydantic for type-safe handling of file operations, including:
     • FileToCreate – describes files to be created or updated.  
     • FileToEdit – describes specific snippet replacements in an existing file.  
     • AssistantResponse – structures chat responses and potential file operations.  

3. System Prompt
   - A comprehensive system prompt (system_PROMPT) guides conversation, ensuring all replies strictly adhere to JSON output with optional file creations or edits.  

4. Helper Functions
   - read_local_file: Reads a target filesystem path and returns its content as a string.  
   - create_file: Creates or overwrites a file with provided content.  
   - show_diff_table: Presents proposed file changes in a rich, multi-line table.  
   - apply_diff_edit: Applies snippet-level modifications to existing files.  

5. "/add" Command
   - Users can type "/add path/to/file" to quickly read a file's content and insert it into the conversation as a system message.  
   - Users can also type "/add path/to/folder" to add all files in a directory (excluding binaries and hidden files).
   - This allows the assistant to reference the file contents for further discussion, code generation, or diff proposals.  

6. Conversation Flow
   - Maintains a conversation_history list to track messages between user and assistant.  
   - Streams the assistant's replies via the DeepSeek API, parsing them as JSON to preserve both the textual response and the instructions for file modifications.  

7. Interactive Session
   - Run the script (for example: "python3 main.py") to start an interactive loop at your terminal.  
   - Enter your requests or code questions. Enter "/add path/to/file" to add file contents to the conversation.  
   - When the assistant suggests new or edited files, you can confirm changes directly in your local environment.  
   - Type "exit" or "quit" to end the session.  

## Getting Started

1. Prepare a .env file with your DeepSeek API key:
   DEEPSEEK_API_KEY=your_api_key_here

2. Install dependencies and run (choose one method):

   ### Using pip
   ```bash
   pip install -r requirements.txt
   python3 main.py
   ```

   ### Using uv (faster alternative)
   ```bash
   uv venv

   uv run main.py
   ```

3. Enjoy multi-line streaming responses, file read-ins with "/add path/to/file", and precise file edits when approved.

### Reasoning-Enabled Version (r1.py)
A new script `r1.py` has been added that uses DeepSeek's Reasoning Model (`deepseek-reasoner`). This version includes Chain of Thought (CoT) reasoning capabilities:

- Shows the AI's reasoning process before providing the final answer
- Maintains all original features (file operations, diff editing, etc.)
- Displays thought process in a dedicated panel
- Only uses final conclusions in conversation history
- Run it with `python3 r1.py` or `uv run r1.py` for an enhanced experience with visible reasoning

> **Note**: This is an experimental project developed by Skirano to test the new DeepSeek v3 API capabilities. It was developed as a rapid prototype and should be used accordingly.

## Model Selector and API Configuration

The application now supports selecting different models and configuring their respective APIs, including DeepSeek, OpenAI, local OpenAI compatible endpoints, and Mistral.

### How to Use the Model Selector

1. When you run the script (`python3 main.py`), you will be prompted to select a model:
   - 1. DeepSeek
   - 2. OpenAI
   - 3. Local OpenAI Compatible Endpoint
   - 4. Mistral

2. Enter the number corresponding to your choice.

3. The application will configure the client with the appropriate API key and base URL based on your selection.

### Configuring Different APIs

1. **DeepSeek**
   - Ensure you have the `DEEPSEEK_API_KEY` set in your `.env` file.
   - The base URL for DeepSeek is pre-configured as `https://api.deepseek.com`.

2. **OpenAI**
   - Ensure you have the `OPENAI_API_KEY` set in your `.env` file.
   - The base URL for OpenAI is pre-configured as `https://api.openai.com`.

3. **Local OpenAI Compatible Endpoint**
   - Ensure you have the `LOCAL_OPENAI_API_KEY` and `LOCAL_OPENAI_BASE_URL` set in your `.env` file.
   - The base URL should point to your local OpenAI compatible endpoint.

4. **Mistral**
   - Ensure you have the `MISTRAL_API_KEY` set in your `.env` file.
   - The base URL for Mistral is pre-configured as `https://api.mistral.com`.

By following these steps, you can easily switch between different APIs and leverage the capabilities of each within the same application.
