# INSTALLATION OF KUBERNETES
sudo apt install apt-transport-https ca-certificates curl software-properties-common \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - \
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" \
sudo apt update \
### For the installation of kubernetes version 1.19.00, docker version that is compatible is 19.03.
sudo apt-cache policy docker-ce | grep 19 \
sudo apt-cache policy docker-ce-cli | grep 19 \
sudo apt install -y docker-ce=5:19.03.15~3-0~ubuntu-bionic docker-ce-cli=5:19.03.15~3-0~ubuntu-bionic \
sudo apt-mark hold docker-ce docker-ce-cli \
sudo apt install docker-compose -y \
sudo apt-mark unhold docker-ce docker-ce-cli \
sudo systemctl status docker \
sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2 \
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - \
sudo chmod 777 /etc/apt/sources.list.d/ \
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list \
sudo apt-get update \   
### Stop swap if the VM has any   
sudo swapoff -a  \  
sudo sed -i '/ swap / s/^/#/' /etc/fstab  \

### One minor version of kubelet is allowed.   
sudo apt-get install -y kubelet=1.18.0-00 kubeadm=1.19.0-00 kubernetes-cni socat kubectl=1.19.0-00

## Ignore this one for worker nodes and check if the swap is disabled or not.
cat /proc/meminfo | grep -i swap     
sudo kubeadm init --ignore-preflight-errors=NumCPU

OUTPUT:

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube \
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config \
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Then you can join any number of worker nodes by running the following on each as root:

kubeadm join xxxxxxxxxxx:6443 --token jdifvr.1x7puhpsxmo7haq7 --discovery-token-ca-cert-hash sha256:5871043f7b1e906f4ea5985e4d92291ace4b226b8ee81c7640d72b83cab69009

# Initialize weave network
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

# To initiallize ingress controller
URL: https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/
Ingress class is really important while installation. Ingress objects should follow the ingress class installed.

# To generate the token with join command
kubeadm token create --print-join-command

# Kubernetes Documentation
URL: https://kubernetes.io/docs/
