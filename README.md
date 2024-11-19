# Tools Installation Guide

## 1. Install Jenkins

# Add Jenkins repository key
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

# Configure Jenkins repository
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

# Update package list and install Jenkins
sudo apt-get update 

sudo apt-get install jenkins -y

## 2. Install Docker

# Update package list
sudo apt-get update

# Install Docker
sudo apt-get install docker.io -y

## 3. Install SonarQube

# Install unzip utility
apt install unzip

# Create sonarqube user
adduser sonarqube

# Download SonarQube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip

# Unzip and set permissions
unzip *
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424

# Navigate and start SonarQube
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
./sonar.sh start

## 4. Install ArgoCD Operator and Cluster

# Install Operator Lifecycle Manager
curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.30.0/install.sh | bash -s v0.30.0

# Create ArgoCD Operator
kubectl create -f https://operatorhub.io/install/argocd-operator.yaml

# Verify CSV
kubectl get csv -n operators

## 5. Install Helm on Minikube

# Update package list
sudo apt update

# Install transport tools
sudo apt install -y apt-transport-https curl

# Add Helm repository key
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -

# Configure Helm repository
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://baltocdn.com/helm/stable/debian/ all main"

# Update and install Helm
sudo apt update
sudo apt install -y helm

# Verify Helm version
helm version

# Update Helm repositories
helm repo update

## 6. Install Prometheus and Grafana using Helm

# Add Prometheus and Grafana repositories
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts

# Update repositories
helm repo update

# Install Prometheus
helm install prometheus prometheus-community/prometheus

# Install Grafana
helm install grafana grafana/grafana
