# Remote File Transfer and RDP Script

This script facilitates secure file transfer from a remote Linux server to a local machine or establishes an RDP (Remote Desktop Protocol) session to a Windows server with drive mapping functionality. Based on the server type (Windows or Linux), the script either opens an RDP session with a mapped drive or downloads files via SSH and SCP.

## Prerequisites

- **Linux Environment**: This script is designed to be run from a Linux environment.
- **Required Packages**:
  - `expect`: Automates SSH and SCP interactions.
  - `xfreerdp`: Used for RDP connections to Windows servers.
  
To install `expect` and `xfreerdp` on Debian-based systems:
```bash
sudo apt-get update
sudo apt-get install expect xfreerdp
```

## Usage

1. **Run the Script**
   ```bash
   ./script.sh
   ```
2. **Select Remote Server Type**  
   The script prompts for the type of remote machine:
   - **Windows (w)**: Opens an RDP session with a mapped drive.
   - **Linux (l)**: Initiates file transfer via SSH and SCP.
---

### Windows Workflow (RDP Session)

1. **Provide Connection Details**:
   - Remote server IP address
   - Remote server username
   - RDP password
   - Drive letter for mapping (e.g., `C`, `D`)
   - Local directory to map as a drive on the remote server
   
2. **Automatic Certificate Acceptance**:
   The script includes `/cert:ignore`, which bypasses certificate verification and allows the RDP connection without manual confirmation.

3. **Initiate RDP Session**:
   An RDP session opens, mapping the specified local directory as a drive in the remote Windows session.

**Example Input**:
```plaintext
Is the remote machine Windows or Linux? (w/l): w
Enter the remote server IP address: 192.168.1.10
Enter the remote server username: AdminUser
Enter the RDP password: [password]
Enter the drive letter to map (e.g., 'C' for drive C): D
Enter the local destination directory for the drive mapping (e.g., /home/kali/letsdefend): /home/kali/letsdefend
```

### Linux Workflow (File Transfer)

1. **Provide Connection Details**:
   - Remote server username
   - Remote server IP address
   - Paths to files on the remote server (multiple files can be specified with space-separated paths)
   - Sudo password for root access on the remote server
   - Destination directory on the local machine

2. **File Transfer Process**:
   - The script uses SSH to access the remote server, temporarily copies specified files, adjusts permissions, and transfers them via SCP to the local destination.
   - After transfer, the temporary file on the remote server is deleted.

**Example Input**:
```plaintext
Is the remote machine Windows or Linux? (w/l): l
Enter the remote server username: user123
Enter the remote server IP address: 192.168.1.20
Enter the paths of the files on the remote server, separated by spaces: /etc/passwd /etc/hosts
Enter the password for sudo access on the remote server: [password]
Enter the destination directory on the local machine (e.g., /home/kali/letsdefend): /home/kali/letsdefend
```

## Output

- **Windows**: Opens an RDP session with the local directory mapped as a drive.
- **Linux**: Copies each specified file to the designated local directory, providing success or failure feedback for each file.

## Important Notes

- Ensure you have the appropriate permissions on both the remote and local systems.
- The script includes automatic certificate acceptance (`/cert:ignore`) for Windows RDP connections, which is helpful for environments with self-signed certificates.
- Only use this script in secure, trusted environments.