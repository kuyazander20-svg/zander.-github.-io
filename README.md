my-programming-site/
├─ public/                # Front-end files (static)
│  ├─ index.html
│  ├─ style.css
│  └─ script.js
├─ server.js              # Back-end main file
├─ package.json           # Dependencies & config
└─ .env                   # Environment variables (secret)
# Initialize project (creates package.json)
npm init -y

# Install packages
npm install express cors dotenv
npm install --save-dev nodemon  # Auto-reload server during dev
// Load dependencies
const express = require('express');
const cors = require('cors');
require('dotenv').config();

// Initialize app
const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(cors()); // Allow cross-origin requests
app.use(express.json()); // Parse JSON data
app.use(express.urlencoded({ extended: true })); // Parse form data
app.use(express.static('public')); // Serve front-end files

// -------------------
// Data (Temporary — replace with database later)
// -------------------
let projects = [
  { id: 1, title: 'Calculator App', description: 'HTML/CSS/JS calculator', code: 'let result = num1 + num2;' },
  { id: 2, title: 'LAN Subnet Calculator', description: 'IP subnetting tool', code: 'subnetMask = 255.255.255.0;' }
];

// -------------------
// API Routes
// -------------------

// Home route — serve website
app.get('/', (req, res) => {
  res.sendFile(__dirname + '/public/index.html');
});

// GET all projects — API endpoint
app.get('/api/projects', (req, res) => {
  res.json({ success: true, data: projects });
});

// GET single project by ID
app.get('/api/projects/:id', (req, res) => {
  const project = projects.find(p => p.id === parseInt(req.params.id));
  if (!project) return res.status(404).json({ success: false, message: 'Project not found' });
  res.json({ success: true, data: project });
});

// POST — add new project
app.post('/api/projects', (req, res) => {
  const newProject = {
    id: projects.length + 1,
    title: req.body.title,
    description: req.body.description,
    code: req.body.code
  };
  projects.push(newProject);
  res.status(201).json({ success: true, data: newProject });
});

// POST — contact form submission
app.post('/api/contact', (req, res) => {
  const { name, email, message } = req.body;
  console.log(`📩 New message from ${name} (${email}): ${message}`);
  res.json({ success: true, message: 'Message sent successfully!' });
});

// -------------------
// Start Server
// -------------------
app.listen(PORT, () => {
  console.log(`🚀 Server running at http://localhost:${PORT}`);
});
{
  "name": "my-programming-site",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.4.5",
    "express": "^4.21.0"
  },
  "devDependencies": {
    "nodemon": "^3.1.7"
  }
}
// Fetch projects from back-end
async function loadProjects() {
  try {
    const res = await fetch('/api/projects');
    const data = await res.json();
    if (data.success) {
      displayProjects(data.data);
    }
  } catch (err) {
    console.error('Error loading projects:', err);
  }
}

// Display projects on page
function displayProjects(projects) {
  const container = document.querySelector('.projects-container') || document.querySelector('#projects');
  container.innerHTML = '<h2>My Projects</h2>';
  projects.forEach(project => {
    container.innerHTML += `
      <div class="project-card">
        <h3>${project.title}</h3>
        <p>${project.description}</p>
        <code>${project.code}</code>
      </div>
    `;
  });
}

// Contact form submission
document.querySelector('#contact-form')?.addEventListener('submit', async (e) => {
  e.preventDefault();
  const formData = new FormData(e.target);
  const data = Object.fromEntries(formData);
  
  const res = await fetch('/api/contact', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data)
  });
  
  const result = await res.json();
  alert(result.message);
  e.target.reset();
});

// Load projects when page loads
document.addEventListener('DOMContentLoaded', loadProjects);

// Keep your existing dark mode & smooth scroll code below
<section id="contact" class="section">
  <h2>Contact Me</h2>
  <form id="contact-form" class="contact-form">
    <input type="text" name="name" placeholder="Your Name" required>
    <input type="email" name="email" placeholder="Your Email" required>
    <textarea name="message" placeholder="Your Message" required></textarea>
    <button type="submit">Send Message</button>
  </form>
