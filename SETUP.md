# 🛠️ Tier-1 C Development Environment Setup (Windows)

**Goal:** Create a professional, "Systems Engineering" grade environment for C development on Windows.

**Constraints:**
- ✅ **No "Run Buttons"** — We control the build process explicitly
- ✅ **Strict ISO C11 Compliance** — Industry-standard language version
- ✅ **Zero Warnings Allowed** — All warnings treated as errors (`-Werror`)
- ✅ **Unified Toolchain** — Single, conflict-free compiler installation

**Toolchain:** `w64devkit` (Portable GCC + GDB + Make) via VS Code

---

## 🛑 Phase 0: The "Clean Slate" Protocol

**Why This Matters:** Multiple C compilers on your system can cause "path conflicts," where the wrong compiler runs, bypassing your strict flags. We must eliminate all conflicting installations first.

### Steps to Remove Old Compilers:

1. Press `Windows Key`, type **"env"**, and select **"Edit the system environment variables"**
2. Click **"Environment Variables..."**
3. In the **System variables** section (bottom panel), find **Path** and click **Edit**
4. **Carefully scan the entire list** and **DELETE** any entries containing:
   - `MinGW` or `MinGW-w64`
   - `Strawberry Perl` (includes a separate GCC)
   - `cygwin` or `cygwin64`
   - `msys2` or `msys64`
   - Any other `gcc` or `g++` paths

5. Repeat step 3-4 for **User variables** (top panel)
6. Click **OK** on all windows to save
7. **Restart your computer** to ensure changes take effect

> **⚠️ Critical:** If you skip this step, VS Code may randomly use the wrong compiler, and your strict flags won't work.

---

## 📥 Phase 1: Install the Toolchain (w64devkit)

**Why w64devkit?**
- ✅ **Portable:** No installer, no registry modifications, no bloat
- ✅ **Complete:** Includes GCC (compiler), GDB (debugger), and Make (build automation)
- ✅ **Modern:** Provides up-to-date GCC with full C11/C17 support
- ✅ **Clean:** Designed to avoid PATH conflicts

### Installation Steps:

1. **Download:**
   - Visit: [w64devkit Releases](https://github.com/skeeto/w64devkit/releases)
   - Download the latest `.zip` file (e.g., `w64devkit-1.xx.0.zip`)

2. **Extract:**
   - Extract the downloaded `.zip` to your `C:\` drive
   - Final path should be: `C:\w64devkit\`
   - Inside, you should see: `bin\`, `include\`, `lib\`, etc.

3. **Add to System PATH:**
   - Open **Environment Variables** again (same as Phase 0)
   - Edit **System variables → Path**
   - Click **New** and add: `C:\w64devkit\bin`
   - **CRITICAL:** Click **Move Up** repeatedly until this entry is **at the very top** of the list
   - This ensures Windows finds our compiler first

4. **Verify Installation:**
   - Open a **new** Command Prompt (type `cmd` in Start menu)
   - Run: `where gcc`
   - **Expected output:** Only one line showing `C:\w64devkit\bin\gcc.exe`
   - Run: `gcc --version`
   - **Expected output:** Should show GCC version 13.x or higher

> **✅ Success Check:** If `where gcc` shows multiple paths or the wrong path, revisit Phase 0 and remove conflicting entries.

---

## ⚙️ Phase 2: VS Code "Systems" Configuration

We will configure VS Code to **reject buggy code at compile-time** using strict compiler flags. This is how professional embedded systems and kernel developers work.

### 1. Create the Workspace

1. Create a folder on your system: `C:\Users\YourName\C_DSA_Mastery` (or any location you prefer)
2. Open VS Code
3. **File → Open Folder** → Select `C_DSA_Mastery`
4. Install the **C/C++ Extension** by Microsoft:
   - Press `Ctrl + Shift + X` to open Extensions
   - Search for: `C/C++`
   - Install the extension by Microsoft (should have 50M+ downloads)

### 2. Configure the Build System (`tasks.json`)

This file defines **how** VS Code compiles your C code. We enable industry-standard strict flags.

**What Each Flag Does:**
- `-g` → Embeds debug symbols for GDB (lets you inspect variables)
- `-std=c11` → Enforces C11 standard (no compiler-specific extensions)
- `-Wall` → Enables all common warnings
- `-Wextra` → Enables additional warnings beyond `-Wall`
- `-Werror` → **Treats all warnings as errors** (code won't compile if there are warnings)

**Setup:**
1. In VS Code, create a new folder: `.vscode` (inside your workspace root)
2. Inside `.vscode`, create a file: `tasks.json`
3. **Paste this configuration:**

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "cppbuild",
            "label": "Build with GCC (Strict)",
            "command": "gcc",
            "args": [
                "-g",                    // Add debug info for GDB
                "-std=c11",              // Use C11 standard
                "-Wall",                 // Enable All Warnings
                "-Wextra",               // Enable Extra Warnings
                "-Werror",               // Treat Warnings as Errors (Industry Standard)
                "${file}",               // The file you are editing
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": ["$gcc"],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "Compiles with strict flags to prevent buggy code."
        }
    ]
}
```

### 3. Configure the Debugger (`launch.json`)

This allows you to:
- **Step through code** line-by-line (F10)
- **Inspect variables** and memory addresses in real-time
- **View the call stack** when your program crashes
- **Set breakpoints** to pause execution at specific lines

**Setup:**
1. Inside `.vscode`, create a file: `launch.json`
2. **Paste this configuration:**

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug with GDB",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": true,         // Automatically pauses at main() start
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,    // Use VS Code's integrated terminal
            "MIMode": "gdb",
            "miDebuggerPath": "C:\\w64devkit\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "Build with GCC (Strict)"
        }
    ]
}
```

> **Note:** The `preLaunchTask` automatically runs the build task before debugging, so you don't need to build manually.

---

## 🧪 Phase 3: The Validation Test

Let's verify that the strict compilation mode is working correctly. This test intentionally includes buggy code that should **fail to compile**.

### Test 1: Intentional Build Failure (Verifying Strict Mode)

1. Create a file named `main.c` in your workspace root
2. Paste this code:

```c
#include <stdio.h>

