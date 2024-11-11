# Remote File Transfer and RDP Session Script

This script facilitates secure file transfers from a remote Linux server to a local machine and supports RDP (Remote Desktop Protocol) sessions to Windows servers with drive mapping. Based on the selected server type, the script initiates an RDP session (for Windows) or recursively downloads specified files and directories (for Linux).

## Features

- **Windows RDP Session**: Connects via `xfreerdp`, allowing drive mapping between local and remote Windows servers.
- **Linux File Transfer**: Uses SSH and SCP to securely transfer files or directories from a Linux server.
- **Progress Indicator**: Displays a loading animation during transfers and provides clear success or error messages.

## Requirements

- **Linux Environment**: Designed to be run from a Linux machine.
- **Dependencies**:
  - `expect`: For automating password input and handling SSH/SCP interactions.
  - `xfreerdp`: For RDP connections to Windows servers.

To install `expect` and `xfreerdp` (Debian-based systems):
```bash
sudo apt-get update
sudo apt-get install expect xfreerdp
```

## Usage

1. **Run the Script**:
   ```bash
   ./script.sh
   ```

2. **Select Remote Server Type**:
   - **Windows (w)**: Establishes an RDP session with a mapped drive.
   - **Linux (l)**: Downloads specified files and directories from the Linux server.

---

### Windows Workflow (RDP Session)

1. **Provide Connection Details**:
   - IP address
   - Username (defaults to `analyst` if left blank)
   - RDP password
   - Drive letter for mapping (e.g., `C`, `D`)
   - Local directory to map as a drive on the remote server

2. **Session Start**: The script initiates an RDP session using `xfreerdp`, mapping the specified local directory.

**Example**:
```plaintext
Is the remote machine Windows or Linux? (w/l): w
Enter the remote server IP address: 192.168.1.10
Enter the remote server username (default: analyst): AdminUser
Enter the RDP password: [password]
Enter the drive letter to map (e.g., 'C' for drive C): D
Enter the local destination directory for the drive mapping (e.g., /home/kali/letsdefend): /home/kali/letsdefend
```

### Linux Workflow (File Transfer)

1. **Provide Connection Details**:
   - Username (defaults to `analyst` if left blank)
   - IP address
   - Paths to files or directories (space-separated for multiple items)
   - Sudo password for root access (defaults to `123` if left blank)
   - Destination directory on the local machine

2. **File Transfer**:
   - The script connects to the Linux server, copies each specified file or directory to a temporary accessible location on the server, and transfers it to the local machine.
   - Each transfer is accompanied by a progress indicator.

**Example**:
```plaintext
Is the remote machine Windows or Linux? (w/l): l
Enter the remote server username (default: analyst): 
Enter the remote server IP address: 3.15.143.200
Enter the paths of the files or directories on the remote server, separated by spaces: /root/Desktop/ChallengeFile/sample.7z
Enter the password for sudo access on the remote server (default: 123): 
Enter the destination directory on the local machine (e.g., /home/kali/letsdefend): /home/kali/letsdefend
```

3. **Completion Message**:
   After transferring all files, the script outputs a message indicating successful completion.

## Output

- **Windows**: Opens an RDP session with drive mapping.
- **Linux**: Recursively downloads files or directories, providing minimal output and a completion message upon success or failure.

## Important Notes

- Ensure permissions on both the remote and local systems allow file transfer and access.
- The script uses automatic certificate acceptance for RDP connections (`/cert:ignore`).
- Run in trusted environments due to password handling in the script.

## License

This script is open-source and available under the MIT License.