Ubuntu 16.04
apt-get install -y git python-pip sshpass
sudo pip install ansible==2.4.2.0
ssh-keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub javdet@localhost

ansible-playbook -i inventory/ -v -b -K virtualization.yml
ansible-playbook -i inventory/ -v -b -K kubernetes.yml

В директории вагранта должны быть права
размер диска
по 20 на ВМ

export ANSIBLE_HOST_KEY_CHECKING=False
