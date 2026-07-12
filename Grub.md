# Edit Grub

## Remember the Last Boot Selection in GRUB

### Edit the Grub settings
```bash
sudo vim /etc/default/grub
```

Comment out the line with `GRUB_DEFAULT=0` and replace it by:

```
#GRUB_DEFAULT=0
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
```

Update Grub

```bash
sudo update-grub
```
