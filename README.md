# PMP Practice Exam Simulator

A static, no-build web app that simulates a full PMP practice exam.

- **Login page** (username `pmpractice01`) gates access to the practice session.
- **Instructions page** explains the format and timing.
- **180 questions** (case studies, single and multiple-select) with a **NEXT** button, Previous, flagging and a question navigator.
- **4-hour exam timer** and one **20-minute break** (the exam clock pauses during the break).
- Auto-submit at zero, score + full answer review at the end, progress saved in the browser.

## Run locally
Open `index.html` in a browser (no server needed), or run `python -m http.server` and visit http://localhost:8000.

## Deploy on GitHub Pages
1. Push this folder to a GitHub repository.
2. Settings -> Pages -> Deploy from branch -> `main` / root.
3. Open the published URL.

## Update the questions
```bash
pip install openpyxl
python tools/convert_xlsx.py PMP_practice_Q_A.xlsx questions.js
```
The converter reads the `180 Question PMP` sheet (questions, options, answer key, case studies).

## Security note
GitHub Pages is static hosting, so the login is a client-side gate only: credentials are stored as SHA-256 hashes, which keeps casual visitors out but is **not real security**. Anyone who can read the source can bypass it, and the answer key ships with `questions.js`. For genuine access control use a private repo or a backend/auth service.

To change the credentials, replace `USER_HASH` and `PASS_HASH` in `index.html` with new SHA-256 hashes.
