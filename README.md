# 🐧 Linux Kernel Process Utilities (kworker)

A collection of efficient Bash shell scripts designed to monitor and report on **kworker** processes. These threads are essential components of the Linux kernel, responsible for handling background tasks and work queues.

---

## 🔢 `mykworkscript`: Count kworker Processes

This script provides an **efficient and direct count** of all currently running kernel worker threads (`kworker`) on the system. It uses pipes to streamline the process and avoid unnecessary file operations.

### **🎯 Goal**
To provide a fast and accurate numerical count of background kernel activity as a quick system health check.

### **⚙️ Execution & Logic**

The script executes a powerful pipeline to achieve its result without creating any temporary files:

```bash
#!/bin/sh
# The number of kworker processes is:
ps ax | grep "kworker" | wc -l
```
Command, Purpose
ps ax, Lists all currently running processes on the system.
`,"grep ""kworker""`"
`,wc -l`

💡 Why This Method is Efficient
This method showcases pipeline efficiency. Instead of relying on slow disk I/O (input/output) to save data to a temporary file (>), the pipe (|) immediately feeds the output of one command into the next command's input, making the script faster and cleaner.

📂 sortProcesses: List and Sort kworker PIDs
This script lists all active kworker threads and sorts them specifically by their Process ID (PID) in reverse numerical order (largest to smallest).

🎯 Goal
To provide a clear, prioritized view of running kernel threads, which is highly useful for system diagnostics and identifying potential issues related to process identifiers.

⚙️ Execution & Logic
The operation is performed in a single, focused pipeline:
```
#!/bin/sh
ps ax | grep "kworker" | sort -k 1 -n -r
```

Command,Purpose
`ps ax,"grep ""kworker""`"
`,sort -k 1 -n -r`
-k 1, Sorts using the first column (which contains the PID).
-n, Treats the sort keys as numbers (numeric sort).
-r, Sorts in reverse order (largest PID to smallest PID).

------------------------------------------------------------------------------------------------------
Created by Tyler Fortune - October 30th, 2025
