# WiFi Password Extractor

A simple Python script that retrieves all saved WiFi profiles and their passwords from a Windows machine using the built-in `netsh` command.

## Requirements

- **OS:** Windows only
- **Python:** 3.x
- **Privileges:** Must be run as Administrator

## How It Works

The script uses Windows' `netsh` command-line utility in two steps:

1. **Fetch profiles** — runs `netsh wlan show profiles` to list all saved WiFi network names.
2. **Fetch passwords** — for each profile, runs `netsh wlan show profile <name> key=clear` to reveal the stored plaintext key (password).

Results are printed in a formatted table to the console.

## Usage

1. Open **Command Prompt** or **PowerShell** as Administrator.
2. Run the script:
   ```
   python wifi_passwords.py
   ```
3. The output will look like:

```
NetworkName                   |  Password
AnotherNetwork                |  mypassword123
HiddenNetwork                 |
```

- A **blank password** means the network has no password or it could not be retrieved.
- **ENCODING ERROR** means `netsh` returned a non-zero exit code for that profile (e.g., insufficient permissions).

## Notes

- This script only works on **Windows** — `netsh` is not available on macOS or Linux.
- Administrator privileges are required to retrieve key content.
- This tool is intended for **recovering your own saved passwords** on your own machine.

## Disclaimer

Use this script responsibly and only on devices you own or have explicit permission to access. Unauthorized retrieval of network credentials may be illegal.
