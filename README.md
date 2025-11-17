# Dobby-framework-guide

A step-by-step guide to integrating and using the Fireworks AI Inference API in Python, JavaScript, and TypeScript. This repo demonstrates how to send prompts, receive model completions, and print responses locally.

********************************************************************************************************************************************************

🧭 Table of Contents
---
* [Overview](#overview)

* [Requirements](#requirements)

* [Environment Variables](#environment-variables)

* [Python Setup](#python-setup)
* [JavaScript Setup](#javascript-setup)
* [TypeScript Setup](#typescript-setup)
* [Example Outputs](#example-outputs)
* [Testing](#testing)
* [Project Ideas](#project-ideas)
* [Support](#support)

****************************************************************************

🚀 Overview
__

The Fireworks AI API lets developers access state-of-the-art large language models (LLMs) through a simple REST interface. You’ll learn how to: • Call Fireworks API from Python, JavaScript, and TypeScript. • Send text prompts and receive AI-generated responses. • Build CLI-style scripts for interactive use.

************

🧠 Requirements
__

Before you begin, ensure you have:

Fireworks API Key — Sign up at Fireworks.ai

Python 3.10+

Node.js 18+ (for JavaScript/TypeScript)

npm or yarn

Git

VS Code (recommended)

Internet connection

****************************

⚙️ Environment Variables
---
Set your API key as an environment variable.

* **macOS / Linux:**

```bash
export FIREWORKS_API_KEY="your_api_key_here"

```

 Windows (PowerShell)

 ```bash
setx FIREWORKS_API_KEY "your_api_key_here"

```

OR

Create a .env file in the root of the repository:
  
 ```bash
FIREWORKS_API_KEY=your_api_key_here
```
Each script loads this file automatically using dotenv.

⚠️ Never commit your .env file to GitHub.

********************************************************

🐍 Python Setup
_______

• Create a Project Folder

 ```bash
 mkdir fireworks-python
cd fireworks-python
```

• Create a Virtual Environment (recommended)

 ```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

• Install Dependencies

 ```bash
pip install requests python-dotenv
```

• Create fireworks_demo.py

 ```bash

import os
import requests

API_KEY = os.getenv("FIREWORKS_API_KEY")
API_URL = "https://api.fireworks.ai/inference/v1/completions"
MODEL_ID = "accounts/sentientfoundation/models/dobby-unhinged-llama-3-3-70b-new"

def call_fireworks(prompt):
    headers = {"Authorization": f"Bearer {API_KEY}"}
    data = {"model": MODEL_ D, "prompt": prompt, "max_tokens": 500}
    response = requests.post(API_URL, headers=headers, json=data)
    response.raise_for_status()
    return response.json()["choices"][0]["text"].strip()

if __name__ == "__main__":
    user_input = input("Enter text to explain or analyze: ")
    output = call_fireworks(f"Explain this in simple terms: {user_input}")
    print("\n--- AI OUTPUT ---\n")
    print(output)

```

• Run the Script

 ```bash
python fireworks_demo.py
```
********************************

**💻 JavaScript Setup**

• Initialize the Project

 ```bash
mkdir fireworks-js
cd fireworks-js
npm init -y
npm install node-fetch
```

• Create fireworks_demo.js

 ```bash
import fetch from "node-fetch";

const FIREWORKS_API_KEY = process.env.FIREWORKS_API_KEY;
const API_URL = "https://api.fireworks.ai/inference/v1/completions";
const MODEL_ID = "accounts/sentientfoundation/models/dobby-unhinged-llama-3-3-70b-new";

async function callFireworks(prompt) {
  const response = await fetch(API_URL, {
    method: "POST",
    headers: {
      "Authorization": `Bearer ${FIREWORKS_API_KEY}`,
      "Content-Type": "application/json",
    },
    body: JSON.stringify({ model: MODEL_ID, prompt, max_tokens: 500 }),
  });

  const data = await response.json();
  return data.choices[0].text.trim();
}

const prompt = "Explain quantum computing in simple terms.";

callFireworks(prompt)
  .then(output => console.log("\n--- AI OUTPUT ---\n" + output))
  .catch(err => console.error("⚠️ Error:", err.message));

```

• Run the Script

 ```bash
node fireworks_demo.js
```

****************************


**🧠 TypeScript Setup**
__

• Initialize Project

 ```bash
mkdir fireworks-ts
cd fireworks-ts
npm init -y
npm install node-fetch @types/node-fetch
npm install typescript ts-node @types/node --save-dev
```

• Add tsconfig.json

 ```bash
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "strict": true,
    "esModuleInterop": true
  }
}
```

• Create fireworks_demo.ts

 ```bash
import fetch from "node-fetch";
import readline from "readline";

const API_URL = "https://api.fireworks.ai/inference/v1/completions";
const MODEL_ID = "accounts/sentientfoundation/models/dobby-unhinged-llama-3-3-70b-new";
const API_KEY = process.env.FIREWORKS_API_KEY;

if (!API_KEY) {
  console.error("Please set FIREWORKS_API_KEY in your environment.");
  process.exit(1);
}

interface FireworksChoice {
  text: string;
}

interface FireworksResponse {
  choices: FireworksChoice[];
}

async function callFireworks(prompt: string, maxTokens = 500, temperature = 0.7): Promise<string> {
  const response = await fetch(API_URL, {
    method: "POST",
    headers: {
      "Authorization": `Bearer ${API_KEY}`,
      "Content-Type": "application/json",
    },
    body: JSON.stringify({ model: MODEL_ID, prompt, max_tokens: maxTokens, temperature }),
  });

  if (!response.ok) throw new Error(await response.text());
  const data = (await response.json()) as FireworksResponse;
  return data.choices?.[0]?.text?.trim() || "(No response)";
}

function askQuestion(query: string): Promise<string> {
  const rl = readline.createInterface({ input: process.stdin, output: process.stdout });
  return new Promise((resolve) => rl.question(query, (ans) => {
    rl.close();
    resolve(ans);
  }));
}

async function main() {
  console.log("🔥 Fireworks API Demo (TypeScript)\n");
  const userInput = await askQuestion("Enter text to explain or analyze: ");
  const prompt = `Explain this text clearly and simply:\n\n${userInput}`;
  console.log("\n⏳ Contacting Fireworks API...");
  const result = await callFireworks(prompt);
  console.log("\n--- AI OUTPUT ---\n");
  console.log(result);
}

main();
```

• Run it:

 ```bash
npx ts-node fireworks_demo.ts
```
****************

Example Output
___

 ```bash
🔥 Fireworks API Demo

Enter text to explain or analyze: Quantum computing uses qubits instead of bits.

⏳ Contacting Fireworks API...

--- AI OUTPUT ---

Quantum computing uses qubits that can represent both 0 and 1 at the same time, allowing massive parallel calculations and faster problem solving.
 ```

__

🧪 Testing
__

To verify everything works:

 ```bash
# Python
cd python && python fireworks_demo.py

# JavaScript
cd javascript && node fireworks_demo.js

# TypeScript
cd typescript && npx ts-node fireworks_demo.ts
 ```

****************

🧭 Project Ideas
_____

AI Tutor Bot (Telegram or Web)

Automatic Quiz Generator

Study Summarizer

Text Explainer CLI Tool

Chat Interface for learners
****************************

💬 Support

___

if you encounter issues:

Check your API key is valid and set in .env

Verify you have network access to https://api.fireworks.ai/

Visit the Fireworks API Documentation

Or open an issue on GitHub: Issues → New Issue

✅ Done!

You now have the Dobby Framework running in three environments. You can extend it for bots, dashboards, or educational tools.




