### 🚀 Deploying and Auto-Starting a Next.js Application on Ubuntu Server

This guide explains how to deploy your Next.js application on an Ubuntu server and configure it to start automatically on system boot using systemd.

---

#### 🧩 Prerequisites

Before you begin, ensure the following:

- ✅ You have **SSH access** to your Ubuntu server.  
- ✅ You have **Node.js** and **npm** (or **yarn**) installed.  
- ✅ You have uploaded your **Next.js project files** to:  
```bash
/var/www/myNextApp

```

**📦 Project Structure Example**
```lua
/var/www/myNextApp
│
├── package.json
├── next.config.js
├── node_modules/
├── .next/
└── server.js
```

---

#### ⚙️ Step 1: Install Node.js (if not already installed)

Check if Node.js is installed:

```bash
node -v
```
If not installed, install via NVM (recommended):
```bash
sudo apt update
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
source ~/.bashrc
nvm install --lts

```

Confirm installation:

```bash
node -v
npm -v
```

---

#### 📦 Step 2: Upload Your Next.js App to the Server

If using **Git**:

```bash
cd /var/www
sudo git clone https://github.com/username/myNextApp.git
```

---

---

#### 🏗️ Step 3: Install Dependencies and Build

Navigate to your app folder:

```bash
cd /var/www/myNextApp
```
Install dependencies:
```bash
npm install
```
Build your Next.js app:
```bash
Build your Next.js app:
```

---

#### 🚀 Step 4: Test the Application

Run the app manually to verify:

```bash
npm start
```
- By default, Next.js runs on port 3000.

You can test by visiting:
```bash
http://your-server-ip:3000
```

