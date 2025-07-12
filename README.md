from pathlib import Path
import shutil
import zipfile

# Create directories again
clean_upload_dir = Path("/mnt/data/ability_clean_upload")
clean_assets_dir = clean_upload_dir / "assets"
clean_zip_path = "/mnt/data/ability_shines_clean_upload.zip"

clean_upload_dir.mkdir(parents=True, exist_ok=True)
clean_assets_dir.mkdir(parents=True, exist_ok=True)

# HTML content
index_html_content = """<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ability Shines Aromatherapy</title>
  <link rel="stylesheet" href="assets/styles.css">
</head>
<body>
  <div class="container">
    <img src="assets/logo-placeholder.png" alt="Ability Shines Logo" class="logo">
    <h1>Ability Shines</h1>
    <h2>Aromatherapy</h2>
    <p>We all have the ability to shine!<br>
    Aromaterappy made with Love and neurodifferent hands.</p>

    <div class="info-box">
      <strong>Wondering where to find us?</strong><br>
      <a href="https://www.facebook.com/profile.php?id=61572144783909">Check out our Facebook page!</a>
    </div>

    <h2>Leave a Review</h2>
    <form onsubmit="event.preventDefault(); addReview();">
      <input type="text" id="name" name="name" placeholder="Name" required>
      <textarea id="review" name="review" rows="4" placeholder="Review" required></textarea>
      <input type="submit" value="Submit">
    </form>

    <div id="reviews" class="review-section">
      <h2>Reviews</h2>
      <ul id="reviewList"></ul>
    </div>
  </div>

  <script>
    function addReview() {
      const name = document.getElementById('name').value;
      const review = document.getElementById('review').value;
      const reviewList = document.getElementById('reviewList');
      const newItem = document.createElement('li');
      newItem.innerHTML = `<strong>${name}</strong>: ${review}`;
      reviewList.appendChild(newItem);
      document.getElementById('name').value = '';
      document.getElementById('review').value = '';
    }
  </script>
</body>
</html>
"""

# CSS content
styles_css_content = """
body {
  margin: 0;
  padding: 0;
  font-family: 'Georgia', serif;
  background: url('background-puzzle.jpg') repeat;
  background-size: cover;
  color: #2a2a2a;
  text-align: center;
}

.container {
  max-width: 600px;
  margin: auto;
  padding: 40px 20px;
  background-color: rgba(255, 255, 255, 0.9);
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
}

.logo {
  max-width: 200px;
  margin: 0 auto 20px;
}

h1 {
  font-size: 2.5rem;
  color: #2a2a2a;
  margin: 0.5em 0;
}

h2 {
  font-size: 1.25rem;
  margin-bottom: 1.5em;
}

.info-box {
  background-color: #fef9f0;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 1em;
  margin: 1em 0 2em;
  font-size: 1rem;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

input[type="text"], textarea {
  padding: 0.75em;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-family: 'Georgia', serif;
}

button, input[type="submit"] {
  padding: 0.75em;
  background-color: #1a4d4a;
  color: white;
  font-size: 1rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

button:hover, input[type="submit"]:hover {
  background-color: #256f6a;
}
"""

# .gitignore content
gitignore_content = """
# Ignore system files
.DS_Store
Thumbs.db

# Ignore IDE/editor folders
.vscode/
.idea/

# Ignore logs and temporary files
*.log
*.tmp
*.bak
*.swp

# Ignore node and build tools
node_modules/
dist/
build/
"""

# Write files
(clean_upload_dir / "index.html").write_text(index_html_content, encoding="utf-8")
(clean_assets_dir / "styles.css").write_text(styles_css_content, encoding="utf-8")
(clean_upload_dir / ".gitignore").write_text(gitignore_content.strip(), encoding="utf-8")

# Placeholder images recreated as blank files
(clean_assets_dir / "background-puzzle.jpg").write_bytes(b"")
(clean_assets_dir / "logo-placeholder.png").write_bytes(b"")

