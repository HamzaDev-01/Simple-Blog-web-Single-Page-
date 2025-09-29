# Simple-Blog-web-Single-Page-
View a list of blog posts.  Add new blog posts using a form.  Posts are stored temporarily in server memory (no database needed).  Clean and responsive design with basic styling.  Backend API to get posts and add new posts.  Simple and easy-to-understand code — perfect for beginners learning full-stack development.
# Simple Blog Application

A beginner-friendly **full-stack blog application** built with **Node.js** and **Express** for the backend, and simple **HTML, CSS, and JavaScript** for the frontend.

# Features

- View a list of blog posts.
- Add new blog posts via a form.
- Posts are stored temporarily in server memory (no database required).
- Clean and responsive design with basic styling.
- Backend API to get posts and add new posts.
- Simple code, ideal for beginners learning full-stack development.
# Getting Started

# Prerequisites

- [Node.js](https://nodejs.org/) installed on your machine.
# Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/simple-blog-app.git
# Front end (Done in HTML/CSS)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Simple Blog</title>
  <style>
    /* Reset some defaults */
    * {
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      max-width: 700px;
      margin: 40px auto;
      background: #f9fafb;
      color: #333;
      padding: 0 20px 40px;
      line-height: 1.6;
    }

    h1 {
      text-align: center;
      color: #2c3e50;
      margin-bottom: 30px;
      font-weight: 700;
      letter-spacing: 1.5px;
      text-transform: uppercase;
    }

    form {
      background: white;
      padding: 25px 30px;
      border-radius: 10px;
      box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
      margin-bottom: 40px;
      transition: box-shadow 0.3s ease;
    }

    form:hover {
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
    }

    input, textarea {
      width: 100%;
      padding: 12px 15px;
      margin: 12px 0 20px;
      border: 2px solid #d1d5db;
      border-radius: 6px;
      font-size: 1rem;
      transition: border-color 0.3s ease;
      font-family: inherit;
      resize: vertical;
    }

    input:focus, textarea:focus {
      border-color: #28a745;
      outline: none;
      box-shadow: 0 0 5px #28a745aa;
    }

    button {
      display: block;
      width: 100%;
      padding: 14px;
      font-size: 1.1rem;
      font-weight: 600;
      color: white;
      background-color: #28a745;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      box-shadow: 0 4px 12px rgba(40, 167, 69, 0.5);
    }

    button:hover {
      background-color: #218838;
      box-shadow: 0 6px 15px rgba(33, 136, 56, 0.6);
    }

    #posts {
      display: flex;
      flex-direction: column;
      gap: 25px;
    }

    .post {
      background: white;
      padding: 20px 25px;
      border-radius: 12px;
      box-shadow: 0 4px 18px rgba(0, 0, 0, 0.08);
      transition: transform 0.3s ease;
    }

    .post:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.12);
    }

    .post-title {
      font-weight: 700;
      font-size: 1.4rem;
      color: #2c3e50;
      margin-bottom: 10px;
      letter-spacing: 0.03em;
    }

    .post-content {
      font-size: 1rem;
      color: #555;
      white-space: pre-wrap; /* keep line breaks */
    }

    /* Responsive for small devices */
    @media (max-width: 480px) {
      body {
        max-width: 90%;
        padding: 0 15px 30px;
      }

      h1 {
        font-size: 1.8rem;
      }

      button {
        font-size: 1rem;
      }
    }
  </style>
</head>
<body>
  <h1>Simple Blog</h1>

  <form id="postForm" method="POST" action="/posts">
    <input type="text" name="title" placeholder="Title" required />
    <textarea name="content" placeholder="Content" rows="5" required></textarea>
    <button type="submit">Add Post</button>
  </form>

  <div id="posts"></div>

  <script>
    // Function to fetch and display posts
    function loadPosts() {
      fetch('/posts')
        .then(response => response.json())
        .then(posts => {
          const postsDiv = document.getElementById('posts');
          postsDiv.innerHTML = '';
          posts.forEach(post => {
            const postDiv = document.createElement('div');
            postDiv.className = 'post';
            postDiv.innerHTML = `<div class="post-title">${post.title}</div>
                                 <div class="post-content">${post.content}</div>`;
            postsDiv.appendChild(postDiv);
          });
        });
    }

    // Load posts when page loads
    window.onload = loadPosts;
  </script>
</body>
</html>

# Back end (Done in HTML/CSS)
const express = require('express');
const path = require('path');
const bodyParser = require('body-parser');

const app = express();

// Middleware to parse form data and JSON
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

// In-memory posts storage
let posts = [
  { id: 1, title: 'Welcome!', content: 'This is the first blog post.' },
];

// Serve the frontend HTML file
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'index.html'));
});

// API endpoint to get all posts
app.get('/posts', (req, res) => {
  res.json(posts);
});

// API endpoint to add a new post
app.post('/posts', (req, res) => {
  const { title, content } = req.body;
  if (!title || !content) {
    return res.status(400).send('Title and content are required');
  }
  const newPost = { id: posts.length + 1, title, content };
  posts.push(newPost);

  // Redirect back to homepage after adding post
  res.redirect('/');
});

// Start server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});

## How to use:

Save your frontend HTML file as index.html in the same folder as this index.js.

Make sure you have Node.js installed.

In terminal, run:

npm init -y
npm install express body-parser
node index.js

## Full project structure
simple-blog-app
Dockerfile
index.js
index.html
package.json
package-lock.json (optional)
