# Subsquid Snapshot

sudo apt update
sudo apt install git

sudo apt install nodejs

sudo apt install npm

npm install -g npm@10.2.0

sudo apt-get install ca-certificates curl gnupg lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y

mkdir global-node-packages
npm config set prefix ~/global-node-packages
export PATH="${HOME}/global-node-packages/bin:$PATH"

d global-node-packages
npm install --global @subsquid/cli@latest

sqd init my-snapshot-squid -t https://github.com/subsquid-quests/snapshot-squid
cd my-snapshot-squid

sqd up

npm ci
sqd build
sqd migration:apply

sqd run .

*The squid should sync in about 1.5 hours. When it's done, stop it with Ctrl-C, then stop and remove the auxiliary containers with*

sqd down
