# Getting the course materials with Git

**English** · [Українська](GIT_GUIDE.uk.md) · [← back to README](README.md)

This guide takes you from "Git isn't installed" to "I have the latest lecture materials", step by step.
You do the setup **once**; after that, getting new materials before each lecture is a single command.

- [Part 1. Install Git](#part-1-install-git)
- [Part 2. Download the repository (clone)](#part-2-download-the-repository-clone)
- [Part 3. Get the latest changes before each lecture (pull)](#part-3-get-the-latest-changes-before-each-lecture-pull)
- [Part 4. Where to keep your own code](#part-4-where-to-keep-your-own-code)
- [Part 5. Authentication: HTTPS or SSH](#part-5-authentication-https-or-ssh)
- [Part 6. When something goes wrong](#part-6-when-something-goes-wrong)
- [Cheat sheet](#cheat-sheet)

> **How to read the commands.** Text in a grey block is a command: type it (or paste it) into the
> terminal and press <kbd>Enter</kbd>. Don't type the `$` at the start of a line if you see one — it only
> marks where the command begins. Everything after `#` is a comment for you, not part of the command.

> **Where is the terminal?**
> - **VS Code** (works on every system): menu **Terminal → New Terminal**.
> - **Windows:** after installing Git you also get **Git Bash** (Start menu → "Git Bash"). PowerShell works too.
> - **macOS:** **Terminal** app (<kbd>Cmd</kbd>+<kbd>Space</kbd>, type "Terminal").
> - **Linux:** <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd> on most distributions.

---

## Part 1. Install Git

1. Check whether Git is already installed:

   ```bash
   git --version
   ```

   If you see something like `git version 2.47.1`, Git is installed: go to [Part 2](#part-2-download-the-repository-clone).
   If you see `command not found` or `'git' is not recognized`, install it:

2. Install Git for your system:

   | System      | How to install                                                                                                                                                                                                                      |
   | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
   | **Windows** | Download the installer from [git-scm.com/downloads/win](https://git-scm.com/downloads/win) and run it. The default options are fine — just keep clicking **Next**. This also installs **Git Bash** and **Git Credential Manager** (used in [Part 5](#part-5-authentication-https-or-ssh)). |
   | **macOS**   | Run `git --version` in Terminal. If Git is missing, macOS offers to install the **Command Line Tools** — click **Install** and wait. Alternatively, with [Homebrew](https://brew.sh): `brew install git`.                                          |
   | **Linux**   | Ubuntu / Debian: `sudo apt update && sudo apt install git`. Fedora: `sudo dnf install git`.                                                                                                                                         |

3. **Close the terminal and open a new one**, then run `git --version` again. You should now see a version number.

4. *(Optional, needed only when you start making your own commits.)* Tell Git who you are:

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

   Use the same email as your GitHub account.

---

## Part 2. Download the repository (clone)

"Cloning" means downloading the whole repository to your computer **together with its history**, so that
later Git can fetch only what changed.

1. Open a terminal and go to the folder where you keep your study materials. For example, `Documents`:

   ```bash
   cd ~/Documents
   ```

   On Windows in PowerShell this is the same command: `cd ~/Documents`.

2. Clone the repository:

   ```bash
   git clone https://github.com/OlegAndrus12/PythonCoreI5.git
   ```

   This repository is public, so **no login or password is needed** to clone or update it.
   You should see lines like `Cloning into 'PythonCoreI5'...` and `Receiving objects: 100%`.

   > Already set up SSH (see [Part 5](#option-b-ssh))? Then you can clone with
   > `git clone git@github.com:OlegAndrus12/PythonCoreI5.git` instead. Both give you the same files.

3. Go into the new folder and check that everything is there:

   ```bash
   cd PythonCoreI5
   git status
   ```

   Expected output:

   ```text
   On branch main
   Your branch is up to date with 'origin/main'.

   nothing to commit, working tree clean
   ```

4. Open the folder in VS Code: **File → Open Folder…** and choose `PythonCoreI5`.
   (If you have the `code` command set up, `code .` from inside the folder does the same.)

> ⚠️ Run `git clone` **only once**. If you run it again in the same place, Git will say
> `destination path 'PythonCoreI5' already exists`. To get new materials, use `git pull` (Part 3).

---

## Part 3. Get the latest changes before each lecture (pull)

New modules and fixes are added as the course goes on. **Before each lecture**, do this:

1. Open a terminal **inside the course folder**. In VS Code with the `PythonCoreI5` folder open,
   **Terminal → New Terminal** already opens in the right place. Otherwise:

   ```bash
   cd ~/Documents/PythonCoreI5
   ```

2. Download the changes:

   ```bash
   git pull
   ```

3. Check the result:

   - `Already up to date.` — you already have everything; nothing new was published yet.
   - A list of files with `+` and `-` signs, ending with something like `3 files changed, 120 insertions(+)` —
     the new materials are now on your computer.
   - Anything else (an `error:` or `fatal:` line) — see [Part 6](#part-6-when-something-goes-wrong).

That's it. You never need to clone again.

---

## Part 4. Where to keep your own code

`git pull` can only update files cleanly if you **haven't edited the course files**. If you change, say,
`module01/strings/basics.py` and then the teacher updates the same file, `git pull` will stop with an error
(how to fix it: [Part 6](#your-local-changes-to-the-following-files-would-be-overwritten-by-merge)).

To avoid this completely:

- **Keep your exercises in a separate folder outside the course folder**, for example
  `~/Documents/python-practice`.
- Want to experiment with a course script? **Copy it** into your own folder first and change the copy.
- Opening and running course files is always safe — only *editing and saving* them causes conflicts.

---

## Part 5. Authentication: HTTPS or SSH

GitHub has two ways to connect: **HTTPS** (addresses that start with `https://`) and **SSH** (addresses that
start with `git@github.com:`).

**For this course you need neither login nor setup**: the repository is public, and cloning and pulling
over HTTPS work without signing in. Authentication becomes necessary when you **push** (upload) code to
your own repositories — for homework, for example — or work with a private repository.

| | HTTPS | SSH |
| --- | --- | --- |
| Clone and pull this course | ✅ no setup at all | needs a one-time key setup |
| Push to your own repositories | sign in through the browser or with a token | works automatically once the key is added |
| Good choice if… | you are just starting | you will push often, or HTTPS is blocked on your network |

> GitHub **does not accept your account password** in the terminal (since August 2021). If Git asks for a
> password and your GitHub password doesn't work, that is expected — use one of the methods below.

### Option A. HTTPS

#### A1. Git Credential Manager (recommended: sign in through the browser)

- **Windows:** already installed together with Git for Windows. Nothing to do.
- **macOS:** install it with Homebrew: `brew install --cask git-credential-manager`.
- **Linux:** see the [installation instructions](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/install.md).

The first time Git needs to sign in (for example, on your first `git push`), a browser window opens with
GitHub. Sign in, click **Authorize**, and return to the terminal. Git remembers this, so you sign in once
per computer.

#### A2. Personal access token (if a browser window can't open)

A token is a long generated password that you use in the terminal instead of your GitHub password.

1. On GitHub: click your avatar (top right) → **Settings** → **Developer settings** (at the bottom of the
   left menu) → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**.
2. Fill in the form:
   - **Token name:** anything, e.g. `laptop`.
   - **Expiration:** e.g. 90 days.
   - **Repository access:** **Only select repositories** → choose the repositories you will push to.
   - **Permissions → Repository permissions → Contents:** **Read and write**.
3. Click **Generate token** and **copy it right away** — GitHub shows it only once.
4. When Git asks:
   - `Username:` — your GitHub username;
   - `Password:` — paste the **token** (the characters don't appear while you type or paste; that's normal) and press <kbd>Enter</kbd>.

> 🔒 Treat the token like a password: don't share it, don't post it in chats, don't commit it into code.
> If it leaks, delete it on the same GitHub page and create a new one.

### Option B. SSH

With SSH, your computer proves who it is with a **key pair**: a *private key*, which never leaves your
computer, and a *public key*, which you give to GitHub. You set it up once per computer.

The commands below work in **Git Bash** (Windows), **Terminal** (macOS) and Linux terminals.

1. **Check whether you already have a key:**

   ```bash
   ls ~/.ssh
   ```

   If you see `id_ed25519` and `id_ed25519.pub`, you already have a key: skip to step 3.
   If you see `No such file or directory` or no `id_ed25519` files, continue with step 2.

2. **Create a key** (use your GitHub email):

   ```bash
   ssh-keygen -t ed25519 -C "you@example.com"
   ```

   - `Enter file in which to save the key` — just press <kbd>Enter</kbd> (keeps the default location).
   - `Enter passphrase` — type a passphrase that protects the key, or press <kbd>Enter</kbd> for none.
     Characters don't appear while you type; that's normal. Repeat it when asked.

3. **Copy the public key** (the file ending in **`.pub`**):

   | System | Command |
   | --- | --- |
   | Windows (Git Bash) | `cat ~/.ssh/id_ed25519.pub \| clip` |
   | macOS | `pbcopy < ~/.ssh/id_ed25519.pub` |
   | Linux | `cat ~/.ssh/id_ed25519.pub` — then select the printed line and copy it |

   The key is one line that starts with `ssh-ed25519` and ends with your email.

   > 🔒 Only ever share the **`.pub`** file. The file without `.pub` is your private key — never send it to anyone.

4. **Add the key to GitHub:** click your avatar → **Settings** → **SSH and GPG keys** → **New SSH key**.
   - **Title:** a name for this computer, e.g. `My laptop`.
   - **Key type:** **Authentication Key**.
   - **Key:** paste the line you copied.
   - Click **Add SSH key**.

5. **Test the connection:**

   ```bash
   ssh -T git@github.com
   ```

   The first time, you will see:

   ```text
   The authenticity of host 'github.com (140.82.xxx.xxx)' can't be established.
   ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
   Are you sure you want to continue connecting (yes/no/[fingerprint])?
   ```

   Check that the fingerprint matches the one in
   [GitHub's SSH key fingerprints](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints),
   then type `yes` and press <kbd>Enter</kbd>. Success looks like this:

   ```text
   Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
   ```

   Despite the wording, that **is** success.

6. **Use SSH addresses.** To clone: `git clone git@github.com:OlegAndrus12/PythonCoreI5.git`.
   Already cloned over HTTPS? Switch the existing folder to SSH (run inside the course folder):

   ```bash
   git remote set-url origin git@github.com:OlegAndrus12/PythonCoreI5.git
   git remote -v
   ```

   Both lines printed by `git remote -v` should now start with `git@github.com:`.

7. *(Only if you set a passphrase and don't want to type it every time.)* Let the SSH agent remember it:

   - **macOS:** create or open the file `~/.ssh/config` and add:

     ```text
     Host github.com
       AddKeysToAgent yes
       UseKeychain yes
       IdentityFile ~/.ssh/id_ed25519
     ```

     then run `ssh-add --apple-use-keychain ~/.ssh/id_ed25519` once.
   - **Windows (Git Bash) and Linux**, once per terminal session:

     ```bash
     eval "$(ssh-agent -s)"
     ssh-add ~/.ssh/id_ed25519
     ```

---

## Part 6. When something goes wrong

Read the **last lines** of the message Git prints: they usually say exactly what is wrong.

### `fatal: not a git repository (or any of the parent directories): .git`

You are not inside the course folder. Go there and repeat the command:

```bash
cd ~/Documents/PythonCoreI5
git pull
```

### `fatal: destination path 'PythonCoreI5' already exists and is not an empty directory`

You already cloned the course. You don't need to clone again: go into the folder and run `git pull`.

### `Your local changes to the following files would be overwritten by merge`

You edited course files, and the teacher changed the same files. Git lists them under the message.
Choose **one** option:

- **Keep your changes** — put them aside, update, then bring them back:

  ```bash
  git stash
  git pull
  git stash pop
  ```

  If `git stash pop` reports a `CONFLICT`, open the listed file in VS Code: it highlights both versions and
  offers **Accept Current / Accept Incoming / Accept Both** buttons. Pick what you need, save the file.
  Your changes are still kept in the stash, so after resolving, remove that copy with `git stash drop`.

- **Throw your changes away** and take the teacher's version:

  ```bash
  git restore .
  git pull
  ```

  ⚠️ This permanently deletes your edits in those files. Copy anything you need into your own folder first.

To avoid this next time, keep your own code outside the course folder ([Part 4](#part-4-where-to-keep-your-own-code)).

### `The following untracked working tree files would be overwritten by merge`

You created a file with the same name as a new file from the course. Rename or move your file (Git prints
its name), then run `git pull` again.

### `fatal: Need to specify how to reconcile divergent branches`

You made a **commit** inside the course folder, and the course has new commits too. Merge them:

```bash
git pull --no-rebase
```

If Git reports a `CONFLICT`, resolve it in VS Code as described above, save, then run `git add .` and
`git commit --no-edit`. Next time, commit your own work in your own folder or repository, not in the course folder.

### `Permission denied (publickey)`

SSH can't find a key that GitHub accepts. Check, in order:

1. You completed [Option B](#option-b-ssh) steps 2–4 on **this** computer.
2. `ssh -T git@github.com` prints `Hi your-username!` (step 5).
3. For this course you can always fall back to HTTPS:
   `git remote set-url origin https://github.com/OlegAndrus12/PythonCoreI5.git`.

### `Authentication failed` or `Support for password authentication was removed`

You entered your GitHub password. Use Git Credential Manager or a token instead
([Option A](#option-a-https)). Note that pulling *this* course never needs a password: if Git asks for one
here, check the address with `git remote -v` — it should be exactly
`https://github.com/OlegAndrus12/PythonCoreI5.git` (a typo in the address also makes GitHub ask you to log in).

### Nothing helps

Start fresh: copy anything of yours out of the course folder, delete the `PythonCoreI5` folder, and clone
again ([Part 2](#part-2-download-the-repository-clone)). Or bring the full error text to the lecture —
copy it as text, not as a photo of the screen.

---

## Cheat sheet

| What you want | Command |
| --- | --- |
| Check Git is installed | `git --version` |
| Download the course (once) | `git clone https://github.com/OlegAndrus12/PythonCoreI5.git` |
| Go into the course folder | `cd ~/Documents/PythonCoreI5` |
| Get the latest materials | `git pull` |
| See what you have changed | `git status` |
| Throw away your edits in course files | `git restore .` |
| Put your edits aside, update, bring them back | `git stash` → `git pull` → `git stash pop` |
| See the address the folder is connected to | `git remote -v` |
| Test SSH | `ssh -T git@github.com` |
