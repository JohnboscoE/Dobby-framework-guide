# Dobby-framework-guide

A step-by-step guide to integrating and using the Fireworks AI Inference API in Python, JavaScript, and TypeScript. This repo demonstrates how to send prompts, receive model completions, and print responses locally.

**🚀 Overview**
The Fireworks AI API lets developers access state-of-the-art large language models (LLMs) through a simple REST interface. You’ll learn how to: • Call Fireworks API from Python, JavaScript, and TypeScript. • Send text prompts and receive AI-generated responses. • Build CLI-style scripts for interactive use.

**🧠 Requirements**
Before you begin, ensure you have:

Fireworks API Key — Sign up at Fireworks.ai
Python 3.10+
Node.js 18+ (for JavaScript/TypeScript)
npm or yarn
Git
VS Code (recommended)
Internet connection

⚙️ Environment Variables
Set your API key as an environment variable.

• macOS / Linux
export FIREWORKS_API_KEY="your_api_key_here"
• Windows (PowerShell)
setx FIREWORKS_API_KEY "your_api_key_here"
OR
Create a .env file in the root of the repository:
FIREWORKS_API_KEY=your_api_key_here
Each script loads this file automatically using dotenv.

⚠️ Never commit your .env file to GitHub.
