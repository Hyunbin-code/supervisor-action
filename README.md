# 🛡️ Supervisor.ai: The Automated QA Intern

[![Supervisor Status](https://img.shields.io/badge/Status-Beta-blue)](https://github.com/marketplace/actions/supervisor-ai)

**Supervisor** is an AI-powered code auditor that runs entirely within your GitHub Actions workflow. It analyzes your Pull Requests for **security risks, hallucinations, and logic flaws** before you merge.

> **"Parasitic Compute"**: We use YOUR GitHub Actions runner to do the heavy AI processing. Our HQ server just stores the results. This makes Supervisor **100% Free** for the underlying compute (you pay only your own OpenAI API costs).

---

## 🚀 Features

- **🔎 DeepThink Audits**: Uses `gpt-4o` or similar models to reason about your code changes.
- **💬 PR Comments**: Posts actionable feedback directly on the Pull Request.
- **📊 Real-time Dashboard**: Track your "Risk Score" over time on our HQ Dashboard.
- **🛡️ Viral Badge**: Show off your code safety with a dynamic README badge.

## 📦 Usage

Add this to your `.github/workflows/audit.yml`:

```yaml
name: Supervisor Audit

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  audit:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3
        with:
          fetch-depth: 0 # Important for diff analysis!

      - name: Run Supervisor
        uses: your-github-username/supervisor-action@v1
        with:
          openai_key: ${{ secrets.OPENAI_API_KEY }}
          hq_secret: ${{ secrets.SUPERVISOR_KEY }} # Optional: For Dashboard history
```

## ⚙️ Inputs

| Input | Description | Required | Default |
| :--- | :--- | :--- | :--- |
| `openai_key` | Your OpenAI API Key (we never store this!) | **Yes** | N/A |
| `hq_secret` | Project Key from Supervisor HQ (for Dashboard) | No | `demo` |
| `github_token` | Automatically provided by Actions | **Yes** | `${{ github.token }}` |

## 🏆 Badges

Add this to your `README.md` to show your Audit Score:

```markdown
[![Supervisor Audit](http://150.136.81.6:8000/api/v1/badge?project_key=YOUR_PROJECT_KEY&repo=YOUR_REPO_NAME)](http://150.136.81.6:8000)
```

## 📜 License

MIT License. Free to fork, free to use.
