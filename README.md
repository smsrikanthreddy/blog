# 🧠 My Dev Journal

Welcome to my personal learning hub! This is where I document my journey through **Machine Learning**, **GenAI**, and **Software Craftsmanship**. This blog is designed as a "Public Second Brain" to capture daily insights, technical deep-dives, and project updates.

---

## 🚀 Built with Quarto
This blog was recently migrated from Fastpages to **[Quarto](https://quarto.org/)**, a state-of-the-art open-source scientific and technical publishing system.

### Why Quarto?
- **Native Jupyter Support**: Author posts directly in `.ipynb` or `.qmd`.
- **Premium Aesthetics**: Clean, modern design with built-in dark mode and glassmorphism.
- **Fast & Flexible**: Powered by Pandoc, making it incredibly fast to render and highly extensible.
- **Automated CI/CD**: Seamless deployment to GitHub Pages via GitHub Actions.

---

## 🛠️ Local Setup

To preview this blog on your local machine:

1.  **Install Quarto CLI**: 
    - [Download for macOS](https://quarto.org/docs/get-started/)
2.  **Clone the Repository**:
    ```bash
    git clone https://github.com/smsrikanthreddy/blog.git
    cd blog
    ```
3.  **Install Python Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```
4.  **Preview the Site**:
    ```bash
    quarto preview
    ```

---

## 📝 How to Add Content

### Adding a New Post
Simply add a new `.md` or `.qmd` file to the `posts/` directory. Use the following YAML frontmatter:

```yaml
---
title: "Your Post Title"
date: "2026-04-14"
categories: [ML, AI]
description: "A short summary of the post."
image: "/images/your-folder/thumbnail.png"
---
```

### Adding a New Notebook
Add your `.ipynb` file to the `notebooks/` directory. To ensure it renders correctly, include a "Raw" cell at the very top of your notebook with the same YAML frontmatter as above.

### Organizing Images
1.  Create a folder for your post's images inside the root `images/` directory.
2.  Reference images in your posts using project-relative paths (starting with `/`):
    - `image: /images/my-new-post/logo.png`
    - `![Alt text](/images/my-new-post/chart.png)`

---

## 🏗️ Project Structure
- `posts/`: Markdown-based blog posts.
- `notebooks/`: Jupyter Notebook-based technical tutorials.
- `images/`: Centralized storage for all media and assets.
- `_quarto.yml`: Main configuration file for the site structure and theme.
- `custom.scss` & `styles.css`: Custom premium styling and design tokens.

---

## 🚢 Deployment
Every push to the `master` branch triggers a **GitHub Action** that automatically builds the site and publishes it to the `gh-pages` branch.

Happy learning! 🚀
