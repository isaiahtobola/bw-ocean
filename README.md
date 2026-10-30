# BW Ocean 🌊🏛️

**BW Ocean** — a digital museum of BW Young Bo. A mini-Flickr in plum and gold:
one long scroll of exhibits (gaming, music, art), where the curator posts
songs, videos, and images that stay up — and visitors can like and comment.

The site itself is a single file (`index.html`). All the storage, posting,
likes, and comments run on a free [Supabase](https://supabase.com) project.
Nobody needs an account to look, like, or comment. Only the curator can post.

---

## One-time setup (about 10 minutes)

### 1. Supabase — the museum's storage vault

1. Go to [supabase.com](https://supabase.com), sign up, and **create a new project**
   (any name — "bw-ocean" works). Pick a region near you and a database password
   (save that password somewhere safe; the site never needs it, but you might).
2. Wait for the project to finish setting up (~2 minutes).
3. In the left sidebar, open **SQL Editor → New query**.
4. Copy the *entire* contents of **`setup.sql`** (from this folder), paste it in,
   and hit **Run**. You should get a success message. This builds the three
   tables (exhibits, likes, comments), the `media` storage bucket, and all the
   permission rules.
5. Create the curator login — that's you:
   - Go to **Authentication → Users → Add user → Create new user**.
   - Enter **your** email and a strong password, and create it.
6. Lock the door behind you:
   - Go to **Authentication → Sign In / Providers** (a.k.a. Auth settings) and
     turn **OFF** "Allow new users to sign up."
   - Now nobody can register — the account you just made is the only key that
     can ever sign in and post. Visitors never need an account at all.

### 2. Connect the site to Supabase

1. In your Supabase dashboard, go to **Project Settings → API**.
2. Copy the **Project URL** and the **anon public** key.
   (Never share the `service_role` key — the site does not use it, ever.)
3. Open **`index.html`** in any text editor and find the CONFIG block at the
   top of the script, near the bottom of the file. Replace the two placeholders:

   ```js
   const SUPABASE_URL = "PASTE_PROJECT_URL_HERE";
   const SUPABASE_ANON_KEY = "PASTE_ANON_KEY_HERE";
   ```

   with your real URL and anon key, keeping the quotes. Save the file.

### 3. GitHub — put the museum on the web

1. Go to [github.com](https://github.com), click **New repository**, name it
   something like `bw-ocean`, make it **Public**, and create it.
2. Click **uploading an existing file** and upload **`index.html`**. Commit it.
3. In the repo, go to **Settings → Pages**. Under "Build and deployment,"
   choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. Wait a minute or two — GitHub shows your live address near the top of that
   same Pages screen, like `https://isaiahtobola.github.io/bw-ocean/`.
   That's the museum's front door. Share it anywhere.

---

## Running the museum

**Posting an exhibit**
1. Open the site and sign in with **Curator sign-in** (top right) using the
   email/password you created in step 1.5.
2. The "Hang a new exhibit" panel appears. Give it a title, pick a room
   (Gaming / Music / Art), then either:
   - **upload a file** — an image, a song (mp3 etc.), or a video, or
   - **paste a YouTube link** for a video exhibit (it shows as an embed).
3. Hit **Hang it on the wall**. It appears at the top of the feed immediately.
4. Sign out when you're done. Signed out = the upload panel disappears;
   nobody else ever sees it.

**Visitors** just scroll. They can filter by room with the tabs, tap ♥ to
like (one like per browser), and open **Comments** on any piece to read or
leave a comment with just a name — no accounts, no hassle.

**Removing something** (for now): delete its row in Supabase under
**Table Editor → exhibits**, and the file itself under **Storage → media**.
Likes and comments attached to it clean themselves up automatically.

---

## Files in this folder

| File | What it is |
| --- | --- |
| `index.html` | The whole museum — design, feed, likes, comments, curator upload |
| `setup.sql` | One-time database setup; paste into Supabase's SQL Editor once |
| `README.md` | This file |

*What connects, remains.*
