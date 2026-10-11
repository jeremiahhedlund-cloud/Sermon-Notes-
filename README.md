# Sermon Notes App

An iPhone-friendly sermon recorder, transcription interface, and local notes library.

## Upload to GitHub from iPhone

1. Extract `sermon-notes-app-upload.zip` in the iPhone Files app.
2. Open your **private** GitHub repository `sermon-notes-app` in Safari.
3. Choose **Add file → Upload files** (Safari may need Request Desktop Website).
4. Upload the files from the extracted folder **at the repository root** (not inside another folder): `index.html`, `server.py`, `requirements.txt`, `render.yaml`, `README.md`, and `.gitignore`.
5. Tap **Commit changes**.

## Deploy on Render

1. In Render, choose **New → Blueprint**, connect the GitHub repository, and apply `render.yaml`.
2. Enter **APP_PASSWORD**: a unique secret of at least 16 characters. Do not enter the variable name itself as the value.
3. Enter **OPENAI_API_KEY**: your own API key, which may incur transcription charges. Never put this key in GitHub or `index.html`.
4. Once deployment succeeds, open the Render HTTPS URL and sign in. Any username can be used; the password must match `APP_PASSWORD`.

If Blueprint is unavailable, create a Python Web Service manually with build command `pip install -r requirements.txt`, start command `gunicorn --bind 0.0.0.0:$PORT --workers 1 --timeout 180 server:app`, and add the two environment variables under Environment. Render's free tier and limits can change; check the current plan offered.

## Important limits

- Recording uses the browser microphone; keep Safari awake and in the foreground. For long sermons, use iPhone Voice Memos as a more reliable recording method.
- Download the audio to preserve it. Browser notes are saved only in that browser's local storage and are not synced or backed up.
- The transcription endpoint accepts files up to 25 MB. Longer recordings may need splitting or compression.
- The app sends uploaded audio to OpenAI for transcription. Obtain permission before recording or uploading a sermon.
- HTTP Basic authentication over HTTPS provides simple personal-use access, not a full multi-user account system. Use a unique strong password.
- The app does not yet automatically summarize or extract scripture citations; these are editable note fields.
