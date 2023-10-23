# Subsquid Snapshot

## Update Packages
```
sudo apt update
sudo apt install git
```
## Install Nodejs and Npm
```
sudo apt install nodejs
sudo apt install npm
npm install -g npm@10.2.0
```
## Install Docker
```
sudo apt-get install ca-certificates curl gnupg lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```
## Patch
```
mkdir global-node-packages
npm config set prefix ~/global-node-packages
export PATH="${HOME}/global-node-packages/bin:$PATH"

cd global-node-packages
npm install --global @subsquid/cli@latest
```
## Run The Squid
```
sqd init my-snapshot-squid -t https://github.com/subsquid-quests/snapshot-squid
cd my-snapshot-squid
```
## Add Keys
<img width="197" alt="image" src="https://github.com/xxcode2/Subsquid/assets/137141202/6000089a-7b18-40e7-8f29-05ad5284624b">


## Start your Squid
```
sqd up
```
##
```
npm ci
sqd build
sqd migration:apply
```
##
```
sqd run .
```
*The squid should sync in about 1.5 hours. When it's done, stop it with Ctrl-C, then stop and remove the auxiliary containers with*
```
sqd down
```
