# base wiki

## setup

```bash
# find newest go version and downloa it: https://go.dev/doc/install
wget https://go.dev/dl/go1.25.1.linux-amd64.tar.gz

# Remove any previous Go installation by deleting the /usr/local/go folder (if it exists), then extract the archive you just downloaded into /usr/local, creating a fresh Go tree in /usr/local/go
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.25.1.linux-amd64.tar.gz

# Add /usr/local/go/bin to the PATH environment variable
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc && source ~/.bashrc

sudo snap install hugo
```

## add content

```bash
hugo new docs/...
```

```bash
git submodule update --remote
hugo mod get -u
```