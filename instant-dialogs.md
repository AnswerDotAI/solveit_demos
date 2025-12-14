# Instant Dialogs and Templates

SolveIt can use plain URLs for creating and opening dialogs — which means you can launch them from anywhere: browser bookmarks, command line (`open https://...`), phone home screen shortcuts, or even links in other apps. This guide shows you how to set that up.

## What You'll Learn

You'll learn how to:

- … create a bookmark that instantly creates a new dialog (optionally in a specific folder)
- … understand how `?name=` behaves depending on whether the target is a folder, dialog, or doesn't exist
- … set up a template dialog and bookmark it, so one click creates a fresh copy ready to use
- … use the "instant delete" button for quick cleanup
- … set up Chrome address bar shortcuts for named dialogs, so you can type `sv my-project` to instantly create or open a dialog called "my-project"

## Creating a New Dialog Instantly

The simplest use case: you want a bookmark that creates a fresh dialog with one click.

### The URL

```
https://your-solveit-url.com/dialog_
```

That's it! When you visit this URL, Solveit automatically:

1. Creates a new dialog called `scratch` (or `scratch_dup1`, `scratch_dup2`, etc. if `scratch` already exists)
2. Opens it for you

You can find your equivalent to `your-solveit-url.com` by examining the URL of a dialog in the instance where you want to create the new dialogs.

### Setting Up the Bookmark in Chrome

1. Right-click on Chrome's bookmarks bar (the strip below the address bar)
2. Click **"Add page..."**
3. In the **Name** field, type something like `New Solveit Dialog`
4. In the **URL** field, paste your solveit URL followed by `/dialog_`, for example:
   ```
   https://my-solveit.answer.ai/dialog_
   ```
5. Click **Save**

Now clicking that bookmark instantly creates and opens a new dialog.

## Creating a Dialog in a Specific Folder

If you organise your dialogs into folders, you can create bookmarks that put new dialogs directly into a particular folder.

### The URL

Add `?name=` followed by the path to a folder on your instance:

```
https://your-solveit-url.com/dialog_?name=projects/experiments
```

This creates a new dialog inside the `projects/experiments` folder, automatically named `scratch` (or `scratch_dup1`, etc.).

### About Slashes in URLs

You might notice that when you copy a URL from your browser, slashes in the folder path sometimes appear as `%2F`. For example, `projects/experiments` might become `projects%2Fexperiments`. Don't worry — both versions work identically. The `%2F` is just a way of encoding the `/` character in URLs. When creating bookmarks manually, you can use plain slashes for readability.

## What Happens When You Use `?name=`

The `?name=` parameter is smart — it behaves differently depending on what the name points to:

