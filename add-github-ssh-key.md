# Creating and Using a GitHub SSH Key

- [Creating and Using a GitHub SSH Key](#creating-and-using-a-github-ssh-key)
    - [Purpose](#purpose)
    - [Step 1: Start the SSH Agent](#step-1-start-the-ssh-agent)
    - [Step 2: Add the Existing SSH Key to the Agent](#step-2-add-the-existing-ssh-key-to-the-agent)
    - [Step 3: Test the Connection to GitHub](#step-3-test-the-connection-to-github)
    - [Step 4: Clone a Repository Using SSH](#step-4-clone-a-repository-using-ssh)
    - [Step 5: Make Changes and Push to GitHub](#step-5-make-changes-and-push-to-github)
  - [Creating a New SSH Key (If Needed)](#creating-a-new-ssh-key-if-needed)
    - [Step 1: Navigate to the SSH Directory](#step-1-navigate-to-the-ssh-directory)
    - [Step 2: Generate a New SSH Key Pair](#step-2-generate-a-new-ssh-key-pair)
    - [Step 3: View the Public Key](#step-3-view-the-public-key)
    - [Commands used](#commands-used)
    - [To create a new key](#to-create-a-new-key)


### Purpose

SSH keys are used to securely authenticate with GitHub **without using a username and password every time**.
This is especially important for **CI/CD pipelines, Jenkins jobs, and automated deployments**, where manual login is not possible.

By setting up an SSH key:

* GitHub can trust your machine (or Jenkins server)
* Git operations become secure, automated, and reliable

---

### Step 1: Start the SSH Agent

The SSH agent manages your SSH keys in memory so you don’t need to re-enter passphrases repeatedly.

```bash
eval `ssh-agent -s`
```

**What this does:**
Starts the SSH agent in the background and prepares it to load keys.

---

### Step 2: Add the Existing SSH Key to the Agent

```bash
ssh-add sherin-github-key
```

**What this does:**
Registers your private SSH key with the agent so it can be used for authentication.

---

### Step 3: Test the Connection to GitHub

```bash
ssh -T git@github.com
```

**Expected result:**
A message confirming successful authentication.

**Why this matters:**
This confirms GitHub recognises your SSH key and trusts your machine.

---

### Step 4: Clone a Repository Using SSH

Navigate to your working directory:

```bash
cd ~/Documents/github
ls
```

Clone the repository using the SSH URL:

```bash
git clone git@github.com:sherinbinny/test-ssh2.git
```

**Why SSH instead of HTTPS:**

* No password prompts
* Required for Jenkins and automated pipelines
* More secure and industry standard

---

### Step 5: Make Changes and Push to GitHub

```bash
cd test-ssh2
ls
cat README.md
nano README.md
```

Stage and commit changes:

```bash
git add .
git commit -m "update readme"
```

Push changes to GitHub:

```bash
git push
```

**What this proves:**
Your SSH setup works end-to-end for cloning, committing, and pushing code.

---

## Creating a New SSH Key (If Needed)

This step is used when setting up a **new machine, Jenkins server, or EC2 instance**.

### Step 1: Navigate to the SSH Directory

```bash
cd /Users/sherinbinny/.ssh
```

---

### Step 2: Generate a New SSH Key Pair

```bash
ssh-keygen -t rsa -b 4096 -C "sherinbinny@gmail.com"
```

**Explanation:**

* `-t rsa` → RSA encryption type
* `-b 4096` → Strong encryption (industry best practice)
* `-C` → Label for identification in GitHub

This creates:

* **Private key** (kept secret)
* **Public key** (shared with GitHub)

---

### Step 3: View the Public Key

```bash
ls
cat sherin-jenkins-2-github-key.pub
```

**Next step (important):**

* Copy the public key
* Paste it into **GitHub → Settings → SSH and GPG Keys**

---

### Commands used

```
 1027  eval `ssh-agent -s`
 1028  ssh-add sherin-github-key
 1029  ssh -T git@github.com
 1030  cd
 1031  cd github
 1032  cd Documents/github
 1033  ls
 1034  git clone git@github.com:sherinbinny/test-ssh2.git
 1035  ls
 1036  cd test-ssh2
 1037  ls
 1038  cat README.md
 1039  nano README.md
 1040  git add .
 1041  git commit -m "update readme"
 1042  git push
```

### To create a new key

```
 1045  cd /Users/sherinbinny/.ssh
 1046  ssh-keygen -t rsa -b 4096 -C "sherinbinny@gmail.com"
 1047  ls
 1048  cat sherin-jenkins-2-github-key.pub
```
