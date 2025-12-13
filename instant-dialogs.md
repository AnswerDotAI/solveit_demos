# Instant Dialogs and Duplicates

SolveIt lets you instantly create new dialogs or duplicate existing ones by using special URLs. This guide shows you how to set up browser bookmarks for quick access to these features.

## What You'll Learn

- How to create a bookmark that instantly creates a new dialog
- How to create those dialogs in a specific folder
- How to create a bookmark that duplicates an existing dialog
- How the "instant delete" button works for duplicates

---

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

---

## Creating a Dialog in a Specific Folder

If you organise your dialogs into folders, you can create bookmarks that put new dialogs directly into a particular folder.

### The URL

Add `?name=` followed by the path to a folder _which already exists_ on your instance:

```
https://your-solveit-url.com/dialog_?name=projects/experiments
```

This creates a new dialog inside the `projects/experiments` folder, automatically named `scratch` (or `scratch_dup1`, etc.).

### About Slashes in URLs

You might notice that when you copy a URL from your browser, slashes in the folder path sometimes appear as `%2F`. For example, `projects/experiments` might become `projects%2Fexperiments`. Don't worry — both versions work identically. The `%2F` is just a way of encoding the `/` character in URLs. When creating bookmarks manually, you can use plain slashes for readability.

---

## Duplicating an Existing Dialog

If you have a template dialog you want to copy frequently, you can create a bookmark for that too.

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

---

## The Instant Delete Button

When you duplicate a dialog, or use the `/dialog_` route to auto-name a new dialog, the copy has a name ending in `_dup` followed by a number (e.g., `scratch_dup3`).

Dialogs with this naming pattern have a special **instant delete** button (a bomb icon 💣) that appears in the menu. They can also be deleted merely by pushing `d`. This makes it quick to clean up duplicates you no longer need.

Dialogs that *don't* follow this naming pattern won't show the instant delete button — this protects your original dialogs from accidental deletion.

---

## Quick Reference

| Goal | URL Pattern |
|------|-------------|
| New dialog at root | `/dialog_` |
| New dialog in folder | `/dialog_?name=folder/subfolder` |
| New dialog with a specific name | `/dialog_?name=folder/dlgname` |
| Duplicate existing dialog | `/dup_?name=path/to/dialog` |

---

## Editing a Bookmark Later

If you need to change a bookmark's URL:

1. Right-click the bookmark
2. Click **"Edit..."**
3. Modify the URL field
4. Click **Save**
