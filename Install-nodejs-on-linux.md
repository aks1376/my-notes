# Nodejs Installation

### Download archive file

```bash
wget https://nodejs.org/dist/v24.17.0/node-v24.17.0-linux-x64.tar.xz
```

### Extract archive file

```bash
tar -xJvf node-v24.17.0-linux-x64.tar.xz 
```

## Install Nodejs Without Root Permission

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

