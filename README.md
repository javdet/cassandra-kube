Ubuntu 16.04
apt-get install -y git python-pip sshpass
sudo pip install ansible==2.4.2.0
python-netaddr
ssh-keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub javdet@localhost

ansible-playbook -i inventory/ -v -b -K virtualization.yml

подождать 30 сек
ansible-playbook -i inventory/ -v -b -K kubernetes.yml

В директории вагранта должны быть права
размер диска
по 20 на ВМ

export ANSIBLE_HOST_KEY_CHECKING=False
kubeadm init --token="jfuw63.1osue85lsh973hbf" --apiserver-advertise-address=172.16.66.2 --kubernetes-version v1.7.0