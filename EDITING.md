# Editing the WSGC Website — Volunteer Guide

This guide is for club volunteers who help keep **westseattlegolfclub.org** up to date.
**You do not need to know how to code.** You'll describe the change in plain English, let an
AI assistant (GitHub Copilot) write the small bit of HTML for you, and submit it for review.
Every change is checked by Dax before it goes live — so don't worry about "breaking" anything.

---

## The one rule that keeps you safe

> **Never change the live site directly. Always submit a "Pull Request" and let Dax publish it.**

That's the whole safety net. As long as you follow the steps below, the worst that can happen
is Dax sees your change, fixes a typo, and approves it. Nothing you do reaches the public site
until Dax clicks **Merge**.

---

## A few words you'll see (don't worry, they're simple)

- **Repository (or "repo")** — the folder that holds the website. Ours is `daxb/WSGC` on GitHub.
- **Branch** — a *safe scratch copy* of the site to make your change on, so the real site is
  untouched while you work. You'll make a new one for every change. GitHub creates it for you.
- **Commit** — saving your change onto that branch.
- **Pull Request (PR)** — a request that says "please review my change and publish it." This is
  what you send to Dax. He reviews it and clicks Merge to make it live.
- **Merge** — Dax's job, not yours. When he merges, the site updates automatically in about a minute.

You will only ever do: **make a branch → commit your change → open a PR.** Dax does the rest.

---

## Before you start (one time only)

