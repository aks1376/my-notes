# Nodejs Installation

### Download archive file

```bash
wget https://nodejs.org/dist/v24.17.0/node-v24.17.0-linux-x64.tar.xz
```

### Extract archive file

```bash
tar -xJvf node-v24.17.0-linux-x64.tar.xz 
```

## Install Nodejs Without Root Permission ( Current logged in User )

### Move to Apps direcoty (optional)

```bash
mkdir Apps
mv node-v24.17.0-linux-x64 ./Apps/
```

### in ~.bashrc Add

```
NODE_HOME=~/Apps/node-v24.17.0-linux-x64
PATH=$NODE_HOME/bin:$PATH
```

### Source the bashrc file or restart terminal 

```bash
source .bashrc
```

### Try
```bash
node --version
npm -v
```

## Global installation

### Move Binary Files
```bash
sudo mv node-v24.17.0-linux-x64 /opt/nodejs
```

### Create symlinks
```bash
sudo ln -sf /opt/nodejs/bin/node /usr/local/bin/node
sudo ln -sf /opt/nodejs/bin/npm /usr/local/bin/npm
sudo ln -sf /opt/nodejs/bin/npx /usr/local/bin/npx
```

### Install Global Packages Without Using `sudo`
To avoid npm permission issues run

```bash
mkdir -p ~/.npm-global
npm config set prefix ~/.npm-global
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Extra commands
### Get npm Cache Location

```bash
npm config get cache
```

### Get npm Global installation

```bash
npm root -g
```
