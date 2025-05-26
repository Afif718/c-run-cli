# 🚀 c-run-cli

A simple shell function to compile and run C files directly from the terminal with a single command.

---

## 🔧 Setup

1. Open your `.bashrc` (on Linux) or Git Bash's `.bash_profile` (on Windows):

   ```bash
   nano ~/.bashrc
   ```

2. Paste the following code into the file:

   ```bash
   run() {
     if [ $# -eq 0 ]; then
       echo "❌ Please provide a .c file. Example: run hello.c"
       return 1
     fi

     file="$1"
     if [ ! -f "$file" ]; then
       echo "❌ File '$file' not found."
       return 1
     fi

     tmp_exe="temp_$$.exe"  # Unique temp executable using shell PID
     gcc "$file" -o "$tmp_exe"

     if [ $? -eq 0 ]; then
       ./"$tmp_exe"
       rm "$tmp_exe"
     else
       echo "❌ Compilation failed."
     fi
   }
   ```

3. Save and exit, then reload your shell:

   ```bash
   source ~/.bashrc
   ```

## ▶️ Usage

Navigate to the directory containing your `.c` file and run:

```bash
run examples/hello.c
```

- ✅ If compiled successfully, it runs immediately.
- ❌ If there's a compilation error, it displays an error message.

## 💡 Features

- ✅ Automatically compiles and runs C programs
- 🧹 Deletes the executable after execution
- ⚠️ Displays errors only when compilation fails
- ⚡ Fast and minimal

## 📁 Example Structure

```
c-run-cli/
├── examples/
│   └── hello.c
├── .bashrc-setup
└── README.md
```

## 📌 Requirements

- `gcc` installed and added to your system `PATH`
- Bash-compatible terminal (e.g., Git Bash, WSL, Linux shell)

## 💬 License

MIT License — feel free to use and modify.
