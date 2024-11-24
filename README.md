<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Zaid Slug Generator Tool</title>
  <style>
    /* General Body Styles */
    body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(to bottom, #f7f9fc, #e2e8f0);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }

    /* Container Styles */
    .container {
      background: #ffffff;
      padding: 20px;
      max-width: 600px;
      width: 100%;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      text-align: center;
    }

    /* Header Styles */
    h1 {
      font-size: 1.8em; /* Adjust font size */
      color: #333333;
      margin-bottom: 10px;
      white-space: nowrap; /* Prevents text from breaking into multiple lines */
      overflow: hidden; /* Prevents overflow */
      text-overflow: ellipsis; /* Adds "..." if the text overflows */
    }

    p {
      color: #666666;
      margin-bottom: 20px;
      font-size: 1em;
    }

    /* Input and Button Styles */
    textarea, button {
      width: 100%;
      margin: 10px 0;
      padding: 15px;
      font-size: 1em;
      border-radius: 5px;
      border: 1px solid #ddd;
    }

    textarea {
      resize: none; /* Prevent manual resizing */
      overflow-y: auto; /* Show scrollbar only when necessary */
      box-sizing: border-box; /* Prevent padding from overflowing */
    }

    button {
      background: linear-gradient(to right, #007bff, #0056b3);
      color: #ffffff;
      border: none;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.3s ease;
    }

    button:hover {
      background: linear-gradient(to right, #0056b3, #003d80);
    }

    /* Output Box Styles */
    .output {
      margin-top: 20px;
      font-weight: bold;
      color: #333333;
      padding: 15px;
      background: #f7f9fc;
      border: 1px solid #ddd;
      border-radius: 5px;
      display: inline-block;
      width: 100%;
      box-sizing: border-box;
    }

    /* Copy Button Styles */
    .copy-btn {
      margin-top: 10px;
      padding: 15px;
      font-size: 1em;
      background: linear-gradient(to right, #28a745, #218838);
      color: #ffffff;
      border: none;
      cursor: pointer;
      border-radius: 5px;
      font-weight: bold;
      transition: background 0.3s ease;
    }

    .copy-btn:hover {
      background: linear-gradient(to right, #218838, #1c7430);
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Mohammad Zaid SEO Slug Generator Tool</h1>
    <p>Enter text to generate an SEO-friendly slug:</p>

    <textarea id="textInput" rows="4" placeholder="Paste your URL here..."></textarea>
    <button onclick="generateSlug()">Generate Slug</button>

    <div class="output" id="output">Your generated slug will appear here...</div>
    <button class="copy-btn" id="copyButton" style="display: none;" onclick="copySlug()">Copy to Clipboard</button>
  </div>

  <script>
    // Slugify function
    function slugify(text) {
      return text
        .toString()
        .normalize('NFD')                   // Normalize to decompose combined characters
        .replace(/[\u0300-\u036f]/g, '')    // Remove diacritics
        .toLowerCase()
        .trim()
        .replace(/[^a-z0-9 -]/g, '')        // Remove invalid characters
        .replace(/\s+/g, '-')               // Replace spaces with hyphens
        .replace(/-+/g, '-');               // Replace multiple hyphens with a single hyphen
    }

    // Generate slug and display output
    function generateSlug() {
      const textInput = document.getElementById('textInput').value.trim();
      const outputElement = document.getElementById('output');
      const copyButton = document.getElementById('copyButton');

      if (textInput === "") {
        // If input is empty, show a message and hide the copy button
        outputElement.textContent = "Please enter text to generate a slug.";
        copyButton.style.display = 'none';
        return;
      }

      const slug = slugify(textInput);
      outputElement.textContent = `Generated Slug: ${slug}`;
      copyButton.style.display = 'inline-block'; // Show the copy button
      copyButton.setAttribute('data-slug', slug); // Store slug in a custom attribute
    }

    // Copy slug to clipboard
    function copySlug() {
      const copyButton = document.getElementById('copyButton');
      const slug = copyButton.getAttribute('data-slug');

      if (!slug) {
        alert("No slug to copy!");
        return;
      }

      // Copy to clipboard
      navigator.clipboard.writeText(slug).then(() => {
        alert(`Slug copied to clipboard: ${slug}`); // Show the slug in the popup
      }).catch(err => {
        console.error('Failed to copy slug: ', err);
      });
    }
  </script>

</body>
</html>
