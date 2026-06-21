# Q&A Website Setup Guide

This guide will help you set up your modern Q&A website using Supabase. No coding knowledge is required!

## Step 1: Create a Supabase Account
1. Go to [supabase.com](https://supabase.com/) and click **"Start your project"**.
2. Sign up with your GitHub account or Email.
3. Click **"New Project"**.
4. Select an Organization (or create one), give your project a name (e.g., "QA-Hub"), and set a secure password.
5. Choose a region close to you and click **"Create new project"**. Wait a few minutes for it to initialize.

## Step 2: Create the Database Table
1. In your Supabase dashboard, click on **"Table Editor"** (the table icon on the left sidebar).
2. Click **"Create a new table"**.
3. Name the table: `questions`.
4. Enable **"Row Level Security (RLS)"** (it should be enabled by default).
5. Columns to add:
   - `id`: Should be `uuid` (default), Primary Key.
   - `created_at`: Should be `timestamptz` (default), default value `now()`.
   - `content`: Select type `text`.
   - `image_url`: Select type `text` (Allow Nullable).
6. Click **"Save"**.

## Step 3: Set up Storage for Images
1. Click on **"Storage"** (the bucket icon on the left sidebar).
2. Click **"New bucket"**.
3. Name it: `question-images`.
4. Make sure to toggle **"Public"** to ON so everyone can see the uploaded images.
5. Click **"Save"**.

## Step 4: Configure Permissions (RLS Policies)
By default, Supabase blocks all access for security. We need to allow people to read and post questions.

### For the `questions` table:
1. Go to **"Authentication"** > **"Policies"** in the sidebar.
2. Find the `questions` table and click **"New Policy"**.
3. Choose **"Get started quickly"** (Templates).
4. Select **"Enable read access for all users"** and click **"Use this template"**, then **"Review"**, then **"Save"**.
5. Click **"New Policy"** again for the `questions` table.
6. Select **"Enable insert access for all users"** (or "Enable insert for anonymous users"), click **"Use this template"**, then **"Review"**, then **"Save"**.

### For the Storage bucket:
1. Stay in **"Policies"** and click the **"Storage"** tab at the top.
2. Find `question-images` and click **"New Policy"**.
3. Choose **"Get started quickly"**.
4. Select **"Give users access to SELECT"** (Read), use the template, and save.
5. Click **"New Policy"** again, select **"Give users access to INSERT"** (Upload), use the template, and save.

## Step 5: Connect your Website
1. Go to **"Project Settings"** (the gear icon at the bottom left).
2. Click **"API"**.
3. Copy the **"Project URL"**.
4. Open the `index.html` file in a text editor (like Notepad or VS Code).
5. Find line 93: `const SUPABASE_URL = 'YOUR_SUPABASE_URL';` and replace `YOUR_SUPABASE_URL` with your actual URL.
6. Go back to Supabase and copy the **"anon public"** key.
7. Find line 94: `const SUPABASE_KEY = 'YOUR_SUPABASE_ANON_KEY';` and replace `YOUR_SUPABASE_ANON_KEY` with your actual key.
8. Save the `index.html` file.

## Step 6: Run and Test
1. Make sure your logo image is in the same folder as `index.html` and named `logo.png`.
2. Simply **double-click `index.html`** to open it in your web browser.
3. Click "Ask Question", type something, upload an image, and hit "Post Question"!

Your question should appear instantly in the feed.
