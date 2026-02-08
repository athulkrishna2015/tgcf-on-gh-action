# tgcf-on-gh-action

This is a specialized version of `tgcf` designed to run entirely on **GitHub Actions** while saving its progress (message `offset`) directly back to the repository.

## Features
- **Zero Server Cost:** Runs on GitHub's free infrastructure.
- **Auto-Persistence:** Automatically commits the updated `tgcf.config.json` after every run.
- **Privacy Focused:** Your API keys and session strings are kept in GitHub Secrets, never in the code.
- **Custom Fixes:** Includes patched handling for protected chats and robust chat ID resolution.

## Setup Instructions

### 1. Create Repository
1. Create a **Private** repository on GitHub.
2. Push this code to your new repository.

### 2. Configure Secrets
Go to your repository **Settings > Secrets and variables > Actions** and add the following secrets:
- `API_ID`: Your Telegram API ID.
- `API_HASH`: Your Telegram API Hash.
- `SESSION_STRING`: Your Telegram Session String (User account).

### 3. Customize Forwards
Edit the `tgcf.config.json` file in this repository to define your source and destination chats. Do not worry about the `login` section; those values are injected automatically from your secrets during the run.

## How it Works
- The workflow runs on a schedule (every hour) or can be triggered manually via the **Actions** tab.
- After forwarding messages, the GitHub Action user will commit the changes to `tgcf.config.json` with the message `Update offset [skip ci]`.
- `[skip ci]` ensures that the automatic commit doesn't trigger a recursive loop of actions.

## Local Development
If you want to run this locally for testing:
1. Install dependencies: `pip install -r requirements.txt && pip install -e .`
2. Create a `.env` file with your credentials.
3. Run `tgcf past`.