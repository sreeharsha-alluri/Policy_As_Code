# Policy_As_Code
Follow these commands to restrict the creation of Pod followed by the restriction in a specific namespace

sudo apt update -y

sudo apt upgrade -y

Installing kubectl

curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl


Installing eksctl

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin

Installing aws cli

sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

Installing helm

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh


aws configure

Access Key : 
Secret Key :

git clone https://github.com/sreeharsha-alluri/Policy_As_Code.git

eksctl create cluster -f cluster.yaml

helm repo add gatekeeper https://open-policy-agent.github.io/gatekeeper/charts

helm install gatekeeper/gatekeeper --name-template=gatekeeper --namespace gatekeeper-system --create-namespace

kubectl get ns

kubectl get pods -n gatekeeper-system

kubectl logs -l control-plane=audit-controller -n gatekeeper-system

kubectl logs -l control-plane=controller-manager -n gatekeeper-system

kubectl create -f constrainttemplate.yaml

kubectl create -f constraint.yaml

kubectl get constrainttemplate

kubectl get constraint

kubectl create -f example.yaml
