# Config wifi

## Find Wi-Fi interface

```sh
ip link
```

## Config file location

```sh
cd /etc/netplan
```

## Edit file

```sh
sudo vim /etc/netplan/50-cloud-init.yaml
```

## Example with both Ethernet and Wi-Fi

```yaml
network:
  version: 2

  ethernets:
    eth0:
      dhcp4: true

  wifis:
    wlan0:
      dhcp4: true
      nameservers:
        addresses:
          - 1.1.1.1
          - 8.8.8.8
      access-points:
        "YourWifiName":
          password: "YourWifiPassword"
```

## 3. Apply the configuration

Check for syntax errors:

```bash
sudo netplan generate
```

Apply:

```bash
sudo netplan apply
```

## Verify DNS

Check what DNS servers are actually being used:

```bash
resolvectl status
```

## If DHCP keeps overriding your DNS

Add:
```yaml
dhcp4-overrides:
  use-dns: false
```

example:

```yaml
network:
  version: 2

  ethernets:
    eth0:
      dhcp4: true
      dhcp4-overrides:
        use-dns: false
      nameservers:
        addresses:
          - 1.1.1.1
          - 8.8.8.8
```
