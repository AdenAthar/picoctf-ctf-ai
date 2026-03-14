# Reflection — CTF-AI Tool (picoCTF EA-1)

**Activity**: picoCTF / picoGym challenge solving + AI solver tool development  
**Date**: March 14, 2026  
**Course**: CPT_S 427 — Distributed Systems Security

---

## Activity description

For this extracurricular assignment I participated in picoCTF, a cybersecurity Capture The Flag competition run by Carnegie Mellon University's CyLab Security and Privacy Institute. The platform hosts challenges across six domains: general skills, cryptography, web exploitation, forensics, binary exploitation, and reverse engineering. Rather than only solving challenges manually, I built a browser-based AI solver tool — CTF-AI — that takes a challenge description or raw encoded string as input and uses a large language model API to identify the encoding type, explain the attack methodology, attempt a direct solve, and recommend relevant CLI tools or Python scripts. I then ran the tool against several live picoGym challenges to validate it and generate proof of participation.

## Technical decisions

The primary decision was to build the deliverable as a single-file HTML/CSS/JS app rather than a Python CLI or full-stack app. This kept the barrier to use zero — no install, no environment, just open the file. It also forced me to think about what logic belongs client-side versus what should be delegated to the model. I chose to keep encoding detection (Base64, hex, binary, RSA parameters, HTML signatures) in client-side JavaScript because deterministic pattern matching is fast and cheap and reduces unnecessary API calls. The AI is reserved for the reasoning-heavy part: interpreting ambiguous inputs, chaining multiple decode steps, and explaining the underlying cryptographic concept.

For the prompt design I structured the output into six sections: identification, approach, solution attempt, flag, tools, and learning objective. This was intentional — unstructured AI output is hard to act on during a timed CTF. The sections mirror how an experienced CTF player documents a writeup, which also made the output easier to parse for the solve history feature.

One tradeoff was skipping streaming responses. Streaming would have made the tool feel faster for longer outputs but added meaningful complexity to the JS without a clear UX win for the typical short challenge inputs picoCTF uses.

## Contributions

Solo participation. All code, prompt engineering, and UI design are my own work.

## Quality assessment

The tool handles the categories it was designed for well — encoding identification is accurate for common patterns and the AI analysis is genuinely useful for cryptography and general skills challenges, which make up the bulk of beginner and intermediate picoCTF content. The weakest area is binary exploitation and reversing: those categories require running actual binaries and examining memory, which a browser-based tool cannot do. I noted this as an explicit limitation rather than pretending the tool covers it.

If I were doing this again I would add a Python companion script that handles the binary exploitation gap — running `strings`, `objdump`, and `ltrace` automatically and piping output back to the AI. I would also add a proper API key input field so the tool is fully self-contained for anyone who clones the repo, rather than relying on the demo runtime. On the competition side, I would spend more time in the forensics category since that maps most directly to the network security and cryptographic protocol material from CPT_S 427 — analyzing packet captures with Wireshark is the same skill set as the lab work in this course.
