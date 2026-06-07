# Python-Security-Scanner


## Introduction

Python is one of the most popular programming languages in the world. However, running unknown Python scripts from the internet can be risky because they may contain commands that execute system operations, download malicious files, or access sensitive information.

This project provides a simple security scanner that analyzes Python source code and detects potentially dangerous functions before execution.

## Features

* Scan Python source files
* Detect dangerous functions
* Simple and lightweight
* Beginner-friendly code
* Useful for code review

## Dangerous Patterns

The scanner looks for:

* os.system()
* subprocess module
* eval()
* exec()
* socket module
* requests module

## Source Code

```python
import re
from pathlib import Path

DANGEROUS_PATTERNS = {
    r"os\.system": "System command execution",
    r"subprocess\.": "Subprocess execution",
    r"eval\(": "Dynamic code execution",
    r"exec\(": "Code execution",
    r"socket\.": "Network communication",
    r"requests\.": "HTTP requests"
}

def scan_file(filename):
    content = Path(filename).read_text(
        encoding="utf-8",
        errors="ignore"
    )

    findings = []

    for pattern, description in DANGEROUS_PATTERNS.items():
        if re.search(pattern, content):
            findings.append(description)

    return findings

if __name__ == "__main__":
    file_path = input("Python file: ")

    results = scan_file(file_path)

    if results:
        print("\nPotential Risks Found:\n")

        for item in results:
            print("[!] " + item)
    else:
        print("\nNo suspicious patterns detected.")
```

## Example Output

```text
Python file: malware.py

Potential Risks Found:

[!] System command execution
[!] HTTP requests
```

## How It Works

The scanner reads a Python source file and searches for predefined regular expression patterns. If suspicious functions are found, they are reported to the user before the file is executed.

## Future Improvements

* Recursive folder scanning
* Malware scoring system
* HTML reports
* GUI application
* Machine learning detection

## License

MIT License
