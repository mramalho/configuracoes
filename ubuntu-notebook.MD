# SCRIPT COM CONFIGURACOES PARA MAQUINA DE DESENVOLVIMENTO

## Pacotes e dependencias utilizadas
```bash
sudo apt-get -y update
sudo apt-get -y upgrade
sudo apt-get -y install vim htop curl wget openjdk-17-jdk maven terminator gnupg software-properties-common openssh-server python3-pydrive python3-pydrive2 ca-certificates npm golang
```

## Adicionando variaveis do JAVA

```bash
echo "export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export MAVEN_HOME=/usr/share/maven
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$JAVA_MAVEN/bin" >> ~/.bashrc
source ~/.bashrc
```

## Configurando Git
```bash
git config --global user.name "Marcos Ramalho"
git config --global user.email "mramalho@gmail.com"
```

## Adicionando melhorias no prompt para o Git
```bash
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
source ~/.bashrc
```

# Adicionando pacotes utilizados
```bash
sudo snap install --classic intellij-idea-community
sudo snap install --classic code
sudo snap install --classic vlc
sudo snap install --classic drawio
sudo snap install --classic obs-studio
sudo snap install --classic discord
sudo snap install --classic dbeaver-ce
sudo snap install --classic postman
sudo snap install --classic inkscape
```

# Instalando docker
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```bash
sudo apt-get -y update
sudo apt-get -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin docker-buildx-plugin
```
```bash
mkdir /home/"$USER"/.docker
sudo usermod -aG docker $USER
sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "$HOME/.docker" -R
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```
# Instalando o docker-compose
```bash
sudo apt-get -y install docker-compose
```

# Instando kubelet, kubeadm e kubectl
```bash
sudo apt-get -y update
sudo apt-get -y  install ca-certificates curl apt-transport-https
sudo curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
```bash
sudo apt-get -y update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
# Instalando o bash Completion do Kubernetes
```bash
echo 'source <(kubectl completion bash)' >>~/.bashrc
source ~/.bashrc
```

# Instalando o K3D
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.18.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

# Instalando o K9s
```bash
wget https://github.com/derailed/k9s/releases/download/v0.27.3/k9s_Linux_amd64.tar.gz
sudo tar xfzv k9s_Linux_amd64.tar.gz -C /usr/local/bin
```

# Instalando o Helm
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
sudo chmod 700 get_helm.sh
./get_helm.sh
rm get_helm.sh
```

# Instalando o Terraform
```bash
wget https://releases.hashicorp.com/terraform/1.4.6/terraform_1.4.6_linux_amd64.zip
unzip terraform_1.4.6_linux_amd64.zip -d /tmp
sudo cp /tmp/terraform /usr/local/bin
rm terraform_1.4.6_linux_amd64.zip
```

# Instalando o AWS CLI
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
rm awscliv2.zip
rm -rf aw/
```
