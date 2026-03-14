# CTF-AI — AI-Powered CTF Challenge Solver

An AI-assisted Capture The Flag solver tool built for picoCTF challenges. Paste in any encoded string, ciphertext, or challenge description and the tool identifies the encoding type, explains the methodology, and attempts a full solve — powered by a large language model API.

---

## What it does

- **Auto-detects** encoding/cipher type from raw input (Base64, hex, binary, RSA params, HTML, and more)
- **Category modes**: Cryptography, Forensics, Web Exploitation, General Skills, Reversing
- **AI-powered analysis**: Sends the challenge to an LLM API, returns structured output covering identification, approach, solution attempt, tools, and learning objectives
- **Flag highlighting**: Automatically highlights any `picoCTF{...}` flags found in the output
- **Solve history**: Tracks previous queries in-session
- **One-file deployment**: Pure HTML/CSS/JS — no build step, no dependencies

---

## Usage

Open `index.html` in a browser. No installation required.

> Note: To deploy independently, add your LLM API key to the fetch headers in `index.html`.

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
| Forensics | File signature hints, steganography description, metadata |
| Web Exploitation | XSS/SQLi pattern recognition, HTTP header analysis |
| General Skills | Encoding detection, CLI tool suggestions |
| Reverse Engineering | Obfuscation pattern hints, decompilation guidance |

---

## Reflection

See [REFLECTION.md](./REFLECTION.md)
