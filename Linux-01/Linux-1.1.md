Here’s the content organized into a well-formatted Markdown file for better readability:
## Key Concept and Actions

### 1. **IP Address Assignment**
- The `ip addr add` comand is uded to assign IP address to network interfaces. 
- Example:
-  ```bash
  sudo ip addr add 172.16.239.15/24 dev eth0
-- This assigns the IP `172.16.239.15` with a subnet mask of `/24` to the `eth0` interface.

### 2. **SSH Authentication**
- When connecting to a new host via SSH for the first time, the host's fingerprint is verified.
- The user is prompted to confirm the fingerprint:
  ```
  The authenticity of host 'app01 (172.16.238.11)' can't be established.
  ED25519 key fingerprint is SHA256:chQYsWlCmIdiWh94Ykq2olH7WkFAHSx4jSEE1l5jHDY.
  Are you sure you want to continue connecting (yes/no/[fingerprint])?
  ```
- Typing `yes` adds the host's fingerprint to `~/.ssh/known_hosts`.

### 3. **Password Authentication Issues**
- If SSH password authentication fails, the user is denied access:
  ```
  thor@app02's password: 
  Permission denied, please try again.
  ```
- This indicates either an incorrect password or misconfigured SSH access.

### 4. **Adding Multiple IP Addresses**
- Multiple IP addresses can be assigned to the same interface (`eth0` in this case):
  ```bash
  sudo ip addr add 172.16.239.15/24 dev eth0
  sudo ip addr add 172.16.239.16/24 dev eth0
  ```

### 5. **Failed SSH Attempts**
- Failed SSH login attempts are logged and displayed:
  ```
  Last failed login: Tue Feb 11 12:02:01 UTC 2025 from 172.16.238.11 on ssh:notty
  There was 1 failed login attempt since the last successful login.
  ```

### 6. **Exiting SSH Sessions**
- The `exit` command is used to log out of an SSH session:
  ```bash
  exit
  ```

### 7. **Persistent SSH Host Keys**
- Once a host's fingerprint is added to `~/.ssh/known_hosts`, subsequent connections do not prompt for verification:
  ```
  Warning: Permanently added 'app02' (ED25519) to the list of known hosts.
  ```

---

## Summary of Commands Used

### **IP Address Management**
```bash
sudo ip addr add <IP>/<subnet> dev <interface>
```

### **SSH Connections**
```bash
ssh <hostname>
```

### **Exiting Sessions**
```bash
exit
```

---

## Key Takeaways

1. **IP Address Assignment:** Multiple IPs can be assigned to a single interface.
2. **SSH Security:** Host fingerprints are verified during the first connection to prevent man-in-the-middle attacks.
3. **Authentication Issues:** Failed SSH attempts can occur due to incorrect passwords or misconfigurations.
4. **Session Management:** Use `exit` to gracefully end SSH sessions.
