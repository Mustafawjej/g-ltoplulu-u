# Q&A Nexus | Cyberpunk Setup Guide

This guide will help you set up your high-performance Q&A website using Supabase. No coding knowledge is required!

## Step 1: Create a Supabase Account
1. Go to [supabase.com](https://supabase.com/) and click **"Start your project"**.
2. Sign up with your GitHub account or Email.
3. Click **"New Project"**.
4. Select an Organization, give your project a name (e.g., "QA-Nexus"), and set a secure password.
5. Choose a region close to you and click **"Create new project"**.

## Step 2: Initialize Database Tables
We need to set up two tables: `questions` and `answers`.

### 1. The Questions Table
1. In the sidebar, click on **"SQL Editor"** (the `>_` icon).
2. Click **"New query"**.
3. Copy and paste the following code and click **"Run"**:

```sql
create table questions (
  id uuid default gen_random_uuid() primary key,
  created_at timestamptz default now(),
  content text not null,
  image_url text,
  category text default 'General Knowledge',
  likes integer default 0
);

-- Enable Row Level Security
alter table questions enable row level security;

-- Create policies to allow anyone to read and post
create policy "Allow public read access" on questions for select using (true);
create policy "Allow public insert access" on questions for insert with check (true);
create policy "Allow public update access" on questions for update using (true);
```

### 2. The Answers Table
1. Click **"New query"** again.
2. Copy and paste the following code and click **"Run"**:

```sql
create table answers (
  id uuid default gen_random_uuid() primary key,
  created_at timestamptz default now(),
  question_id uuid references questions(id) on delete cascade,
  content text not null
);

-- Enable Row Level Security
alter table answers enable row level security;

-- Create policies
create policy "Allow public read access" on answers for select using (true);
create policy "Allow public insert access" on answers for insert with check (true);
```

## Step 3: Set up Image Storage
1. Click on **"Storage"** (the bucket icon) in the sidebar.
2. Click **"New bucket"**.
3. Name it: `question-images`.
4. Toggle **"Public"** to **ON**.
5. Click **"Save"**.
6. Click **"New Policy"** for the bucket.
7. Select **"Get started quickly"**.
8. Add both **"Give users access to SELECT"** (Read) and **"Give users access to INSERT"** (Upload) policies.

## Step 4: Connect your Website
1. Go to **"Project Settings"** (the gear icon at bottom left) > **"API"**.
2. Copy your **"Project URL"**.
3. Open `index.html` in a text editor.
4. Replace `YOUR_SUPABASE_URL` (around line 214) with your URL.
5. Copy your **"anon public"** key from Supabase.
6. Replace `YOUR_SUPABASE_ANON_KEY` (around line 215) with your key.
7. Save the file.

## Step 5: Final Check
1. Ensure your logo is named `logo.png` and is in the same folder.
2. **Double-click `index.html`** to enter the nexus.
3. Test the search bar, category filters, likes, and reply system!
