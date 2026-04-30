# github-sandbox

# 📥 Download Files via Commit Message

A GitHub Actions workflow that lets you download files into your repository just by writing a special commit message — no terminal or command line needed
--
## ⚙️ Setup
0. Fork this repo
1. Go to your repository on GitHub
2. Click **Settings** → **Actions** → **General**
3. Scroll down to **Workflow permissions**
4. Select **Read and write permissions** and click **Save**

That's it — no tokens or secrets needed.
---

## 🚀 Usage

You trigger downloads by editing any file directly on GitHub and using a special commit message when saving.

### How to trigger a download

1. Open any file in your repository on GitHub (for example, this `README.md`)
2. Click the **pencil icon** (✏️) at the top right to edit it
3. Make any small change (add a space, a blank line, anything)
4. Scroll down to the **Commit changes** section
5. Select **Commit directly to the `main` branch**
6. In the commit message box, type one of the commands below
7. Click **Commit changes**

The workflow will run automatically and the downloaded files will appear in the `downloads/` folder.

---

## 📝 Commands

### Download files individually

Downloads each file and saves it by its original filename.

```
download: URL1 URL2 URL3
```

**Examples:**
```
download: https://productionresultssa0.blob.core.windows.net/actions-results/1bdfd299-12d9-43cc-9024-d1cc75769e06/workflow-job-run-2aae21c0-e6bf-5015-8903-72bb43d06304/artifacts/cc5963e1ab0f423d93fbf22f85bdcc9a62e5093b49654e0731ec4ce4bcf89e52.zip?rscd=attachment%3B+filename%3D%22BluSpoofer-debug.zip%22&rsct=application%2Fzip&se=2026-04-30T18%3A28%3A39Z&sig=mamas4qzUlDE4YmCfK59vayEwjwOi3a7W8Fs%2FMvfKTg%3D&ske=2026-04-30T21%3A32%3A01Z&skoid=ca7593d4-ee42-46cd-af88-8b886a2f84eb&sks=b&skt=2026-04-30T17%3A32%3A01Z&sktid=398a6654-997b-47e9-b12b-9515b896b4de&skv=2025-11-05&sp=r&spr=https&sr=b&st=2026-04-30T18%3A18%3A34Z&sv=2025-11-05
```

```
download: https://example.com/a.zip https://example.com/b.pdf https://example.com/c.zip
```

---

### Download and archive into a single ZIP

Downloads all files and bundles them into one timestamped `.zip` archive saved to `downloads/`.

```
download-zip: URL1 URL2 URL3
```

**Examples:**

```
download-zip: https://example.com/file.zip
```

```
download-zip: https://example.com/a.zip https://example.com/b.pdf https://example.com/c.zip
```

The resulting archive will be named like: `archive_20250423_153012.zip`

---

## 📁 Output

| Command | Result |
|---|---|
| `download:` | Each file saved individually in `downloads/` with its original name |
| `download-zip:` | All files bundled into a single `archive_YYYYMMDD_HHMMSS.zip` in `downloads/` |

---

## 👀 Checking the result

After committing, you can monitor the workflow:

1. Click the **Actions** tab in your repository
2. Click the latest workflow run to see progress and logs
3. Once it completes, go back to the **Code** tab and open the `downloads/` folder to find your files

---

## ⚠️ Notes

- URLs must be publicly accessible (no login required)
- Separate multiple URLs with spaces
- The workflow skips itself using `[skip ci]` in its own commit message to avoid infinite loops
- If no valid `download:` or `download-zip:` command is found in the commit message, the workflow will exit without doing anything
