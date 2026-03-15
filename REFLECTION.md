# Reflection: CTF-AI Tool (picoCTF EA-1)

Activity: picoCTF challenge solving + AI solver tool development
Date: March 14, 2026
Course: CPT_S 427 - Distributed Systems Security

## Activity description

For this assignment I participated in picoCTF, a cybersecurity CTF competition run by Carnegie Mellon University. Instead of just grinding through challenges manually, I built a browser-based tool called CTF-AI that takes a challenge description, encoded string, or uploaded file and uses an LLM API to analyze it and attempt a solve. The output is structured into six sections: identification, approach, solution, flag, tools, and learning objective, which mirrors the format of a real CTF writeup. I then used the tool on three live picoGym challenges: a forensics challenge involving a binary-encoded JPEG (Binary Digits), a reverse engineering challenge involving integer parsing in a compiled Linux binary (gatekeeper), and a Solidity smart contract challenge involving broken access control on an Ethereum testnet (Access_Control).

## Technical decisions

The main decision was building this as a single HTML/CSS/JS file instead of a Python script or a full web app with a backend. The reasoning was that a single file has zero setup cost, which matters a lot if you want to actually use something during a timed CTF. No virtual environment, no npm install, just open the file.

The other interesting decision was how to handle file uploads. My first instinct was to branch on file extension but that caused a bug: digits.bin has a .bin extension but is actually a plaintext ASCII string of 1s and 0s, so treating it as a true binary file and hex-dumping it would have broken the analysis. I changed the logic to always try reading the file as text first and check if it's ASCII before falling back to a hex dump. For images, the file gets base64 encoded and sent directly to the vision endpoint so the model can look for steganography or hidden text visually.

For the prompt structure I picked six fixed output sections because unstructured LLM output is hard to scan quickly when you're trying to solve something fast. The sections also happen to match what a good CTF writeup looks like, which made the repo easier to document.

One thing I skipped was streaming responses. It would have made the tool feel more responsive but added a decent amount of complexity to the JavaScript for a pretty minor UX improvement, so I left it out.

## Contributions

Solo. All the code, prompt design, and UI work is mine.

## Quality assessment

The tool worked well on the three challenges I ran it against. Binary Digits was a complete solve: the binary string decoded to a JPEG and the flag was printed in the image in plain text. The gatekeeper challenge was a solid partial solve through static analysis, strings extraction revealed the strtol integer parsing trick and the reversed string hint, though the actual flag requires connecting to a live netcat instance which the browser tool can't do. Access_Control was the cleanest solve: the missing access modifier on changeOwner() was immediately obvious from reading the contract code, and the three-step exploit (changeOwner, solve, getFlag) follows directly from the vulnerability.

The biggest weakness in the tool is anything that requires dynamic analysis, running a binary, examining registers, fuzzing. A browser tool just can't do that. If I redid this I would write a Python companion script that runs strings, objdump, and ltrace on uploaded binaries and feeds the output into the analysis. I would also add an API key input box in the UI so the key does not have to be hardcoded in the file. On the competition side I would spend more time on the blockchain category since Access_Control made it clear that smart contract security maps really well to the distributed systems and authentication concepts from CPT_S 427, both are fundamentally about who is allowed to do what in a system with no central authority enforcing trust.
