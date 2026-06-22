# config SSH

## add user to ssh config

### Create User

```bash
sudo adduser someuser
```

### Give sudo permission

```bash
sudo usermod -aG sudo someuser
```

verify:

```bash
groups someuser
```

You should see sudo in the list.

## Install SSH server

```bash
sudo apt update
sudo apt install openssh-server
```

Check status:

```bash
sudo systemctl status ssh
```

Enable it:

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

## Allow ONLY someuser to SSH

Edit SSH config:

```bash
sudo vim /etc/ssh/sshd_config
```

Add at the bottom:

```
AllowUsers someuser
```

## Disable root login (Optional):

```
PermitRootLogin no
```

## Disable password login (if you want key-only access):

```
PasswordAuthentication no
```

## Restart SSH service

```
sudo systemctl restart ssh
```

## Generate SSH key (on your client machine)

Run this on your laptop/PC (not the server):

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

### What it will ask:

* File location → press Enter (default: `~/.ssh/id_ed25519`)
* Passphrase →

  * press Enter for no password (fully automatic login)
  * or set one for extra security

---

# Copy key to server

```bash
cat ~/.ssh/id_ed25519.pub
```

On server past key:

```bash
mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys
```

Then fix permissions (if required):
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

## (Important) SSH config hardening globally

```bash
sudo vim /etc/ssh/sshd_config
```

Set:

```
PubkeyAuthentication yes
PasswordAuthentication no
```

# Configure per-user rules

## Open SSH config:

```bash
sudo vim /etc/ssh/sshd_config
```

Make sure these global settings are enabled:
```
PubkeyAuthentication yes
PasswordAuthentication yes
```

Add this at the bottom of the file:

```
# Default behavior for everyone (optional but recommended baseline)
PasswordAuthentication yes

# --- Alex: password allowed ---
Match User Alex
    PasswordAuthentication yes
    PubkeyAuthentication yes

# --- Bob: ONLY SSH key login ---
Match User Bob
    PasswordAuthentication no
    PubkeyAuthentication yes
    AuthenticationMethods publickey
```

Note: AuthenticationMethods publickey enforces strict key-only login
Note: Match User rules MUST be at the end of the file.

## Config Permissions (important)
On server:
```
chmod 700 /home/Bob/.ssh
chmod 600 /home/Bob/.ssh/authorized_keys
chown -R Bob:Bob /home/Bob/.ssh
```

## More user Rules

```
Match User Alex
    ForceCommand /bin/false
    AllowTcpForwarding yes
    PermitTTY no
    X11Forwarding no
    AllowAgentForwarding no
```

## Port Forwarding

```bash
ssh -L 8080:localhost:80 Alex@server-ip
```

## Reverse

```bash
ssh -R 2222:localhost:22 Alex@server-ip
```


