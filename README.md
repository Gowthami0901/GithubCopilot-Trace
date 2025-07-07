# GitHub Copilot Traces in VS Code

### Step 1: Ensure GitHub Copilot Extension is Installed

1. Open **VS Code**
2. Go to the **Extensions panel** (`Ctrl+Shift+X`)
3. Search for and install:

   * **GitHub Copilot**
   * **GitHub Copilot Chat**
   * 
4. Make sure both extensions are **enabled**

---

### Step 2: Enable Trace Logging via `settings.json` (Persistent Method)

1. Press `Ctrl+Shift+P` → Search: **`Preferences: Open Settings (JSON)`**
2. Add this block (merge into your existing settings if needed):

```json
{
  "github.copilot.logLevel": "trace",
  "github.copilotChat.logLevel": "trace",
  "github.copilot.advanced": {
    "debug.logging": true,
    "debug.telemetry": true
  }
}
```

> This enables trace-level logging every time VS Code starts.

---

### Step 3: Restart VS Code

* **Close all windows** of VS Code
* **Reopen** to apply the new log settings

---

### Step 4: Enable Trace Logging via Command Palette

This sets the log level **instantly**, valid for the current session:

1. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS)
2. Type: **`Developer: Set Log Level`**
3. Select `Trace` from the dropdown

Now, all extensions (including Copilot) log at trace level until VS Code is closed.

---

### Step 5: View Logs in the Output Panel

1. Press `Ctrl+Shift+P` → Type: **`Output: Show Output Channels`**
   *(Or use menu: View → Output)*
2. In the **dropdown list** in the Output panel (top-right corner):

   * Choose **`GitHub Copilot`**
   * Or **`GitHub Copilot Chat`**

---

### Step 6: Check for Trace Logs

Start typing code (e.g., `def greet(name):`) to trigger Copilot.
Then look for trace-like entries in the Output panel:

```
[trace] Sending request to Copilot...
[trace] Prompt: def greet(name):
[trace] Completion: return f"Hello, {name}"
```

> If you see only `[info]`, that’s also fine—Copilot is working.

---

### Step 7: (Optional) Use Developer Tools for Full Internal Logs

1. Press `Ctrl+Shift+P` → Run: **`Developer: Toggle Developer Tools`**
2. Click the **Console** tab
3. Trigger Copilot completions → you’ll see raw logs, including request/response, model metadata, token count, etc.

---

### Switch Between Copilot Log Channels

In the **Output panel dropdown**, you can switch between:

* `GitHub Copilot` (main suggestions)
* `GitHub Copilot Chat` (chat features)

---

### Log Type Reference

| Log Type    | Description                                    |
| ----------- | ---------------------------------------------- |
| `[trace]`   | Full request/response details (prompt, tokens) |
| `[info]`    | Basic events (completion fetched, chat loaded) |
| `[warning]` | Non-critical issues (e.g., fallback used)      |
| `[error]`   | Critical errors or failed requests             |

---

## Notes

* GitHub limits trace output for privacy and performance. You may not see full `[trace]` in the Output panel, but detailed logs often appear in **Developer Tools Console**.
* This is helpful when working with **Copilot Chat**, **slow responses**, or **debugging model behavior**.
* All logs are **local** unless telemetry is manually enabled.