1. **Make a free GitHub account** at [github.com](https://github.com) if you don't have one.
2. **Accept the invite.** Dax will invite you to the `daxb/WSGC` repository. You'll get an email
   with an **Accept invitation** button — click it. (This gives you permission to submit changes.)
3. That's it. Everything below happens in your web browser. Nothing to install.

---

## How a change goes live (the big picture)

```
You describe + paste the change  →  You open a Pull Request  →  Dax reviews & merges  →  Site updates (~1 min)
```

---

# Track A — Adding photos and documents (the easy stuff)

Use this for **gallery photos** and **newsletters / meeting minutes**. There's no code to write —
you're just uploading a file.

### Add gallery photos
1. Go to the repository: **https://github.com/daxb/WSGC**
2. Click into the **`media`** folder.
3. Click **Add file ▾ → Upload files**.
4. Drag your photo(s) in (or **choose your files**). Use simple file names, no weird characters
   — e.g. `summer-scramble-2026.jpg`. **Remember the exact file name**, you'll need it in Track B.
5. At the bottom, choose **"Create a new branch for this commit and start a pull request."**
6. Click **Propose changes**, then **Create pull request**. Done — that's your PR.

> Uploading the photo file makes it *available*, but it won't appear on the page until a small
> caption/image entry is added to the page. That part is **Track B → "Add a gallery photo."**
> You can do both in the same Pull Request (see the note at the end of Track B).

### Post a newsletter or meeting minutes
Same steps, but click into the **`newsletters and minutes`** folder instead, and upload the PDF.
Name it in the same style as the existing ones, e.g. `Jul'26 Meeting Minutes.pdf`.
For meeting minutes there's usually a link to add on the page too — ask Copilot (Track B) for
"add a meeting-minutes link for July 2026" if you want it listed, or just note it in your PR and
Dax will add it.

---

# Track B — Text changes (Copilot writes the HTML for you)

Use this for the **president's message, news updates, events, board members, and the photo
captions** that go with Track A uploads. The website is one big file (`index.html`), so we use
Copilot to write the correct snippet and we **paste it into a clearly-marked spot**.

## Step 1 — Ask Copilot to write the snippet

1. Go to **[github.com/copilot](https://github.com/copilot)**.
2. Make sure the mode button says **Ask**.
3. Click the repository button and select **`daxb/WSGC`** (so Copilot can see our website and
   match its style). *Tip: pick a Claude model if offered — it's good at this.*
4. Type your request in plain English. **Copy one of the ready-made prompts below**, fill in your
   details, and send it.
5. Copilot will reply with a block of HTML. Click the **copy** button on that block.

> **Important — what Copilot Free can and can't do:** Copilot will *write* the snippet for you,
> but on the free plan it **won't edit the website itself** — you'll paste it in (Step 2). Also,
> the free plan allows about **50 Copilot messages per month**, so don't burn them on chit-chat.
> If you ever get stuck, just write what you want in plain English in your Pull Request and Dax
> will finish it.

### Ready-made Copilot prompts (copy, then fill in the blanks)

**New monthly president's message — this one has TWO parts.** A president's message is its own
full web page (an `.html` file) *and* a card on the home page that links to it. Do both in the
same Pull Request.

*Part 1 — create the message page.* Ask Copilot:
> Using the daxb/WSGC repo, look at the file `newsletters and minutes/Jun'26 President's Message.html`.
> Write me a **complete new page just like it** (same layout, styles, header, and footer) for the
> **MONTH YEAR** president's message. Here is the message text: "_______ (paste the full message) _______".
> Give me the entire HTML file so I can save it.

Then save it as a new file:
> Go to **https://github.com/daxb/WSGC**, open the **`newsletters and minutes`** folder, click
> **Add file ▾ → Create new file**, name it exactly like `Jul'26 President's Message.html`, paste
> Copilot's page in, and **Commit changes → "Create a new branch… start a pull request."** Keep
> that branch name in mind — you'll add Part 2 to the *same* branch/PR.

> *Too much? You can skip Part 1 and ask Dax to create the message page — then just do Part 2 and
> mention it in your PR.*

*Part 2 — add the home-page card.* Ask Copilot:
> Using the daxb/WSGC repo, in index.html find the comment "NEWS / PRESIDENT'S MESSAGE". Write me a
> new **featured** news card titled "_______", summary "_______", dated "Month Year", linking to the
> file `newsletters and minutes/MON'YY President's Message.html`. Also show me how to turn the
> current featured card into a regular news card. Match the existing HTML and classes exactly.

**A news update:**
> In daxb/WSGC index.html, near the "NEWS / PRESIDENT'S MESSAGE" comment, write me a regular
> news card titled "_______", summary "_______", dated "Month Year". Match the existing markup.

**Add a gallery photo (pairs with a Track A upload):**
> In daxb/WSGC index.html, near the "ADD A GALLERY PHOTO" comment, write me a gallery-item entry
> for the image file `media/MY-FILE.jpg` with the caption "_______" and date "Month Year".
> Match the existing markup exactly.

**Add or update an event:**
> In daxb/WSGC index.html, near the "ADD OR UPDATE AN EVENT" comment, write me an event card for
> "Event Name" on DATE, format "_______", with this description: "_______". Match the existing markup.

**Update a board member or email:**
> In daxb/WSGC index.html, near the "BOARD OF DIRECTORS" comment, the card for "Role" should now
> read name "_______" and email "_______@westseattlegolfclub.org". Show me the corrected card.

## Step 2 — Paste it into the website

1. Go to **https://github.com/daxb/WSGC** and click on **`index.html`** to open it.
2. Click the **pencil icon** (✏️ "Edit this file") at the top right of the file.
3. Press **Ctrl+F** (Windows) or **Cmd+F** (Mac) to search *inside the file*, and type the
   matching anchor name to jump to the right spot:
   - President's message / news → search **`NEWS / PRESIDENT'S MESSAGE`**
   - Gallery photo → search **`ADD A GALLERY PHOTO`**
   - Event → search **`ADD OR UPDATE AN EVENT`**
   - Board member → search **`BOARD OF DIRECTORS`**
4. You'll see a clearly-marked comment block with instructions and a template. **Paste the snippet
   Copilot gave you right below that comment block** (or, for edits, replace the existing card).
   Add new items at the **top** of news and gallery so the newest shows first.
5. *(Optional sanity check)* Click the **Preview** tab to glance at your change.

## Step 3 — Submit it for review (open the Pull Request)

1. Click **Commit changes…** (top right).
2. In the box, choose **"Create a new branch for this commit and start a pull request."**
   (GitHub will suggest a branch name — that's fine, leave it.)
3. Add a short message like *"Add June president's message"* and click **Propose changes**.
4. On the next screen click **Create pull request**. 🎉 You're done.

Dax gets notified, reviews it, and merges it. The site updates by itself shortly after.

> **Doing a photo in one go:** A gallery photo needs both the upload (Track A) *and* the caption
> entry (Track B). Easiest path: do the Track A upload first and choose "create a new branch."
> Then, while that PR is open, you can add the Track B caption to the **same branch** and it'll
> join the same Pull Request. If that feels fiddly, just open two PRs and mention they go together.

---

## The optional shortcut for the adventurous

On the repository page you can press the **`.`** (period) key to open a built-in web editor
(github.dev). If a Copilot panel appears there, you can describe your change and let it edit the
file directly, then commit + open a PR from the same screen. **This may or may not be available
on the free plan** — if you don't see Copilot there, just ignore this and use Track B above.

---

## If something looks wrong

- **Don't panic and don't try to merge** — you can't publish anyway; only Dax can.
- Leave a comment on your Pull Request describing what's confusing, and Dax will sort it out.
- If you closed something by accident, just start over with a fresh change. Nothing is lost and
  the live site is never affected by an unmerged PR.

**Questions?** Email the board or ping Dax. Thanks for helping keep the WSGC site fresh!
