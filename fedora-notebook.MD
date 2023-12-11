# CONFIGURAÇÕES PARA MÁQUINA DE DESENVOLVIMENTO

## Pacotes e dependências utilizadas
```bash
sudo apt-get -y update
sudo apt-get -y upgrade
sudo apt-get -y remove thunderbird
sudo apt-get -y autoremove
sudo yum -y install htop curl wget awscli java-17-openjdk maven terminator gnupg  zip openssh-server
```

## Adicionando variáveis do JAVA

```bash
cat >> ~/.bashrc << EOL
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export MAVEN_HOME=/usr/share/maven
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$JAVA_MAVEN/bin

parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
EOL
source ~/.bashrc
```

## Adicionando pacotes utilizados
```bash
sudo flatpak -y install com.google.Chrome
sudo flatpak -y install org.videolan.VLC
sudo flatpak -y install org.videolan.VLC
sudo flatpak -y install org.videolan.VLC
sudo flatpak -y install com.discordapp.Discord
sudo flatpak -y install com.getpostman.Postman
sudo flatpak -y install com.obsproject.Studio
sudo flatpak -y install io.dbeaver.DBeaverCommunity
sudo flatpak -y install com.sublimetext.three
sudo flatpak -y install com.jetbrains.PyCharm-Community
sudo flatpak -y install com.jetbrains.IntelliJ-IDEA-Community
```

## Instalando Docker e Docker-Compose
```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo usermod -aG docker $USER

newgrp docker
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
sudo apt-get -y install docker-compose
```

## Instando kubectl
```bash
sudo apt-get -y update
sudo apt-get -y install apt-transport-https ca-certificates curl
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get -y update
sudo apt-get -y install kubectl bash-completion

echo 'source <(kubectl completion bash)' >>~/.bashrc
source ~/.bashrc
```

## Instalando o Kind
```bash
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```


## Instalando o EKSCTL
```bash
# for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH
curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
# (Optional) Verify checksum
curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check
tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
sudo mv /tmp/eksctl /usr/local/bin
```

## Instalando o K9s
```bash
curl -sLO "https://github.com/derailed/k9s/releases/download/v0.28.2/k9s_Linux_amd64.tar.gz"
tar -xzf k9s_Linux_amd64.tar.gz -C /tmp && rm k9s_Linux_amd64.tar.gz
chmod +x /tmp/k9s
sudo mv /tmp/k9s /usr/local/bin
```

## Instalando o Helm
```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get -y install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get -y update
sudo apt-get -y install helm
```

## Instalando o Terraform
```bash
sudo apt-get -y update && sudo apt-get -y install gnupg software-properties-common
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com lunar main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt-get -y update
sudo apt-get -y install terraform
```

## Instalando o Terragrunt
```bash
curl -o /tmp/terragrunt https://github.com/gruntwork-io/terragrunt/releases/download/v0.53.8/terragrunt_linux_amd64
chmod +x /tmp/terragrunt
sudo mv /tmp/terragrunt /usr/local/bin
```

## Instalando o OpenLens
```bash
curl -sLO "https://github.com/MuhammedKalkan/OpenLens/releases/download/v6.5.2-366/OpenLens-6.5.2-366.amd64.deb"
sudo mv OpenLens-6.5.2-366.amd64.deb /tmp/.
sudo dpkg -i /tmp/OpenLens-6.5.2-366.amd64.deb
```