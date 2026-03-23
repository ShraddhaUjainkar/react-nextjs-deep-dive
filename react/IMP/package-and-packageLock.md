# 📦 `package.json` vs `package-lock.json`

| Feature | `package.json` | `package-lock.json` |
| :--- | :--- | :--- |
| **What it is** | A **Wishlist** for your project. | A **Blueprint** of exactly what was installed. |
| **Created by** | You (the developer) | npm (automatically) |
| **Versions** | Flexible (`^` or `~`) | Fixed and Exact |
| **Contents** | Top-level packages only | Every single nested package |
| **Purpose** | To define project intent | To ensure "Install Reproducibility" |