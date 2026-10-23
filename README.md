# 🛋️ CouchHotKeys
Media-PC Remote Hotkey Tool for Kodi & HTPC setups

<img width="1350" height="907" alt="Bild1" src="https://github.com/user-attachments/assets/3017eef0-a695-47fc-b4fa-95e3fad51534" />

<img width="1345" height="916" alt="Bild2" src="https://github.com/user-attachments/assets/77fa1b52-db99-41bf-9ff3-f5d27e2aa4e3" />

<img width="1348" height="918" alt="Bild3" src="https://github.com/user-attachments/assets/0733ae02-dacc-4930-a733-66bce499d357" />


## 📖 User Guide & Documentation

### 1. Getting started: create a macro
- Click **"+ New"** to create a new macro.
- Click **"🔍 Scan Key"** and press the desired key on your remote.
- Choose an action and click **"💾 Save Macro"**.

> 💡 *Only deleting takes effect immediately. All other changes apply after "Save Macro".*

---

### 2. Live status (key display)
The live status shows what CouchKey received last. It helps with learning keys and with troubleshooting.

**The lines mean:**
- **Device:** `"Couch"` or `"Main"` with the device path. `"Couch"` means the key comes from the remote, `"Main"` from the main keyboard.
- **Key:** `VK=… SC=…` for keyboard keys. `VK` is the Windows code of the key, `SC` the hardware code. Both values are decimal. *Example: VK=48 SC=11 is the digit 0.*
- **HID:** `…` for keys that do not go through the keyboard, e.g. volume, rewind or mail on the remote. The value is the raw report in hex. *Example: 01 B4 00 is rewind.*

> 💡 *After releasing a key, 01 00 00 appears (no key pressed). Read the value while you hold the key.*  
> 💡 *If the display does not change, no message has arrived.*

---

### 3. Learning keys (scan)
- The scan remembers the device and the key. The same key on your normal keyboard does not trigger the macro.
- The detected key appears in the **"Trigger"** field, for example: `D1 (Scan=2, HID#VID_4037…)`.
- If the key is already assigned, a notice appears and the existing macro is opened. Edit or delete it first, or choose another key.
- Scanning also works without a selected macro. The new macro is only created once a free key is detected.

---

### 4. Action: start a program or script
Enter the path or pick the file with **"Browse"**.

**Examples:**
- `E:\Kodi\kodi.exe -p` *(with parameter)*
- `"C:\Program Files\VideoLAN\VLC\vlc.exe" --fullscreen` *(path with spaces)*
- `C:\Scripts\monitor_tv.bat` *(script)*
- `notepad.exe` *(Windows program without full path)*

> ⚠️ **Paths with spaces need quotation marks.** Parameters go after the closing quotation mark.  
> 💡 *Programs without a full path are found by Windows search.*

---

### 5. Bring a window to the front instead of opening it again (Focus)
- `Focus{kodi}` brings Kodi to the front.
- `Focus{firefox}` switches to the browser.
- `Focus{thunderbird}` switches to the e-mail program.
- `Focus{explorer}` brings Explorer to the front, or opens it if no Explorer window is open.

> 💡 *The name is the process name without ".exe", as shown in Task Manager under "Details". If CouchKey finds no process, it searches by window title.*

---

### 6. Send a key combination
The input is sent to the currently active window.

- **Modifiers:** `+` = Shift, `^` = Ctrl, `%` = Alt
- **Special keys in curly braces:** `{ENTER}` `{ESC}` `{TAB}` `{BACKSPACE}` `{DELETE}` `{UP}` `{DOWN}` `{LEFT}` `{RIGHT}` `{HOME}` `{END}` `{PGUP}` `{PGDN}` `{F1}` to `{F12}`

**Examples:**
- `%{TAB}`: switch window (Alt+Tab)
- `%{F4}`: close window (Alt+F4)
- `^w`: close browser tab (Ctrl+W)
- `^+t`: reopen closed tab (Ctrl+Shift+T)
- `{F11}`: toggle full screen
- `{RIGHT 5}`: right arrow five times

