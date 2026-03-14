# CTF-AI — AI-Powered CTF Challenge Solver

An AI-assisted Capture The Flag solver tool built for picoCTF challenges. Paste in any encoded string, ciphertext, or challenge description and the tool identifies the encoding type, explains the methodology, and attempts a full solve — powered by a large language model API.

---

## Setup

1. Get a free API key from [console.anthropic.com](https://console.anthropic.com) (no credit card required to start)
2. Open `index.html` in a text editor
3. Find this line:
   ```js
   headers: { 'Content-Type': 'application/json' },
   ```
   Replace it with:
   ```js
   headers: { 'Content-Type': 'application/json', 'x-api-key': 'YOUR_API_KEY_HERE', 'anthropic-version': '2023-06-01' },
   ```
4. Open `index.html` in any browser — no server, no install, no build step

> Do not commit your API key to a public repository.

---

## What it does

- **Auto-detects** encoding/cipher type from raw input (Base64, hex, binary, RSA params, HTML, and more)
- **File upload support**: drag and drop any file — images are analyzed visually for steganography, text files are read directly, binary files are hex-dumped
- **Category modes**: Cryptography, Forensics, Web Exploitation, General Skills, Reversing
- **AI-powered analysis**: returns structured output covering identification, approach, solution attempt, tools, and learning objectives
- **Flag highlighting**: automatically highlights any `picoCTF{...}` flags found in the output
- **Solve history**: tracks previous queries in-session
- **One-file deployment**: pure HTML/CSS/JS — no build step, no dependencies

---

## Screenshots

See `/screenshots/` for proof of the tool running against live picoCTF challenges.

---

## Tech stack

- Vanilla HTML/CSS/JS (single file, zero dependencies)
- LLM API (messages endpoint)
- Google Fonts (Share Tech Mono + Rajdhani)

---

## Cybersecurity relevance

This tool engages with the following picoCTF challenge categories:

| Category | Coverage |
|---|---|
| Cryptography | Caesar, ROT13, Base64, XOR, RSA parameter identification |
| Forensics | File signature hints, steganography, image analysis, metadata |
| Web Exploitation | XSS/SQLi pattern recognition, HTTP header analysis |
| General Skills | Encoding detection, CLI tool suggestions |
| Reverse Engineering | Obfuscation pattern hints, decompilation guidance |

---

## Reflection

See [REFLECTION.md](./REFLECTION.md)
