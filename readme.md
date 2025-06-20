Create IAM user and attach required polices 

create access keys

install aws cli 

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install
aws configure

install kubecl

curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client


install eksctl


curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version


Create EKS CLUSTER



eksctl create cluster --name=EKS-1 \
                      --region=us-east-1 \
                      --zones=us-east-1a,us-east-1b \
                      --without-nodegroup

eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster EKS-1 \
    --approve

eksctl create nodegroup --cluster=EKS-1 \
                       --region=us-east-1 \
                       --name=node2 \
                       --node-type=t3.medium \
                       --nodes=3 \
                       --nodes-min=2 \
                       --nodes-max=4 \
                       --node-volume-size=20 \
                       --ssh-access \
                       --ssh-public-key=ansible \
                       --managed \
                       --asg-access \
                       --external-dns-access \
                       --full-ecr-access \
                       --appmesh-access \
                       --alb-ingress-access

sudo apt install openjdk-17-jre-headless




sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y


sudo cat /var/lib/jenkins/secrets/initialAdminPassword

sudo apt  install docker.io

chmod 666 /var/run/docker.sock

plugins

install plugins dcoker, docker pipleline, kubernets, kubernets CLI, multibranch scan webhook trigger

manage jenkins --> tools-->
configure docker

add creds

with id (docker-cred)

create multi-branch

add branch source git

Scan Multibranch Pipeline Triggers

http://34.201.52.4:8080/multibranch-webhook-trigger/invoke?token=sam

go to githib settings webhook 

enter above url 
select application/json

save


create namespace

kubectl create namespace webapps

create svc.yml with service account

kubectl apply -f svc.yml

kubectl apply -f role.yml

kubectl apply -f bind.yml

kubectl apply -f sec.yml -n webapps

kubectl describe secret mysecretname -n webapps

eyJhbGciOiJSUzI1NiIsImtpZCI6IkpZRkpfVWtUUVdXQ2ttYXFmQ29ERU9xc2hVX1Ntd1RDRkJJTWU0MndXdHcifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJ3ZWJhcHBzIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6Im15c2VjcmV0bmFtZSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJqZW5raW5zIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiNWZmNzYzZmItNDhmYS00YzNlLTkxNjgtYzNlNmFmOGQ4YjcyIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50OndlYmFwcHM6amVua2lucyJ9.CVLIM7ojgqUOoel5D_miKRvzJcIkTs7b57StDsiEyR2KafDXEAc6O2kDJ5zXnfKgizF0zE1GdJqUqlJh-HZwlJ_eK5FZBgb9rCj5IGGCo_Xu5DUAyHnhFMTj2p1C1XnolCgEyyjXeKtCrbdhI7EQt4t61Kyzaykige48GoRAcXnybOL8b9UGCWhcKYzZCSvTFovsLSqk6GpjIyTYYbx1jm2nCroG7Z1euThUaVb6SC5TA1yQ7G1Ogc2fyQbRanFUndaquLBLgvDkRamJPMl55PkhWas-qfu6EBWvg0Kuf4rwVtz_pmf_kiHTiabia-g1x2-JaHLFGdrYB7YG1dAnZA

create new pipeline test

select hello world

genrate pipepline syntx withkubeconfig CLI

withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://7E7214F3DB9EF0E7CF0E9AC7193D0F5A.gr7.us-east-1.eks.amazonaws.com']]) {
    // some block
}




Note: relpace saamrajepatil in each deployment.yml and jenkinsfile to your dockerhub username





