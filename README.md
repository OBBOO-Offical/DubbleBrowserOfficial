# 🎮 DubbleBrowser — Game Dev Edition

A Chrome-style desktop browser built for game developers.
- **Search engine**: DuckDuckGo with strict safe search enforced
- **Content filter**: Blocks adult sites, gambling, gore, and inappropriate search terms
- **Game dev bookmarks**: Unity, Unreal, Godot, GitHub, itch.io, and more
- **Built on**: .NET 8 + Microsoft WebView2 (real Chromium engine)

---

## ✅ Requirements

| Requirement | Details |
|---|---|
| OS | Windows 10 or 11 (64-bit) |
| .NET 8 SDK | https://dotnet.microsoft.com/download/dotnet/8.0 |
| WebView2 | Already built into Windows 10/11 — no install needed |

---

## 🚀 Run in Dev Mode

```bash
dotnet run
```

---

## 📦 Build Standalone .exe

```bash
dotnet publish -c Release -r win-x64 --self-contained
```

Your `.exe` will be at:
```
bin\Release\net8.0-windows\win-x64\publish\DubbleBrowser.exe
```

Copy just that folder and distribute it — no .NET install required on end-user machines.

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl+T` | New tab |
| `Ctrl+W` | Close tab |
| `Ctrl+L` | Focus address bar |
| `Ctrl+R` / `F5` | Reload |
| `Ctrl+Tab` | Next tab |
| `Ctrl+Shift+Tab` | Previous tab |
| `Ctrl+1–9` | Switch to tab N |
| `F12` | Open DevTools |
| `Esc` | Stop loading |

---

## 🛡️ Content Filter

Edit `ContentFilter.cs` to customize:
- **`BlockedDomains`** — add/remove blocked website domains
- **`BlockedKeywords`** — add/remove blocked search terms
- DuckDuckGo safe search is always enforced via `&kp=1` parameter

---

## 🔌 JS ↔ C# Bridge (for Game Devs)

Post a message from a web page to your C# code:
```js
window.chrome.webview.postMessage("myEvent:someData");
```

Receive it in C#:
```csharp
webView.CoreWebView2.WebMessageReceived += (s, e) => {
    var msg = e.TryGetWebMessageAsString();
    // handle msg
};
```

Send from C# to the web page:
```csharp
webView.CoreWebView2.PostWebMessageAsString("hello from C#");
```
