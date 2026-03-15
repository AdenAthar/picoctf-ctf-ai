# CTF-AI: AI-Powered CTF Challenge Solver

A browser-based tool I built for picoCTF challenges that uses an LLM API to analyze encoded strings, ciphertext, source code, and uploaded files. You paste in a challenge or drop a file and it identifies the encoding type, explains how to approach it, attempts a solve, and gives you working code to reproduce the solution.

## Setup

1. Get a free API key from [console.anthropic.com](https://console.anthropic.com)
2. Open `index.html` in a text editor
3. Find this line:
   ```js
   headers: { 'Content-Type': 'application/json', 'x-api-key': 'YOUR_KEY_HERE' ... },
   ```
   Replace `YOUR_KEY_HERE` with your actual API key
4. Open `index.html` in any browser. No server, no install, no build step needed.

Do not commit your API key to a public repo.

## What it does

- Auto-detects encoding type from raw input (Base64, hex, binary, RSA params, HTML, and more)
- File upload support: images are analyzed visually for steganography, text files are read directly, binary files are hex-dumped
- Category modes: Cryptography, Forensics, Web Exploitation, General Skills, Reversing
- Returns structured output covering identification, approach, solution attempt, tools, and learning objectives
- Automatically highlights any picoCTF{...} flags found in the output
- Tracks previous queries in-session

## Tech stack

- Vanilla HTML/CSS/JS (single file, zero dependencies)
- LLM API (messages endpoint)
- Google Fonts (Share Tech Mono + Rajdhani)

## Challenges solved

| Challenge | Category |
|---|---|
| Binary Digits | Forensics |
| gatekeeper | Reversing |
| Access_Control | Blockchain |

## Screenshots

See the screenshots folder for proof of the tool running against live picoCTF challenges.

## Reflection

See REFLECTION.md
