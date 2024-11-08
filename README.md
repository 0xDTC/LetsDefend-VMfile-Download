## Script: Remote File Transfer and Cleanup

### Overview
This script automates the secure transfer of a file from a remote server to a local machine using SSH and SCP with `expect`. It also performs file cleanup on the remote server after confirming a successful download. The script prompts the user for necessary input details and minimizes output for a cleaner terminal experience.

### Features
- Transfers a file from a specified path on a remote server to a local directory.
- Handles `sudo` permissions for files located in restricted directories on the remote server.
- Automatically cleans up the temporary file on the remote server post-transfer.
- Provides a final success message if the file transfer is successful.

### Requirements
- **Bash**
- **Expect**: This script uses `expect` for handling password prompts interactively.

### Usage

1. Make the script executable:
   ```bash
   chmod +x your_script_name.sh
   ```

2. Run the script:
   ```bash
   ./your_script_name.sh
   ```

3. Follow the prompts to enter:
   - **Remote server username**
   - **Remote server IP address**
   - **Path of the file on the remote server** (e.g., `/etc/shadow`)
   - **Password for sudo access** on the remote server
   - **Local destination directory** where the file should be saved

### Prompts
- **Remote server username**: The username with SSH access to the remote server.
- **Remote server IP address**: The IP of the remote server.
- **Path of the file on the remote server**: The full path to the file that needs to be transferred (e.g., `/root/Desktop/ChallengeFile/Pcap_Analysis.pcapng`).
- **Password for sudo access**: Password for `sudo` access if the file is in a restricted directory.
- **Destination directory on the local machine**: The local path where the file will be saved.

### Script Breakdown

1. **File Transfer Preparation**:
   - The script creates a temporary copy of the specified file on the remote server in a location accessible by the SSH user.
2. **File Transfer to Local**:
   - The script transfers the temporary file to the specified local destination.
   - If successful, it proceeds to clean up; otherwise, it exits with an error message.
3. **Remote Cleanup**:
   - The script removes the temporary file from the remote server.

### Example

```plaintext
Enter the remote server username: analyst
Enter the remote server IP address: 18.222.171.163
Enter the path of the file on the remote server (e.g., /etc/shadow): /root/Desktop/ChallengeFile/Pcap_Analysis.pcapng
Enter the password for sudo access on the remote server:
Enter the destination directory on the local machine (e.g., ~/letsdefend): /home/kali/letsdefend/
File has been successfully transferred to /home/kali/letsdefend and cleaned up on the remote server.
```

### Error Handling
- If the file transfer fails, an error message will indicate the issue, advising to check connectivity and paths.

### Notes
- Ensure `expect` is installed on your system to enable the script to handle password prompts.

### Security Notice
- Avoid storing passwords in plain text within scripts.
- Use appropriate access controls and delete temporary files after use.