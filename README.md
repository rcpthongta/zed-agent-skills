# 🤖 Zed Agent Skills

This repository is a collection of Markdown (`.md`) files that serve as custom prompts and skills to enhance the capabilities of AI Agents within the **[Zed Editor](https://zed.dev/)**.

## 📦 Available Skills

| Skill File | Description |
| :--- | :--- |
| [`git-commit-skill.md`](./git-commit-skill.md) | Generates accurate Git commit messages from diffs following Conventional Commits standards, strictly scoped to output only the message. |
| *(Future skill files)* | *(Description...)* |

## 🚀 How to Use

Zed Agent supports fetching skills directly from Markdown files hosted on GitHub. To install a skill from this repository:

1. Navigate to the desired `.md` skill file in this repository.
2. Click the **Raw** button at the top right of the file view.
3. Copy the raw file URL (it should start with `https://raw.githubusercontent.com/...`).
4. Open your Zed Editor.
5. Open the AI Assistant or Command Palette and navigate to **Agent Configuration > Skills > Create Skill**.
6. Paste the copied Raw URL into the input field.
7. Zed will automatically fetch and populate the form. Save it to start using your new skill immediately.

## 🛠️ How to Create a New Skill

If you want to contribute or write a new skill for this repository, it is highly recommended to follow this structure to ensure the AI behaves predictably:

- **Scope:** Clearly define what the AI is responsible for and **strictly what it MUST NOT do**.
- **Workflow:** Provide a step-by-step reasoning or execution process.
- **Output Rules:** Specify the exact format of the desired output (e.g., no code fences, no conversational filler, JSON only).
- **Examples:** Include examples of both valid and invalid outputs to guide the AI.

---
*Built to enhance productivity in Zed Editor.*
