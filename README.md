Installation Steps:


1.Install Jenkins:

sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  
sudo apt-get update

sudo apt-get install jenkins

2.Install Docker:

sudo apt-get update

sudo apt-get install docker.io -y

3.Install SonarQube:

apt install unzip

adduser sonarqube

wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip

unzip *

chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424

chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424

cd sonarqube-9.4.0.54424/bin/linux-x86-64/

./sonar.sh start

4.Install ArgoCD Operator and Cluster:

curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.30.0/install.sh | bash -s v0.30.0

kubectl create -f https://operatorhub.io/install/argocd-operator.yaml

kubectl get csv -n operators

5.Install Helm on Minikube:

sudo apt update

sudo apt install -y apt-transport-https curl

curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -

sudo apt-get install -y software-properties-common

sudo add-apt-repository "deb https://baltocdn.com/helm/stable/debian/ all main"

sudo apt update

sudo apt install -y helm

helm version

helm repo update // To update the helm repo's

6.Install Prometheus and Grafana using Helm:

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo add grafana https://grafana.github.io/helm-charts

helm repo update

helm install prometheus prometheus-community/prometheus

helm install grafana grafana/grafana 



