# 🚀 Deploying a Next.js Project on cPanel

Next.js is typically deployed on hosting platforms like **Vercel** or **Netlify**, but you can also deploy it using **cPanel**.  
Below is the complete step-by-step process to deploy your Next.js app on a cPanel server.

---

#### 🧩 Step 1: Create `server.js` File

First, create a file named `server.js` in your project’s **root directory**.  
This file allows the Next.js app to run using a Node.js server.

```js
const { createServer } = require('http')
const { parse } = require('url')
const next = require('next')

const dev = process.env.NODE_ENV !== 'production'
const hostname = '0.0.0.0'
const port = 3000

const app = next({ dev, hostname, port })
const handle = app.getRequestHandler()

app.prepare().then(() => {
  createServer(async (req, res) => {
    try {
      const parsedUrl = parse(req.url, true)
      const { pathname, query } = parsedUrl

      if (pathname === '/a') {
        await app.render(req, res, '/a', query)
      } else if (pathname === '/b') {
        await app.render(req, res, '/b', query)
      } else {
        await handle(req, res, parsedUrl)
      }
    } catch (err) {
      console.error('Error occurred handling', req.url, err)
      res.statusCode = 500
      res.end('internal server error')
    }
  })
    .once('error', (err) => {
      console.error(err)
      process.exit(1)
    })
    .listen(port, () => {
      console.log(`> Ready on http://${hostname}:${port}`)
    })
})
```
---
#### ⚙️ Step 2: Build the Project
Run the following command in your terminal to build the Next.js project:
```bash
npm run build
```
This command will create a `.next` folder containing all the compiled files for production.
---
#### 🗜 Step 3: Zip the Project
Before zipping, exclude the `node_modules` folder, as it is typically large.
Create a ZIP file of your project without the `node_modules` directory.
---
#### 📤 Step 4: Upload Files to cPanel

- Log in to cPanel and open File Manager.
- Upload your ZIP file to the public_html directory (or your desired domain folder).
- Extract the ZIP file there
---

#### ⚡ Step 5: Set Up the Node.js Application

- Go to Setup Node.js App in cPanel.
- Click Create Application and fill in the following details:
  - **Application Root:** Path to your project directory
  - **Application URL:** Your domain name
  - **Application Startup File:** server.js
- Click Create Application to complete setup.
---

#### 🧠 Step 6: Install Dependencies & Restart Server

Once the application is created, cPanel will automatically detect your `package.json` file.
Click **Run NPM Install** to install all dependencies.
After installation, click **Restart** to start your Node.js server.

**✅ Result**
If all steps are completed correctly, your Next.js app will go live on your cPanel server successfully.

--- 

#### 📋 Summary

- Create `server.js` file
- Build the project
- Zip without `node_modules`
- Upload and extract in `public_html`
- Set up Node.js app
- Install dependencies and restart the server
