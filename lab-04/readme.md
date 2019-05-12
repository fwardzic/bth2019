# Lab 04 - kubernetes

create new K8s cluster

https://labs.play-with-k8s.com

`kubeadm init --apiserver-advertise-address $(hostname -i)`

` kubectl apply -n kube-system -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"`

wait until node will be ready:

`kubectl get nodes`

check command to join other worker nodes:

`kubeadm token create --print-join-command`

Add new instance - open terminal of node2:

`kubeadm join 192.168.0.13:6443 --token dnxg5d.9pmytqezc6mf9e5w --discovery-token-ca-cert-hash sha256:5467b42fb5e11d36d95f682575d9997ba7809d89e5fb56f9f8c1d9bfd0d724eb`

wait until node will be ready:

`kubectl get nodes`

create POD:

`kubectl apply -f https://github.com/fwardzic/bth2019/blob/master/lab-04/pod.yaml`

create deployment:

`kubectl apply -f https://github.com/fwardzic/bth2019/blob/master/lab-04/deployment.yaml`

create service:

`kubectl apply -f https://github.com/fwardzic/bth2019/blob/master/lab-04/service.yaml`