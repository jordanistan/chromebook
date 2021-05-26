Setting up a chromebook for development
Documenting my steps
#howto #chromebook #docker

I just switch my pixelbook back to the stable channel, and this is what I did to get back to developing on it.

First:
Open up settings
Linux (Beta)
Turn on
Wait for it to download
Startup the terminal app
Everything from here happens in the terminal app.

Configure git
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
Install Docker
Install docker the normal way

# Update debian
sudo apt-get update -y && sudo apt-get upgrade

sudo apt-get install -y \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common

# Add the gpg key if it;s not there
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

# Add the docker repository
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

# Update and add docker-ce
sudo apt-get update -y && sudo apt-get install docker-ce -y

# Install docker-compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" \
  -o /usr/local/bin/docker-compose

# Add yourself to the docker group if you aren't already
sudo groupadd docker && sudo usermod -aG docker $USER
Now you may need to shutdown the linux installation to make sure that your user is in the docker group.

Alt-click on the terminal icon in the dock
Select “Shutdown Linux (Beta)”
Restart terminal
Run docker run hello-world to test out the installation

# Installing Vs Code
cd /tmp
wget -O discord.deb "https://discordapp.com/api/download?platform=linux&format=deb"
sudo dpkg -i discord.deb

# Install Zsh
sudo apt install zsh -y
# Install Oh My Zsh
wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh
sh install.sh

# Unattended Install Oh My Zsh
If you're running the Oh My Zsh install script as part of an automated install, you can pass the flag --unattended to the install.sh script. This will have the effect of not trying to change the default shell, and also won't run zsh when the installation has finished.

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/inst

Installing go
cd /tmp
wget https://dl.google.com/go/go1.12.1.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.12.1.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.zshrc
source ~/.zshrc
Test out using go version

Installing Vscode
# First of all, You need to enable package repository in your system. Run the following command to enable Visual studio code repository to your system.
echo "deb [arch=amd64] http://packages.microsoft.com/repos/vscode stable main" | sudo tee /etc/apt/sources.list.d/vs-code.list

# Import the package signing gpg key on your system using the following command.
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

# Install Visual Studio Code on your Debian based system.
sudo apt-get update -y && sudo apt-get install code -y

Installing Google Cloud CLI
# Create environment variable for correct distribution
export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)"

# Add the Cloud SDK distribution URI as a package source
echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list

# Import the Google Cloud Platform public key
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

# Update the package list and install the Cloud SDK
sudo apt-get update -y && sudo apt-get install google-cloud-sdk -y
Test out using gcloud auth login


Actually it’s all standard stuff
There’s nothing specifically Chromebook about this, but its easier for me to keep this all written down in one place.

