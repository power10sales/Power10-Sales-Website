# Your Website

This folder is your website, www.powertensales.com.

You don't need to know how to code. You tell Claude what you want, in normal words, and Claude
does it for you.

## Making a change

Open Claude Code and ask. For example:

- "Change the phone number on the About Us page to 650-555-1234."
- "Replace the paragraph about METALfx with this text: ..."
- "Add a new partner logo below King Epoxy."

Claude makes the change and saves it.

## Look at it before anyone else does

This is the most useful habit to build. Ask:

> "Show me the site on my computer before we publish."

Claude opens a private preview that only you can see. Check it over. If something looks wrong,
say what's wrong and ask Claude to fix it. Nobody sees any of this until you say so.

## Publishing

When you're happy with it, say:

> "Publish this."

Your change is live in about one or two minutes. Then go to www.powertensales.com and refresh.

**Don't see your change?** Hold down Shift and click the refresh button. Your browser saves a copy
of pages to load them faster, and sometimes it shows you the old saved copy. Shift-refresh forces
it to fetch the new one.

## Your three pages

- **Home** — `index.html`
- **About Us** — `about-us/index.html`
- **Privacy Policy** — `privacy-policy/index.html`

You don't have to remember the file names. Just say "the home page" and Claude will know.

## The other folders

- **`assets/img`** — all your pictures
- **`assets/css`** — the colors, fonts and spacing
- **`assets/js`** — makes the menu and the scroll-to-top arrow work
- **`_source`** — a saved copy of your old website. None of this is on the internet. It's kept in
  case something from the old site is ever needed. Leave it alone.

## Adding a picture

1. Put the picture file into the `assets/img` folder.
2. Ask Claude to add it where you want it.

Photos from a phone or camera are usually far bigger than a website needs, which makes pages slow
to load. Ask Claude to shrink it for the web and it will handle that.

## If something looks wrong

Say:

> "Undo my last change."

Every version is saved automatically. Nothing is ever truly lost, so you can't permanently break
this by trying something.

## Please don't delete these

At the top of the folder are two small files, `CNAME` and `.nojekyll`. They look unimportant.
They aren't.

- **`CNAME`** connects your web address to this site. If it's deleted, the site goes offline.
- **`.nojekyll`** stops the website from being rearranged automatically.

Also, don't rename or move the folders. The pages find their pictures and colors by folder name,
so moving things breaks those connections.

## One good habit

After any change, ask:

> "Check that all three pages still work."

Claude will load each page and confirm nothing broke. It takes a few seconds and it catches
mistakes before your customers do.
