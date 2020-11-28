# INSTALLATION OF KUBERNETES
sudo apt install apt-transport-https ca-certificates curl software-properties-common \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - \
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" \
sudo apt update \
sudo apt install docker-ce docker-compose \
systemctl status docker \
sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2 \
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - \
sudo chmod 777 /etc/apt/sources.list.d/ \
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list \
sudo apt-get update \
sudo apt-get install -y kubelet kubeadm kubernetes-cni socat kubectl

# Ignore this one for the worker nodes.
sudo kubeadm init --ignore-preflight-errors=NumCPU

OUTPUT:

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube \
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config \
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Then you can join any number of worker nodes by running the following on each of the nodes as root:

kubeadm join xxxxxxxxxxx:6443 --token jdifvr.1x7puhpsxmo7haq7 --discovery-token-ca-cert-hash sha256:5871043f7b1e906f4ea5985e4d92291ace4b226b8ee81c7640d72b83cab69009

# Initialize weave network
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"


# To initiallize ingress controller in the document
# To initiallize ingress controller in document

URL: https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/

# To generate the token with the join command
kubeadm token create --print-join-command

# Kubernetes Provider Documentation of the year
URL: https://kubernetes.io/docs/

# Test line from new branch
