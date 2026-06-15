## Edit SSH config

```bash
sudo nano /etc/ssh/sshd_config
```
## Important SSH configuration

Disable root login (recommended for security):

```conf
PermitRootLogin no
```

Restart SSH:

```bash
sudo systemctl restart sshd
```

Check SSH status:

Description:
Shows whether SSH service is running or not.

```bash
systemctl status sshd
```

---

## How SSH config override works (IMPORTANT)

SSH reads multiple configuration files.

Main config file:

```bash
/etc/ssh/sshd_config
```

Additional config directory:

```bash
/etc/ssh/sshd_config.d/
```

Inside main file:

```conf
Include /etc/ssh/sshd_config.d/*.conf
```

👉 This means files inside `sshd_config.d/` can **override** main settings.

---

## Fixing PermitRootLogin issue

If root login still works after setting:

```conf
PermitRootLogin no
```

Check this file:

```bash
/etc/ssh/sshd_config.d/01-permitrootlogin.conf
```

If you see:

```conf
PermitRootLogin yes
```

Comment it out:

```conf
# PermitRootLogin yes
```

Then restart SSH:

```bash
sudo systemctl restart sshd
```
---
## Let's now verify the configuration we have made. 
### Step 1: Connect to server using your own user

First, you connect to the server using SSH with your normal user account:

### Step 2: Check current user

```bash
whoami
```

### Step 3: Switch to root (if allowed)

If your user has sudo privileges, you can upgrade your access to root:

```bash
sudo -i
```

After this:
- Your shell becomes root
- You have full system access

Check again:

```bash
whoami
```

Output:

```text
root
```

---

### Important Notes

- SSH does NOT give root access automatically
- You always start with the user you logged in with
- `sudo -i` only works if your user is allowed in `/etc/sudoers`
- This is the standard and secure workflow in Linux systems