| What `name` points to | What happens |
|----------------------|--------------|
| An existing **folder** | Creates `scratch` (or `scratch_dup1`, etc.) inside that folder |
| An existing **dialog** | Opens that dialog directly |
| **Nothing** (doesn't exist yet) | Creates a new dialog with that exact name |

### Examples

Here's how this works in practice:

- **`?name=projects`** where `projects` is a folder → creates `projects/scratch`
- **`?name=projects/my-analysis`** where that dialog already exists → opens it
- **`?name=projects/new-experiment`** where nothing with that name exists → creates a new dialog called `projects/new-experiment`

Think of it this way: if you're pointing at a folder, Solveit puts a new scratch dialog inside it. If you're pointing at a dialog, Solveit opens it. If you're pointing at nothing, Solveit creates it.

## Duplicating an Existing Dialog

You can set up a **template dialog** and create a bookmark that instantly spawns a fresh copy whenever you need one. This is perfect for recurring workflows: set up a dialog with your preferred preamble, starter code, or instructions, then bookmark its duplication URL.

### The URL

Use `/dup_` instead of `/dialog_`, and specify which dialog to duplicate:

```
https://your-solveit-url.com/dup_?name=templates/my-starter
```

When you visit this URL, Solveit:

1. Creates a copy of `templates/my-starter`
2. Names it `templates/my-starter_dup1` (or `_dup2`, `_dup3`, etc.)
3. Opens the new copy

### Finding the Path of an Existing Dialog

To create a duplication bookmark, you need to know the dialog's path. The easiest way:

1. Open the dialog you want to duplicate
2. Look at the URL in your browser's address bar
3. The path appears after `/dialog_?name=`

For example, if the URL is:
```
https://my-solveit.answer.ai/dialog_?name=work%2Fprojects%2Fanalysis
```

The dialog path is `work/projects/analysis` (remembering that `%2F` is just `/`).

## The Instant Delete ("bomb") Button

When you duplicate a dialog, or use the `/dialog_` route to auto-name a new dialog, the copy has a name ending in `_dup` followed by a number (e.g., `scratch_dup3`).

Dialogs with this naming pattern have a special **instant delete** button (a bomb icon 💣) that appears in the menu. This makes it quick to clean up duplicates you no longer need.

If you find yourself with a duplicate you want to keep, just rename it to remove the `_dup` suffix — this removes the bomb icon and protects it from accidental deletion.

Dialogs that *don't* follow this naming pattern won't show the instant delete button — this protects your original dialogs from accidental deletion.

## Practical Workflow Tips

### Quick Scratch Dialogs

A handy workflow is to create a folder specifically for throwaway dialogs, then bookmark it:

1. Open the integrated Terminal in Solveit
2. Create a folder: `mkdir chats` (or any name you like)
3. Create a bookmark to `/dialog_?name=chats`

Now whenever you need a quick dialog for testing, experimenting, or a one-off chat, just click your bookmark. You'll get a fresh `chats/scratch` dialog (or `chats/scratch_dup1`, etc.) ready to go.

Because these auto-generated dialogs have names ending in `_dup`, they show the bomb icon — perfect for quick cleanup when you're done.

### Forking with `d`

Press `d` while in any dialog to instantly duplicate it. This is a great way to "fork" your work — explore a new direction without risking your original.

If the fork works out, rename it to something meaningful. If not, just hit the bomb icon to discard it. You can also copy messages from your fork back to the original using the standard `c` (copy) and `v` (paste) keys.

### Quick Named Dialogs from the Address Bar

Chrome's "site search shortcuts" feature lets you create new named dialogs directly from your address bar. Here's how to set it up:

1. Open Chrome and go to **Settings** → **Search engine** → **Manage search engines and site search**
2. Scroll down to **Site search** and click **Add**
3. Fill in the fields:
   - **Search engine**: `Solveit New Dialog` (or whatever you like)
   - **Shortcut**: `sv` (or any short keyword you prefer)
   - **URL**: `https://your-solveit-url.com/dialog_?name=chats/%s`
4. Click **Save**

Now you can type `sv my-project` in Chrome's address bar, and it will create a new dialog called `chats/my-project` — or open it if it already exists.

See [Google's guide to site search shortcuts](https://support.google.com/chrome/answer/95426) for more details.

### Keeping a Throwaway Dialog

Sometimes a "throwaway" dialog turns out to be valuable. To keep it:

1. Rename it to something meaningful (removing the `_dup` suffix)
2. The bomb icon disappears
3. Your dialog is now protected from instant deletion and has a meaningful name.

---

## Quick Reference

| Goal | URL Pattern | Result |
|------|-------------|--------|
| New dialog at root | `/dialog_` | Creates `scratch` (or `scratch_dup1`, etc.) |
| New dialog in folder | `/dialog_?name=folder/subfolder` | Creates `folder/subfolder/scratch` |
| Open existing dialog | `/dialog_?name=folder/my-dialog` | Opens `folder/my-dialog` |
| Create named dialog | `/dialog_?name=folder/new-name` | Creates `folder/new-name` (if it doesn't exist) |
| Duplicate existing dialog | `/dup_?name=path/to/dialog` | Creates `path/to/dialog_dup1` |

## Editing a Bookmark Later

If you need to change a bookmark's URL:

1. Right-click the bookmark
2. Click **"Edit..."**
3. Modify the URL field
4. Click **Save**
