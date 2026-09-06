John Zander Guerrero website
├─ index.html      (Main content)
├─ style.css       (Design/styling)
└─ script.js       (Interactive features)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Programming Hub</title>
    <link rel="stylesheet" href="style.css"> <!-- Connect CSS -->
</head>
<body>
    <!-- Navigation Bar -->
    <nav class="navbar">
        <h1 class="logo">💻 My Code Hub</h1>
        <ul class="nav-links">
            <li><a href="#home">Home</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#tutorials">Tutorials</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
        <h2>Welcome to My Programming World</h2>
        <p>Sharing code, projects, and tech tutorials!</p>
        <button id="themeBtn">Toggle Dark Mode</button>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="section">
        <h2>My Projects</h2>
        <div class="project-card">
            <h3>Calculator App</h3>
            <p>A simple calculator built with HTML/CSS/JS.</p>
            <code>let result = num1 + num2;</code>
        </div>
        <div class="project-card">
            <h3>LAN Subnet Calculator</h3>
            <p>Network tool for IP subnetting.</p>
            <code>subnetMask = 255.255.255.0;</code>
        </div>
    </section>

    <!-- Tutorials Section -->
    <section id="tutorials" class="section">
        <h2>Code Tutorials</h2>
        <pre class="code-block">
// Hello World in JavaScript
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet("Coder"));
        </pre>
    </section>

    <!-- Footer -->
    <footer id="contact">
        <p>© 2026 My Programming Hub | Built with ❤️ and code</p>
    </footer>

    <script src="script.js"></script> <!-- Connect JavaScript -->
</body>
</html>
/* Global Styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Arial', sans-serif;
    transition: background 0.3s, color 0.3s;
}

:root {
    --bg-color: #f4f4f4;
    --text-color: #222;
    --card-bg: white;
    --accent: #007bff;
}

/* Dark Mode */
.dark-mode {
    --bg-color: #1a1a1a;
    --text-color: #f4f4f4;
    --card-bg: #2d2d2d;
}

body {
    background-color: var(--bg-color);
    color: var(--text-color);
    line-height: 1.6;
}

/* Navbar */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 5%;
    background: var(--accent);
    color: white;
}

.nav-links {
    list-style: none;
    display: flex;
    gap: 2rem;
}

.nav-links a {
    color: white;
    text-decoration: none;
    font-weight: 500;
}

.nav-links a:hover {
    color: #ffd700;
}

/* Sections */
.hero {
    text-align: center;
    padding: 4rem 5%;
}

.hero h2 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
}

.section {
    padding: 3rem 5%;
    max-width: 1200px;
    margin: 0 auto;
}

.section h2 {
    text-align: center;
    margin-bottom: 2rem;
    color: var(--accent);
}

/* Project Cards */
.project-card {
    background: var(--card-bg);
    padding: 1.5rem;
    margin-bottom: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

code {
    background: #eee;
    padding: 0.2rem 0.5rem;
    border-radius: 4px;
    font-family: monospace;
}

.dark-mode code {
    background: #444;
}

/* Code Block */
.code-block {
    background: var(--card-bg);
    padding: 1.5rem;
    border-radius: 8px;
    overflow-x: auto;
    font-family: 'Courier New', monospace;
    border-left: 4px solid var(--accent);
}

/* Button */
button {
    margin-top: 1rem;
    padding: 0.8rem 1.5rem;
    background: var(--accent);
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1rem;
}

button:hover {
    background: #0056b3;
}

/* Footer */
footer {
    text-align: center;
    padding: 2rem;
    background: var(--accent);
    color: white;
    margin-top: 2rem;
}

/* Responsive (Mobile Friendly) */
@media (max-width: 768px) {
    .navbar {
        flex-direction: column;
        gap: 1rem;
    }
    .nav-links {
        gap: 1rem;
    }
    .hero h2 {
        font-size: 1.8rem;
    }
}
// Dark Mode Toggle
const themeBtn = document.getElementById('themeBtn');
const body = document.body;

// Check saved theme
if (localStorage.getItem('darkMode') === 'enabled') {
    body.classList.add('dark-mode');
    themeBtn.textContent = 'Toggle Light Mode';
}

themeBtn.addEventListener('click', () => {
    body.classList.toggle('dark-mode');
    
    // Save preference
    if (body.classList.contains('dark-mode')) {
        localStorage.setItem('darkMode', 'enabled');
        themeBtn.textContent = 'Toggle Light Mode';
    } else {
        localStorage.setItem('darkMode', 'disabled');
        themeBtn.textContent = 'Toggle Dark Mode';
    }
});

// Smooth scroll for navigation links
document.querySelectorAll('.nav-links a').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const targetId = this.getAttribute('href');
        document.querySelector(targetId).scrollIntoView({
            behavior: 'smooth'
        });
    });
});

// Optional: Add current year to footer
const year = new Date().getFullYear();
document.querySelector('footer p').innerHTML = 
    `© ${year} My Programming Hub | Built with ❤️ and code`;
node -v   # Shows version (e.g., v20.x.x)
npm -v
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
    <section id="contact" class="section">
  <h2>Contact Me</h2>
  <form id="contact-form" class="contact-form">
    <input type="text" name="name" placeholder="Your Name" required>
    <input type="email" name="email" placeholder="Your Email" required>
    <textarea name="message" placeholder="Your Message" required></textarea>
    <button type="submit">Send Message</button>
  </form>
</section>
  </div>
    `
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
