# AmogOs 🛸

A desktop operating system that runs right inside your web browser. No installs, no downloads, no server. The whole thing lives in **one HTML file**.

Made by [FallGameDev](https://youtube.com/@FallGameDev) at Here Studios.

---

## What can it do?

- **Accounts:** set up a new account, sign in from a lock screen, and switch between users.
- **Files:** a File Explorer with folders, image thumbnails, uploads, downloads, and delete.
- **Notes:** a text editor that saves straight into your files.
- **Paint:** draw with a color palette and brush sizes, then save pictures to your Pictures folder.
- **Comet:** the built-in web browser with a start page and an address bar.
- **Calculator:** for quick math.
- **Settings:** System info, Storage, Personalization, Accounts, Backup, and Activation.
- **Storage plans:** enter a product key to change how much drive space you have.
- **Backup and restore:** save everything to one password-protected file, then restore it later.

---

## Product keys and storage

When you set up your account (or later in **Settings > Activation**), you can type in a product key. The key decides how big your drive is. No key means 16 GB.

Product keys are private. They are only shared with friends by the creator, so please do not post them.

The drive fills up as you save files. When it is full, saving is blocked until you delete things or activate a bigger plan.

---

## Backup and restore

**To back up:** open **Settings > Backup**, type a password, and click **Back up now**. You get a `.json` file. The text is also shown in a box so you can copy it.

**To restore:** use **Settings > Backup > Restore from a backup**, or click **Restore from a backup** on the first setup screen. Pick the file (or paste the text) and type the same password.

Backups are locked with AES-256 encryption. If you forget the password, the backup cannot be opened, so keep it safe!

---

## How it works (for developers)

Everything is inside `amogos.html`: the HTML, the CSS, and the JavaScript. The code has comments so it is easy to read.

| Part | How it works |
| --- | --- |
| Accounts | Saved in `localStorage` under the key `amogos`. Passwords are hashed with SHA-256 and never stored as plain text. |
| Files | Stored as a flat object. Each path (like `/Documents/Welcome.txt`) points to `{ t, m, d }`: type, MIME type, and the file data as a base64 data URL. |
| Storage meter | Counts the size of your saved data and multiplies it so it feels like a real drive. Saves are refused if the drive is over its limit. |
| Backups | `PBKDF2` turns your password into a key, and `AES-GCM` encrypts the data (Web Crypto API). |
| Windows | Draggable, minimizable, and maximizable. Each app is a function that draws into a window body. |
| Browser app | Uses an `<iframe>`. Some websites do not allow being shown inside other pages, so they may look blank. |
| Sounds and icons | Icons are emoji. Sounds are made with the Web Audio API, so there are no extra files. |

### Adding a new app

1. Write a function that takes the window body and draws into it.
2. Add it to the `APPS` list with a name, an icon, and a starting size.

```js
{ n: 'MyApp', i: '⭐', r: (b) => myApp(b), w: 500, h: 360 }
```

The Start menu, taskbar, and window system pick it up automatically.

---

## Good to know

- Your data stays **in your browser only**. Clearing your browser data erases your accounts and files, so make a backup first.
- Browsers limit `localStorage` to a few megabytes. Big storage plans are only a number on screen, so the real limit is your browser's.
- Different browsers (or private windows) do not share data.

---

## Ideas for the future

- Real sound effects and a music player
- A terminal app
- Drag and drop files between folders
- Rename files
- More wallpapers and accent colors

---

## Credits

Built by **FallGameDev** at **Here Studios**.

- YouTube: [@FallGameDev](https://youtube.com/@FallGameDev)
- itch.io: [fallgamedev.itch.io](https://fallgamedev.itch.io)
