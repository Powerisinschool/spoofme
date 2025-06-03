# SpoofMe

**SpoofMe** assigns a random hostname and random MAC address to your Linux system every time it boots.

It detects all physical (non-virtual) network interfaces — both wired and wireless — and spoofs their MAC addresses using `macchanger`.

---

## 🧠 Requirements
- `macchanger` must be installed.
    ```bash
    sudo apt install macchanger
    ```

## 🛠️ Installation

1. **Clone the repository and navigate to the directory:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/spoofme.git 
   cd spoofme
   ```

2. Copy the `spoofme` script to a location in your `$PATH` (e.g. `/usr/bin/`):
  ```bash
  sudo cp spoofme /usr/bin
  sudo chmod +x /usr/bin/spoofme
  ```
  >**Note**: *If copying "spoofme" to a location other than "/usr/bin", update the ExecStart in line 8 in "spoofme.service" accordingly*:
  >```diff
  >- ExecStart=/usr/bin/spoofme
  >+ ExecStart=/your/directory/spoofme
  >```

3. Install the systemd service file:
  ```bash
  sudo cp spoofme.service /etc/systemd/system/
  sudo chmod 644 /etc/systemd/system/spoofme.service
  ```

4. Reload systemd to recognize the new service:
  ```bash
  sudo systemctl daemon-reexec
  sudo systemctl daemon-reload
  ```

5. Enable the service to run at boot:
  ```bash
  sudo systemctl enable spoofme
  ```

<details>
<summary>
  <h3>Optional</h3><br />
  Before rebooting, verify the service works as expected:
</summary>
<br />
1. Start the service manually:
```bash
sudo systemctl start spoofme
```

2. Verify the hostname has changed:
```bash
hostname
```

3. Check if MAC addresses were spoofed:
```bash
ip link show
```

4. Review changes in "/etc/hosts":
```bash
cat /etc/hosts
```
</details>

### 📌 Notes
This script skips loopback, bridge, docker, and virtual interfaces.
MAC spoofing is applied to all physical wireless and ethernet interfaces by default, or you can pass specific interfaces as arguments.
