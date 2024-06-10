# CONFIGURAÇÕES PARA MÁQUINA DE DESENVOLVIMENTO -FEDORA

## Pacotes e dependências utilizadas
```bash
sudo dnf -y install htop curl wget awscli java-17-openjdk maven terminator gnupg  zip openssh-server golang
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
** Precisa primeiramente ativar o uso de repositórios 
```bash
sudo flatpak -y update
sudo flatpak -y install com.google.Chrome
sudo flatpak -y install com.visualstudio.code
sudo flatpak -y install com.jgraph.drawio.desktop
sudo flatpak -y install io.dbeaver.DBeaverCommunity
sudo flatpak -y install com.sublimetext.three
sudo flatpak -y install com.jetbrains.IntelliJ-IDEA-Community
```

## Instalando Docker e Docker-Compose
```bash
sudo dnf remove -y  docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo                  
                  
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin   
sudo systemctl start docker
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
sudo dnf istall -y docker-compose
                  
```

## Instando kubectl
```bash
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.28/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.28/rpm/repodata/repomd.xml.key
EOF
sudo dnf install -y kubectl
sudo dnf install -y bash-completion
echo 'source <(kubectl completion bash)' >>~/.bashrc
source ~/.bashrc
```

## Instalando o Kind
```bash
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
sudo chmod +x ./kind
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
sudo dnf install -y helm
```

## Instalando o Terraform
```bash
sudo dnf install -y dnf-plugins-core	
sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/fedora/hashicorp.repo
sudo dnf -y install terraform
touch ~/.bashrc
terraform -install-autocomplete
```

## Instalando o Terragrunt
```bash
curl -o /tmp/terragrunt https://github.com/gruntwork-io/terragrunt/releases/download/v0.53.8/terragrunt_linux_amd64
chmod +x /tmp/terragrunt
sudo mv /tmp/terragrunt /usr/local/bin
touch ~/.bashrc
terragrunt --install-autocomplete
```

## Instalando o OpenLens
```bash
curl -sLO "https://github.com/MuhammedKalkan/OpenLens/releases/download/v6.5.2-366/OpenLens-6.5.2-366.x86_64.rpm"
sudo mv OpenLens-6.5.2-366.x86_64.rpm /tmp/.
sudo rpm -i /tmp/OpenLens-6.5.2-366.x86_64.rpm
```
