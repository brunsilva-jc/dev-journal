# How to Create and Use Shell Scripts in Linux

Creating your own scripts in Linux can boost your productivity and simplify repetitive tasks. This guide walks you through the steps of creating a simple shell script to extract IP addresses from log files.

---

## Step 1: Create a `bin` Directory

For better organization, we start by creating a `bin` directory in the home folder:

```bash
mkdir ~/bin
cd ~/bin
```

---

## Step 2: Create the Script File

Create a new shell script file called `extract_ips.sh`:

```bash
touch extract_ips.sh
```

Now open it using `vim`, `nano`, or any editor of your choice, and paste the code below:

```bash
#!/bin/bash

if [ -z "$1" ]; then
    echo "Usage: $0 <filename> [--count]"
    exit 1
fi

if [ "$2" == "--count" ]; then
    # Extract and count unique IPs
    grep -Eo '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' "$1" | sort | uniq -c | sort -nr
else
    # Just extract IPs
    grep -Eo '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' "$1"
fi
```

---

## Step 3: Script Explanation

- The script uses `grep` to extract IP addresses from a given log file.
- If `--count` is passed as an argument, it counts unique IPs.
- Otherwise, it simply extracts them.

### Breakdown:

- `$0` — name of the script
- `$1` — the filename (mandatory)
- `$2` — optional flag (`--count`) to count unique IPs
- `-z "$1"` — checks if the first argument is empty

---

## Step 4: Make the Script Executable

Run the command below to make your script executable:

```bash
chmod +x extract_ips.sh
```

---

## Step 5: Run the Script

You can now run the script on any log file:

```bash
./extract_ips.sh /path/to/file.log
```

Or count the unique IPs:

```bash
./extract_ips.sh /path/to/file.log --count
```

---

## Step 6: Make the Script Available System-wide

To use your script from anywhere, add the `bin` directory to your system `PATH`:

```bash
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

---

## That's It!

Now you can call your script from any location:

```bash
extract_ips.sh file.log
extract_ips.sh /path/to/file.log
```
