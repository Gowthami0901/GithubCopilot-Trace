# GitHub Copilot Traces in VS Code

### Step 1: Ensure GitHub Copilot Extension is Installed

1. Open **VS Code**
2. Go to the **Extensions panel** (`Ctrl+Shift+X`)
3. Search for:

   * **GitHub Copilot**
   * *(Optional)* **GitHub Copilot Chat**
    
4. Install and **enable** both if not already

---

### Step 2: Enable Trace Logging in `settings.json`

1. Press `Ctrl+Shift+P` → Search for:
   **`Preferences: Open Settings (JSON)`**
2. Add the following configuration:

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

> If your file already has settings, insert commas appropriately.

---

### Step 3: Restart VS Code

After editing `settings.json`:

* Fully close and reopen **VS Code** to apply changes.

---

### Step 4: Open Output Panel to View Logs

1. Go to: **View → Output**
2. In the **dropdown menu** (top-right), select:

   * ✅ `GitHub Copilot`
   * ✅ `GitHub Copilot Chat`

---

### Step 5: Check for Trace Logs

When Copilot is triggered (e.g., by typing code like `def greet(name):`), you should see:

```
[trace] Sending request to Copilot...
[trace] Prompt: def greet(name):
[trace] Completion: return f"Hello, {name}"
```

If you only see `[info]` or no trace entries, go to Developer Tools.

---

### Step 6: (Optional) Use Developer Tools for Raw Logs

1. Press `Ctrl+Shift+P`
2. Run: **`Developer: Toggle Developer Tools`**
3. Click the **Console** tab
4. Interact with Copilot → Trace and API logs will appear here too

---

### Expected Log Types

| Log Type    | Meaning                                      |
| ----------- | -------------------------------------------- |
| `[trace]`   | Full details of request, prompt, token usage |
| `[info]`    | Basic operation status (working, idle, etc.) |
| `[warning]` | Something didn’t go as expected              |
| `[error]`   | Critical failure or API issue                |

---

### Notes

* Trace logs **help debug completions** by showing prompt/response round trips.
* They’re especially helpful when working with **custom APIs, Copilot Chat**, or **slow completions**.
* These logs are **local** — nothing is sent to GitHub for debugging unless you opt in.