</section>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Code Playground | Run Your Code</title>
    <link rel="stylesheet" href="style.css">
    <!-- Optional: Code highlighting -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/atom-one-dark.min.css">
</head>
<body>
    <!-- Navbar -->
    <nav class="navbar">
        <h1 class="logo">💻 Code Playground</h1>
        <ul class="nav-links">
            <li><a href="#editor">Code Editor</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#tutorials">Tutorials</a></li>
        </ul>
    </nav>

    <!-- Hero -->
    <section class="hero">
        <h2>Write & Run Code Instantly</h2>
        <p>Type your HTML, CSS, or JavaScript — click Run — see results live!</p>
    </section>

    <!-- Code Editor & Runner -->
    <section id="editor" class="section editor-section">
        <h2>📝 Code Editor</h2>
        
        <div class="editor-grid">
            <!-- Input Panels -->
            <div class="code-inputs">
                <!-- HTML -->
                <div class="code-panel">
                    <div class="panel-header">HTML</div>
                    <textarea id="htmlCode" placeholder="Write HTML here...">
<!DOCTYPE html>
<html>
<body>
    <h1>Hello World!</h1>
    <p>My first code run 🎉</p>
    <button onclick="greet()">Click Me</button>
</body>
</html>
                    </textarea>
                </div>

                <!-- CSS -->
                <div class="code-panel">
                    <div class="panel-header">CSS</div>
                    <textarea id="cssCode" placeholder="Write CSS here...">
body {
    font-family: Arial;
    padding: 20px;
    background: #f0f8ff;
}
h1 { color: #007bff; }
button {
    padding: 10px 20px;
    background: #28a745;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
                    </textarea>
                </div>

                <!-- JavaScript -->
                <div class="code-panel">
                    <div class="panel-header">JavaScript</div>
                    <textarea id="jsCode" placeholder="Write JavaScript here...">
function greet() {
    alert('Hello from JavaScript! 🚀');
}
                    </textarea>
                </div>
            </div>

            <!-- Output Panel -->
            <div class="output-panel">
                <div class="panel-header">
                    Output
                    <button id="runBtn" class="run-btn">▶ Run Code</button>
                    <button id="clearBtn" class="clear-btn">🗑 Clear</button>
                </div>
                <iframe id="outputFrame" class="output-frame" title="Code Output"></iframe>
            </div>
        </div>

        <!-- Console Log -->
        <div class="console-panel">
            <div class="panel-header">Console Log</div>
            <div id="consoleOutput" class="console-output"></div>
        </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="section">
        <h2>My Projects</h2>
        <div id="projectsContainer" class="projects-grid">
            <!-- Loaded from back-end -->
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <p>© 2026 Code Playground | Built with ❤️ & code</p>
    </footer>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>
    <script src="code-runner.js"></script>
    <script src="script.js"></script>
</body>
</html>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', sans-serif;
}

:root {
    --bg: #0f172a;
    --card: #1e293b;
    --text: #e2e8f0;
    --accent: #3b82f6;
    --success: #10b981;
    --warning: #f59e0b;
    --danger: #ef4444;
}

body {
    background: var(--bg);
    color: var(--text);
    line-height: 1.6;
}

/* Navbar */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 5%;
    background: var(--card);
    border-bottom: 1px solid #334155;
}

.nav-links {
    list-style: none;
    display: flex;
    gap: 2rem;
}

.nav-links a {
    color: var(--text);
    text-decoration: none;
    transition: color 0.2s;
}

.nav-links a:hover {
    color: var(--accent);
}

/* Hero */
.hero {
    text-align: center;
    padding: 3rem 5%;
    background: linear-gradient(135deg, var(--accent), #8b5cf6);
}

.hero h2 { font-size: 2.2rem; margin-bottom: 0.5rem; }
.hero p { font-size: 1.1rem; opacity: 0.9; }

/* Sections */
.section {
    padding: 2rem 5%;
    max-width: 1400px;
    margin: 0 auto;
}

.section h2 {
    font-size: 1.8rem;
    margin-bottom: 1.5rem;
    color: var(--accent);
}

/* Editor Grid */
.editor-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
}