int main() {
    int x; // Unused variable -> Should trigger -Werror=unused-variable
    printf("Tier-1 System Check: Online\n");
    return 0;
}
```

3. Press **`Ctrl + Shift + B`** to build
4. **Expected Result:** Build should **FAIL** with error:
   ```
   error: unused variable 'x' [-Werror=unused-variable]
   ```

> **✅ If it fails:** Your strict mode is working! This is the correct behavior.  
> **❌ If it succeeds:** Your `-Werror` flag is not active. Double-check your `tasks.json` file.

### Test 2: Successful Build (Clean Code)

1. Fix the code by using the variable:

```c
#include <stdio.h>

int main() {
    int x = 42;
    printf("Tier-1 System Check: Online. Value: %d\n", x);
    return 0;
}
```

2. Press **`Ctrl + Shift + B`** to build
3. **Expected Result:** Build should **SUCCEED** with:
   ```
   Build finished successfully.
   ```

### Test 3: Running the Debugger

1. Press **`F5`** to start debugging
2. **Expected Behavior:**
   - The program should compile automatically
   - Execution should **pause** at the first line of `main()`
   - You should see the Debug toolbar at the top of VS Code
   
3. **Try these debugger controls:**
   - **F10** (Step Over) — Execute the current line and move to the next
   - **F11** (Step Into) — Step into function calls
   - **F5** (Continue) — Run until the next breakpoint or program end
   - **Shift + F5** (Stop) — Terminate the debugger
   
4. **Inspect the variable:**
   - Hover your mouse over `x` in the code
   - You should see a tooltip showing: `x = 42`

> **✅ Success:** If you can step through the code and see variable values, your debugger is working correctly!

---

## 🚀 Daily Development Workflow

Now that everything is set up, here's how to work efficiently every day.

### Method 1: Terminal Workflow (Recommended for Learning)

This method builds essential "systems thinking" — you see exactly what commands are running. This is how professional C developers work in production environments.

1. **Build:** Press `Ctrl + Shift + B`
   - This compiles your code using the strict flags
   - Check the Terminal panel for any errors
   
2. **Run:** Open the integrated terminal with **Ctrl + `** (backtick key, usually below ESC)
   - Type: `.\main.exe`
   - Press Enter to run your program
   
