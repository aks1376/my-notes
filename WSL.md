# WSL

## Install linux from .wsl file

for installing linux from file run this command

```cmd
wsl --install --from-file .\ubuntu-24.04.3-wsl-amd64.wsl --name myLinux
```

## Get installed distro list

```cmd
wsl -l -v
```

## Run distro

```cmd
wsl -d myLinux
```