.code-inputs {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.code-panel {
    background: var(--card);
    border-radius: 8px;
    overflow: hidden;
    border: 1px solid #334155;
}

.panel-header {
    background: #334155;
    padding: 0.5rem 1rem;
    font-weight: 600;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

textarea {
    width: 100%;
    height: 150px;
    background: #1e293b;
    color: #e2e8f0;
    border: none;
    padding: 1rem;
    font-family: 'Courier New', monospace;
    font-size: 14px;
    resize: vertical;
    outline: none;
}

.output-panel {
    background: var(--card);
    border-radius: 8px;
    overflow: hidden;
    border: 1px solid #334155;
    display: flex;
    flex-direction: column;
    height: 100%;
}

.output-frame {
    flex: 1;
    min-height: 450px;
    background: white;
    border: none;
}

/* Buttons */
.run-btn {
    background: var(--success);
    color: white;
    border: none;
    padding: 0.4rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    font-weight: 600;
    transition: background 0.2s;
}

.run-btn:hover { background: #059669; }
.clear-btn {
    background: var(--danger);
    color: white;
    border: none;
    padding: 0.4rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    margin-left: 0.5rem;
}

/* Console */
.console-panel {
    margin-top: 1rem;
    background: var(--card);
    border-radius: 8px;
    border: 1px solid #334155;
    overflow: hidden;
}

.console-output {
    padding: 1rem;
    height: 120px;
    overflow-y: auto;
    background: #0f172a;
    font-family: monospace;
    font-size: 13px;
}

.log-log { color: #94a3b8; }
.log-error { color: var(--danger); }
.log-warn { color: var(--warning); }

/* Projects Grid */
.projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1rem;
}

.project-card {
    background: var(--card);
    padding: 1.5rem;
    border-radius: 8px;
    border: 1px solid #334155;
    transition: transform 0.2s;
}

.project-card:hover { transform: translateY(-3px); }
.project-card h3 { color: var(--accent); margin-bottom: 0.5rem; }

/* Footer */
footer {
    text-align: center;
    padding: 2rem;
    background: var(--card);
    border-top: 1px solid #334155;
    margin-top: 2rem;
}

/* Responsive */
@media (max-width: 900px) {
    .editor-grid { grid-template-columns: 1fr; }
    .nav-links { gap: 1rem; }
}
// Code Runner — executes HTML/CSS/JS in sandboxed iframe
class CodeRunner {
    constructor() {
        this.htmlInput = document.getElementById('htmlCode');
        this.cssInput = document.getElementById('cssCode');
        this.jsInput = document.getElementById('jsCode');
        this.outputFrame = document.getElementById('outputFrame');
        this.consoleOutput = document.getElementById('consoleOutput');
        this.runBtn = document.getElementById('runBtn');
        this.clearBtn = document.getElementById('clearBtn');
        
        this.init();
    }

    init() {
        // Run on button click
        this.runBtn.addEventListener('click', () => this.runCode());
        
        // Auto-run on Ctrl+Enter
        document.addEventListener('keydown', (e) => {
            if (e.ctrlKey && e.key === 'Enter') {
                e.preventDefault();
                this.runCode();
            }
        });

        // Clear console
        this.clearBtn.addEventListener('click', () => {
            this.consoleOutput.innerHTML = '';
            this.htmlInput.value = '';
            this.cssInput.value = '';
            this.jsInput.value = '';
        });

        // Initial run
        setTimeout(() => this.runCode(), 500);
    }

    // Capture console.log from iframe
    captureConsole() {
        return `
            <script>
                const originalLog = console.log;
                const originalError = console.error;
                const originalWarn = console.warn;
                
                console.log = function(...args) {
                    window.parent.postMessage({
                        type: 'console',
                        method: 'log',
                        message: args.map(a => typeof a === 'object' ? JSON.stringify(a) : a).join(' ')
                    }, '*');
                    originalLog.apply(console, args);
                };
                
                console.error = function(...args) {
                    window.parent.postMessage({
                        type: 'console',
                        method: 'error',
                        message: args.map(a => typeof a === 'object' ? JSON.stringify(a) : a).join(' ')
                    }, '*');
                    originalError.apply(console, args);
                };
                
                console.warn = function(...args) {
                    window.parent.postMessage({
                        type: 'console',
                        method: 'warn',
                        message: args.map(a => typeof a === 'object' ? JSON.stringify(a) : a).join(' ')
                    }, '*');
                    originalWarn.apply(console, args);
                };

                // Catch runtime errors
                window.onerror = function(msg, src, line, col, err) {
                    window.parent.postMessage({
                        type: 'console',
                        method: 'error',
                        message: msg + ' (line ' + line + ')'
                    }, '*');
                    return true;
                };
            <\/script>
        `;
    }

    runCode() {
        const html = this.htmlInput.value;
        const css = this.cssInput.value;
        const js = this.jsInput.value;

        // Build full document
        const fullCode = `
            <!DOCTYPE html>
            <html>
            <head>
                <meta charset="UTF-8">
                <style>${css}</style>
            </head>
            <body>
                ${html.replace(/<\/?html>|<\/?head>|<\/?body>/gi, '')}
                ${this.captureConsole()}
                <script>${js}<\/script>
            </body>
            </html>
        `;

        // Write to iframe
        this.outputFrame.srcdoc = fullCode;
        
        // Clear old console & log run time
        this.log('system', 'Code executed at ' + new Date().toLocaleTimeString());
    }

    log(method, message) {
        const div = document.createElement('div');
        div.className = `log-${method}`;
        div.textContent = `[${method.toUpperCase()}] ${message}`;
        this.consoleOutput.appendChild(div);
        this.consoleOutput.scrollTop = this.consoleOutput.scrollHeight;
    }
}

// Listen for messages from iframe
window.addEventListener('message', (event) => {
    if (event.data && event.data.type === 'console') {
        const runner = window.codeRunner;
        if (runner) runner.log(event.data.method, event.data.message);
    }
});

// Initialize when page loads
document.addEventListener('DOMContentLoaded', () => {
    window.codeRunner = new CodeRunner();
});
// Load projects from back-end
async function loadProjects() {
    try {
        const res = await fetch('/api/projects');
        const data = await res.json();
        if (data.success) {
            displayProjects(data.data);
        }
    } catch (err) {
        console.error('Error:', err);
    }
}

function displayProjects(projects) {
    const container = document.getElementById('projectsContainer');
    container.innerHTML = '';
    projects.forEach(p => {
        container.innerHTML += `
            <div class="project-card">
                <h3>${p.title}</h3>
                <p>${p.description}</p>
                <pre><code>${p.code}</code></pre>
            </div>
        `;
    });
}

// Dark mode toggle (optional)
document.addEventListener('DOMContentLoaded', () => {
    loadProjects();
    // Highlight code blocks
    document.querySelectorAll('pre code').forEach(block => {
        hljs.highlightElement(block);
    });
});
const express = require('express');
const cors = require('cors');
const mongoose = require('mongoose');
require('dotenv').config();

const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(cors());
app.use(express.json());
app.use(express.static('public'));

// MongoDB Connection
const MONGODB_URI = process.env.MONGODB_URI || 'mongodb://localhost:27017/code_website';
mongoose.connect(MONGODB_URI)
  .then(() => console.log('✅ Connected to MongoDB'))
  .catch(err => console.error('❌ DB Error:', err));

// Project Model
const projectSchema = new mongoose.Schema({
    title: String,
    description: String,
    code: String
});
const Project = mongoose.model('Project', projectSchema);

// API Routes
app.get('/api/projects', async (req, res) => {
    const projects = await Project.find();
    res.json({ success: true, data: projects });
});

app.post('/api/projects', async (req, res) => {
    const project = new Project(req.body);
    await project.save();
    res.json({ success: true, data: project });
});

// Start Server
app.listen(PORT, () => {
    console.log(`🚀 Website running at http://localhost:${PORT}`);
});
npm init -y
npm install express cors mongoose dotenv
npm install --save-dev nodemon
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js"
}
npm run dev
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();

const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(cors());
app.use(express.json());
app.use(express.static('public'));

// -------------------
// DATABASE CONNECTION
// -------------------
const MONGODB_URI = process.env.MONGODB_URI || 'mongodb://localhost:27017/code_website';

mongoose.connect(MONGODB_URI)
  .then(() => console.log('✅ Connected to MongoDB Database'))
  .catch(err => console.error('❌ MongoDB Connection Error:', err));
// -------------------
// DATABASE MODELS
// -------------------

// Model 1: Projects
const projectSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true,
    trim: true
  },
  description: {
    type: String,
    required: true
  },
  code: {
    type: String,
    required: true
  },
  language: {
    type: String,
    default: 'JavaScript'
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});
const Project = mongoose.model('Project', projectSchema);

