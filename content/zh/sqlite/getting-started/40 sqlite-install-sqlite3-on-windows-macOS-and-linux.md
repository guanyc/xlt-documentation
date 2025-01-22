---
# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: false
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams:
  enable: false
  options: ""

title: "Install Sqlite3 on Windows MacOS and Linux"
date: "2024-12-15 20:49:48+08:00"
lastmod: "2024-12-15 20:49:48+08:00"
draft: false

keywords: ["sqlite3"]
tags: ["sqlite3"]
categories: [tech]
author: "guanyc"
aliases: []

description: ""
summary:

featured_image:
weight: 40
type: docs
---

### **Installing SQLite3 on Windows, macOS, and Linux, and check your installation**

**James:** David, I’m excited to get started! How do I install SQLite3 on my computer?

**David:** That depends on your operating system, James. SQLite3 is pretty straightforward to install on Windows, macOS, and Linux. Let’s go through them one by one.

---

**Windows**

**David:** On Windows, you’ll need to download the SQLite binaries.
1. Go to the [SQLite Downloads page](https://www.sqlite.org/download.html).
2. Under the “Precompiled Binaries for Windows” section, download the ZIP archive for the SQLite tools.
3. Extract the ZIP file to a folder on your computer, like `C:\sqlite`.
4. Add the folder to your PATH environment variable so you can run SQLite from any command prompt.

**James:** What’s the PATH environment variable?

**David:** It tells your system where to look for executable files. By adding the SQLite folder to PATH, you can type `sqlite3` in the Command Prompt and it’ll work from any location.

**James:** How do I add it to PATH?

**David:**
1. Open **Control Panel** > **System** > **Advanced system settings**.
2. Click **Environment Variables**.
3. Find the `Path` variable in the system variables, and edit it.
4. Add `C:\sqlite` to the list and save.

**James:** Got it. Is there a way to confirm it’s installed?

**David:** Yes! Open Command Prompt and type `sqlite3`. If it’s installed correctly, you’ll see the SQLite3 prompt.

---

**macOS**

**David:** For macOS, SQLite is often pre-installed. Open the Terminal and type:
```bash
sqlite3
```
If you see the SQLite3 prompt, you’re all set.

**James:** What if it’s not installed?

**David:** You can install it using **Homebrew**. If you don’t have Homebrew installed, first install it by running:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Then, install SQLite by running:
```bash
brew install sqlite
```

**James:** That’s simple enough!

---

**Linux**

**David:** On most Linux distributions, SQLite is available in the package manager. For example:
- On Ubuntu or Debian:
  ```bash
  sudo apt update
  sudo apt install sqlite3
  ```

- On Fedora:
  ```bash
  sudo dnf install sqlite
  ```

**James:** That looks easy. How do I verify the installation?

**David:** Just type `sqlite3` in the terminal. If it’s installed, you’ll see the SQLite prompt.

---

**James:** That’s awesome! Seems like it’s easy to get started regardless of the OS.

**David:** Absolutely, James! Once you have SQLite installed, we can start creating your first database. That’s where the fun begins.

**James:** I’m ready for the next step!

**David:** Great! Let’s meet next time to create your first SQLite database and table.

---

### **Main Takeaways:**
1. **Windows Installation:** Download precompiled binaries, extract them, and add the folder to your PATH environment variable.
2. **macOS Installation:** SQLite is often pre-installed, but you can use Homebrew to install it if needed.
3. **Linux Installation:** Install via the package manager, like `apt` for Ubuntu or `dnf` for Fedora.
4. **Verification:** Confirm the installation by typing `sqlite3` in the command line or terminal.
5. **Next Steps:** After installation, you’re ready to create your first database and table!
