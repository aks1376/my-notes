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