// Model 2: Code Snippets (for your code runner)
const snippetSchema = new mongoose.Schema({
  name: { type: String, required: true },
  html: String,
  css: String,
  js: String,
  author: { type: String, default: 'Anonymous' },
  createdAt: { type: Date, default: Date.now }
});
const Snippet = mongoose.model('Snippet', snippetSchema);

// Model 3: Users (optional — for login system)
const userSchema = new mongoose.Schema({
  username: { type: String, required: true, unique: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  joinedAt: { type: Date, default: Date.now }
});
const User = mongoose.model('User', userSchema);
// -------------------
// PROJECTS API
// -------------------

// CREATE: Add new project
app.post('/api/projects', async (req, res) => {
  try {
    const project = new Project(req.body);
    await project.save();
    res.status(201).json({ success: true, data: project });
  } catch (err) {
    res.status(400).json({ success: false, error: err.message });
  }
});

// READ: Get all projects
app.get('/api/projects', async (req, res) => {
  try {
    const projects = await Project.find().sort({ createdAt: -1 }); // Newest first
    res.json({ success: true, count: projects.length, data: projects });
  } catch (err) {
    res.status(500).json({ success: false, error: err.message });
  }
});

// READ: Get single project by ID
app.get('/api/projects/:id', async (req, res) => {
  try {
    const project = await Project.findById(req.params.id);
    if (!project) return res.status(404).json({ success: false, message: 'Project not found' });
    res.json({ success: true, data: project });
  } catch (err) {
    res.status(500).json({ success: false, error: err.message });
  }
});

// UPDATE: Edit project
app.put('/api/projects/:id', async (req, res) => {
  try {
    const project = await Project.findByIdAndUpdate(
      req.params.id,
      req.body,
      { new: true, runValidators: true } // Return updated data
    );
    if (!project) return res.status(404).json({ success: false, message: 'Project not found' });
    res.json({ success: true, data: project });
  } catch (err) {
    res.status(400).json({ success: false, error: err.message });
  }
});

// DELETE: Remove project
app.delete('/api/projects/:id', async (req, res) => {
  try {
    const project = await Project.findByIdAndDelete(req.params.id);
    if (!project) return res.status(404).json({ success: false, message: 'Project not found' });
    res.json({ success: true, message: 'Project deleted successfully' });
  } catch (err) {
    res.status(500).json({ success: false, error: err.message });
  }
});

// -------------------
// SNIPPETS API (Save code from your code runner)
// -------------------

// Save new code snippet
app.post('/api/snippets', async (req, res) => {
  try {
    const snippet = new Snippet(req.body);
    await snippet.save();
    res.status(201).json({ success: true, data: snippet });
  } catch (err) {
    res.status(400).json({ success: false, error: err.message });
  }
});

// Get all saved snippets
app.get('/api/snippets', async (req, res) => {
  try {
    const snippets = await Snippet.find().sort({ createdAt: -1 });
    res.json({ success: true, count: snippets.length, data: snippets });
  } catch (err) {
    res.status(500).json({ success: false, error: err.message });
  }
});

// Start Server
app.listen(PORT, () => {
  console.log(`🚀 Server running at http://localhost:${PORT}`);
});
PORT=3000
# Local MongoDB
MONGODB_URI=mongodb://localhost:27017/code_website
# OR MongoDB Atlas (cloud):
# MONGODB_URI=mongodb+srv://username:password@cluster0.abc123.mongodb.net/code_website
const mysql = require('mysql2/promise');

// Create connection pool
const db = mysql.createPool({
  host: 'localhost',
  user: 'root',
  password: 'your_mysql_password',
  database: 'code_website',
  waitForConnections: true,
  connectionLimit: 10
});

// Test connection
async function testDB() {
  try {
    const connection = await db.getConnection();
    console.log('✅ Connected to MySQL Database');
    connection.release();
  } catch (err) {
    console.error('❌ MySQL Connection Error:', err);
  }
}
testDB();

// Example: Get all projects
app.get('/api/projects', async (req, res) => {
  try {
    const [rows] = await db.query('SELECT * FROM projects ORDER BY created_at DESC');
    res.json({ success: true, data: rows });
  } catch (err) {
    res.status(500).json({ success: false, error: err.message });
  }
});
CREATE DATABASE IF NOT EXISTS code_website;
USE code_website;

CREATE TABLE IF NOT EXISTS projects (
  id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT NOT NULL,
  code TEXT NOT NULL,
  language VARCHAR(50) DEFAULT 'JavaScript',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
// Save Project to Database
async function saveProject(projectData) {
  try {
    const res = await fetch('/api/projects', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(projectData)
    });
    const data = await res.json();
    if (data.success) {
      alert('✅ Project saved to database!');
      loadProjects(); // Refresh list
    }
  } catch (err) {
    console.error('Error:', err);
  }
}

// Load Projects from Database
async function loadProjects() {
  try {
    const res = await fetch('/api/projects');
    const data = await res.json();
    if (data.success) {
      displayProjects(data.data);
    }
  } catch (err) {
    console.error('Error loading projects:', err);
  }
}

// Save Code Snippet from Code Runner
async function saveSnippet() {
  const snippet = {
    name: prompt('Enter snippet name:'),
    html: document.getElementById('htmlCode').value,
    css: document.getElementById('cssCode').value,
    js: document.getElementById('jsCode').value
  };

  const res = await fetch('/api/snippets', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(snippet)
  });
  const data = await res.json();
  if (data.success) alert('✅ Snippet saved!');
}

// Display Projects
function displayProjects(projects) {
  const container = document.getElementById('projectsContainer');
  container.innerHTML = '';
  projects.forEach(p => {
    container.innerHTML += `
      <div class="project-card">
        <h3>${p.title}</h3>
        <p>${p.description}</p>
        <small>${new Date(p.createdAt).toLocaleDateString()}</small>
        <pre><code>${p.code}</code></pre>
        <button onclick="deleteProject('${p._id}')">Delete</button>
      </div>
    `;
  });
}

// Delete Project
async function deleteProject(id) {
  if (!confirm('Delete this project?')) return;
  await fetch(`/api/projects/${id}`, { method: 'DELETE' });
  loadProjects();
}

// Load on page start
document.addEventListener('DOMContentLoaded', loadProjects);
# Start MongoDB (if local)
mongod

# Run your website
npm run dev
Feature	Status
✅ MongoDB database connection	Done
✅ 3 Data Models (Projects, Snippets, Users)	Done
✅ Full CRUD API endpoints	Done
✅ Frontend ↔ Database integration	Done
✅ MySQL alternative option	Done
✅ Data persists after server restart	Done
✅ Auto timestamps for all entries	Done
