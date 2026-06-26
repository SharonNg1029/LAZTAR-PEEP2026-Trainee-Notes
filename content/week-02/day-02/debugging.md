+++
title = "Debugging Skills Notes"
weight = 3
+++

### 1. AI-Assisted Debugging

Using AI tools (like Antigravity, Gemini, ChatGPT...) accelerates identifying and fixing bugs:
- **Share logs directly:** Paste the exact stack trace or error message into the AI prompt.
- **Provide context:** Share the file containing the error alongside the trace.
- **Ask for the root cause:** Ask the AI to analyze the underlying architecture issue rather than just a quick fix.
- **Prompt Example:** "Explain the following error: `[error message]`. Here is the related code: `[paste code]`. What is causing this and how do I resolve it?"

---

### 2. Best Practices for Console Logs

Console logging (`console.log`) is simple but needs discipline:
- **Use labeled logs:** Always add a clear label so you can track where the log is printed.
  * *Bad:* `console.log(data);`
  * *Good:* `console.log(">>> Auth API Response:", data);`
- **Use specialized console methods:**
  * `console.error()`: Highlights errors in red.
  * `console.warn()`: Displays warnings in yellow.
  * `console.table()`: Renders arrays or objects in a clean table view.
- **Production rule:** **Always remove console logs before pushing to production.** Leftover logs can cause performance degradation and leak sensitive credentials.

---

### 3. Breakpoints

Using debugger breakpoints (via VS Code, Chrome DevTools, Xcode) pauses execution to inspect the application state:
- **How it works:** When code execution hits a breakpoint, the engine pauses. You can inspect all active variables in the variables scope panel without adding logs.
- **Stepping through code:**
  * *Step Over:* Move to the next line.
  * *Step Into:* Enter the function call on the current line.
  * *Step Out:* Complete the current function and return to the caller.
- **Conditional Breakpoint:** Pauses execution only when a specified expression is true. Helpful for debugging loops (e.g., pause only when `index === 99`).
- **Logpoint:** Prints a message to the console without modifying your actual source files.

---

### 4. Reading a Stack Trace

A stack trace represents the active call stack when an unhandled exception occurs.

* **Steps to read:**
  1. **Identify the error type:** Look at the top line to understand what went wrong (e.g., `TypeError: Cannot read properties of undefined (reading 'map')`).
  2. **Find user-written files:** Ignore lines pointing to `node_modules` libraries. Look for the top-most line referencing your project files (e.g., `at OnboardingScreen.tsx:45:12`).
  3. **Trace the call flow:** Read the stack trace from top to bottom to follow the function call sequence leading to the crash.
