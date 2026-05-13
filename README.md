# 📥 Universal Downloader (GitHub Actions)

> **Smart download tool that splits large files ( >90MB ) and keeps small ones intact. Perfect for censorship environments and unstable internet.**

[![GitHub stars](https://img.shields.io/github/stars/mamadprogrammer/downloadfile)](https://github.com/mamadprogrammer/downloadfile/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/mamadprogrammer/downloadfile)](https://github.com/mamadprogrammer/downloadfile/network)

---

## 🎯 What does it do?

This GitHub Actions workflow downloads any file from a direct link and:

- ✅ **Keeps files under 90MB as-is** (no splitting)
- ✂️ **Splits files over 90MB** into 90MB chunks (`part_aa`, `part_ab`, ...)
- 📦 **Commits and pushes** everything to your repository automatically
- 🌍 **Bypasses internet restrictions** using GitHub's global servers

Perfect for downloading **anime, movies, PDFs, or any file** when your local internet is censored or unstable.

---

## 🚀 How to use it?

### 1. **Fork this repository** to your GitHub account

### 2. **Enable GitHub Actions** in your fork settings
   - Go to `Settings` → `Actions` → `General`
   - Under **Workflow permissions**, select **Read and write permissions**

### 3. **Run the workflow**
   - Go to the **Actions** tab
   - Select **📥 Download (Conditional Split)**
   - Click **Run workflow**
   - Paste your direct **file URL** and start

### 4. **Get your file**
   - After completion, your file(s) will be in the `downloads/` folder of your repository
   - If split, merge them using:
     ```bash
     cat part_* > myfile.mkv
     ```

---

## 🛠️ How it works (for developers)

The workflow (`download.yml`) does the following:

```yaml
1. Downloads the file via curl
2. Checks file size (in MB)
3. If < 90MB → saves with original filename
4. If ≥ 90MB → splits into 90MB chunks using `split -b 90M`
5. Commits and pushes everything back to the repository