> ⚠️ *The characters `+ ^ % ~ ( ) { }` have a special meaning. To send them as normal characters, put them in curly braces, for example `{+}`.*  
> ⚠️ *This action cannot send media keys such as volume or play/pause.*

---

### 7. Manage macros
- **Edit:** Click the macro in the list, change it, then click **"Save Macro"**.
- **Delete:** Select the macro and click **"Delete"**.
- **Export:** Back up all macros as a JSON file.
- **Import:** Load a JSON file. You decide whether to append the macros ("Yes"), replace the existing list ("No"), or cancel the import ("Cancel").

📁 **Storage location:** `%APPDATA%\CouchHotKeys\macros.json`

---

### 8. Solving problems
- **Macro does not react:** Was it saved? Is CouchKey running (tray icon)? Scan the key again.
- **The wrong window receives the keys:** First bring the target window to the front with `Focus{…}`.
- **"File not found":** Check the path and use quotation marks if it contains spaces.
- **Focus{…} finds nothing:** Check the process name in Task Manager under "Details".
- **Error details are in the log:** `%APPDATA%\CouchHotKeys\error.log`

---

### 9. Back up & restore macros
**Why back up?** Your macros are stored in a file on your PC. If it is lost (reinstalling Windows, a failing hard drive, accidental deletion), all macros are gone. A backup protects against that.

📤 **Back up (Export):**
- Click **"Export"** and choose a folder and file name.
- All macros are saved in a JSON file, for example `couchhotkeys_export_20261020_113000.json`.
- Keep the file somewhere safe, for example on a USB stick or in the cloud.

📥 **Restore (Import):**
- Click **"Import"** and choose the backup file.
- The app shows how many macros were found. Then you choose:
  - **Add:** The macros are appended to the existing list. Duplicate macros are skipped.
  - **Overwrite:** The existing list is replaced completely by the backup.
  - **Cancel:** Nothing is changed.
- After the import, the macros are saved immediately.

> ⚠️ *Overwriting removes the current macros. Export the current list first if you want to keep it.*  
> ⚠️ *Keys are tied to the device. On another PC or after replacing the remote, you need to scan the keys again.*  
> 💡 *Back up after larger changes, for example after creating several new macros.*

---

### 10. Input mode (K symbol)
The **K symbol** in the header determines what happens to the keys of the remote.

**There are two modes:**
1. **Pass key through (compatibility mode, default):** CouchKey runs the macro's action. The key also goes to the active program, for example an editor, where the character then appears. Recommended if you are unsure.
2. **Block key (couch mode):** The remote's keys are processed only by CouchKey. Windows and other programs do not receive the signal. This avoids double input.

> ⚠️ *In couch mode, a main keyboard key with the same scan code is blocked as well and triggers the macro. Nothing is blocked during a scan.*  
> 💡 *The choice is saved and stays after a restart.*

---

### 11. Appearance & language
- **Design:** 15 themes via the palette icon. They include "System" (follows the Windows mode) and two high-contrast themes for better readability.
- **Language:** 15 languages via the language icon, switchable at any time.

---

### 12. Background operation & autostart
- Minimizing hides CouchHotKeys in the notification area next to the clock. The macros stay active.
- Double-clicking the tray icon opens the window again. Right-clicking shows "Open" and "Exit".
- The autostart icon in the header starts CouchHotKeys with Windows, hidden in the background.
- If you close the window with the X, CouchHotKeys exits and the macros are no longer active.


System Requirements

    Windows 10 (version 1809 or later) or Windows 11, 64-bit
    Not supported: Windows 10 before 1809 and 32-bit Windows
    Windows on ARM: not tested
    No .NET installation required, the runtime is included in the folder

Starting

Start CouchHotKeys.exe. The folder can be copied to any location.

On first launch, Windows may show the warning
"Windows protected your PC", because the program is not signed.
Click "More info" and then "Run anyway".
Data

Macros and settings are stored in:
%APPDATA%\CouchHotKeys\macros.json
%APPDATA%\CouchHotKeys\error.log (error log)
Uninstalling

Delete the folder. Optionally delete %APPDATA%\CouchHotKeys as well.
