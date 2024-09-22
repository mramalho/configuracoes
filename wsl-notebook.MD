# CONFIGURAÇÕES PARA MÁQUINA DE DESENVOLVIMENTO

## Pacotes e dependências utilizadas
```bash
sudo apt-get -y update
sudo apt-get -y upgrade
sudo apt-get -y remove thunderbird
sudo apt-get -y autoremove
sudo apt-get -y install htop curl wget openjdk-8-jdk openjdk-11-jdk openjdk-17-jdk openjdk-21-jdk maven terminator gnupg software-properties-common zip openssh-server python-is-python3 golang
```

## Adicionando variáveis do JAVA

```bash
cat >> ~/.bashrc << EOL
export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
export MAVEN_HOME=/usr/share/maven

parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
EOL
source ~/.bashrc
```

# Install .NET SDK or .NET Runtime on Ubuntu

## Install the SDK

```bash
sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-8.0
```` 

## Install the runtime

```bash
sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-8.0
````

```bash
sudo apt-get install -y dotnet-runtime-8.0
````


# Install the Azure CLI on Linux

```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
````

```bash
sudo mkdir -p /etc/apt/keyrings
curl -sLS https://packages.microsoft.com/keys/microsoft.asc |
  gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
sudo chmod go+r /etc/apt/keyrings/microsoft.gpg
````

```bash
AZ_DIST=$(lsb_release -cs)
echo "Types: deb
URIs: https://packages.microsoft.com/repos/azure-cli/
Suites: ${AZ_DIST}
Components: main
Architectures: $(dpkg --print-architecture)
Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources
````


```bash
sudo apt-get update
sudo apt-get install azure-cli
````

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
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
````