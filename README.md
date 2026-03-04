# Reyes Tham — Portfolio

A minimalist personal portfolio with a built-in CMS admin panel. Hosted free on GitHub Pages.

---

## 📁 File Structure

```
portfolio/
├── index.html      ← Your live portfolio website
├── admin.html      ← Private CMS to edit all content
├── data.json       ← All your content lives here
└── README.md
```

---

## 🚀 Deploy to GitHub Pages (Free Hosting)

### Step 1 — Create a GitHub Account
Go to [github.com](https://github.com) and sign up if you don't have an account.

### Step 2 — Create a New Repository
1. Click the **+** button → **New repository**
2. Name it: `portfolio` (or `yourusername.github.io` for a custom URL)
3. Set it to **Public**
4. Click **Create repository**

### Step 3 — Upload Your Files
1. In your new repo, click **Add file → Upload files**
2. Drag and drop all 3 files: `index.html`, `admin.html`, `data.json`
3. Click **Commit changes**

### Step 4 — Enable GitHub Pages
1. Go to your repo **Settings** tab
2. Scroll to **Pages** in the left sidebar
3. Under **Source**, select **main** branch → **/ (root)**
4. Click **Save**
5. Wait ~60 seconds — your site will be live at:
   `https://yourusername.github.io/portfolio`

---

## ✏️ How to Update Content

### Using the Admin Panel

1. Open `https://yourusername.github.io/portfolio/admin.html`
2. Password: `reyes2025` *(change this in admin.html line 1 — search for `const PASS`)*
3. Edit anything — projects, clubs, photos, achievements
4. Click **Save & Export JSON** → downloads `data.json`
5. Go to your GitHub repo → click `data.json` → click the **pencil icon** → paste the new content → **Commit**

OR drag & drop the new `data.json` onto your repo via **Add file → Upload files**.

Your live site updates within seconds.

### Changing the Admin Password

Open `admin.html`, find this line near the top of the `<script>` section:
```js
const PASS = 'reyes2025';
```
Change it to whatever you want, then re-upload `admin.html` to GitHub.

---

## 📸 Adding Photos to Clubs

1. Open `admin.html` → Clubs section
2. Click a club to expand it
3. Click **Upload** and select photos from your device (up to 5 per club)
4. Photos are embedded directly in `data.json` as base64
5. Export and commit the updated `data.json`

---

## 🔗 Adding Project Links

1. Open `admin.html` → Projects section
2. Expand a project
3. Paste the GitHub/demo URL in the **Link** field
4. Export and commit

If a project has no link, the expand panel shows only the description (no button).