3. **Iterate:** Make changes, rebuild with `Ctrl + Shift + B`, run again

> **Pro Tip:** The backtick key (`) is located below the Escape key on most keyboards.

### Method 2: Debug Mode (For Investigating Issues)

Use this when your program logic is broken or you need to inspect pointers, arrays, or complex data structures.

1. **Start Debugging:** Press `F5`
   - Automatically builds and launches with GDB
   - Pauses at the first line of `main()`
   
2. **Debug Controls:**
   - **F10** — Step Over (execute current line, move to next)
   - **F11** — Step Into (enter function calls)
   - **Shift + F11** — Step Out (return from current function)
   - **F5** — Continue (run until next breakpoint)
   - **Shift + F5** — Stop Debugging
   
3. **Set Breakpoints:**
   - Click in the left margin (gutter) next to any line number
   - Red dot appears → program will pause there during execution
   
4. **Inspect Variables:**
   - Hover over any variable to see its value
   - Check the **Variables** panel (left sidebar during debugging)
   - Use the **Debug Console** to evaluate expressions like `x + 5`

### Method 3: Quick Run Without Debugging

Use this for simple programs when you don't need to inspect anything.

- **Run Without Debugging:** Press `Ctrl + F5`
- Builds and runs immediately without pausing

---

## 🚫 Critical Rules

### ❌ NEVER Install "Code Runner" Extension

Many beginners install the "Code Runner" extension thinking it will make life easier. **Don't do this.** Here's why:

- ❌ Bypasses your `tasks.json` configuration
- ❌ Ignores your strict compiler flags (`-Werror`)
- ❌ Allows buggy code to compile (defeating the entire purpose)
- ❌ Uses a different compiler if multiple are installed
- ❌ No control over compilation process

**We explicitly control the build process** through `tasks.json`. This is professional practice.

### ✅ The Correct Approach

- ✅ Always use `Ctrl + Shift + B` to build
- ✅ Always use `F5` for debugging
- ✅ Always use `Ctrl + F5` for quick runs
- ✅ Trust the build system we've configured

---

## 🔧 Troubleshooting

### Problem: "gcc is not recognized as an internal or external command"

**Solution:**
1. Verify `C:\w64devkit\bin` is in your System PATH (Environment Variables)
2. Make sure it's at the **top** of the PATH list
3. **Restart VS Code** completely (close all windows and reopen)
4. Open a **new** terminal in VS Code and run: `where gcc`

### Problem: Build succeeds even with unused variables

**Solution:**
1. Check your [tasks.json](d:\C_DSA_Mastery\.vscode\tasks.json) includes `-Werror`
2. Verify you're using `Ctrl + Shift + B` to build (not a different method)
3. Make sure no other extensions are interfering (disable Code Runner if installed)

### Problem: Debugger won't start or shows "Unable to start debugging"

**Solution:**
1. Verify the path in [launch.json](d:\C_DSA_Mastery\.vscode\launch.json): `"miDebuggerPath": "C:\\w64devkit\\bin\\gdb.exe"`
2. Make sure the `.exe` file was created by building first (`Ctrl + Shift + B`)
3. Check that `preLaunchTask` matches your task label exactly: `"Build with GCC (Strict)"`

### Problem: Multiple GCC versions showing up

**Solution:**
1. Run `where gcc` in Command Prompt
2. If you see multiple paths, revisit Phase 0 and remove all conflicting entries
3. Only `C:\w64devkit\bin\gcc.exe` should appear
4. Restart your computer after making PATH changes

---

## 📚 Next Steps

Your environment is now production-ready! You can:

1. **Start Learning C:** Focus on algorithms and data structures without worrying about setup
2. **Write Strict Code:** Your compiler will catch common mistakes automatically
3. **Debug Like a Pro:** Use GDB to understand exactly what your code is doing at the CPU level
4. **Build Good Habits:** Clean compilation with zero warnings is a professional standard

**Remember:** Every warning is a potential bug. `-Werror` forces you to write cleaner code from day one.

---

**📌 Pro Tip:** Bookmark this file and keep it in your workspace. Whenever you set up a new machine or help a classmate, you'll have the complete setup guide ready to go.

---

*Last Updated: January 2026*