### Cassandra kube ###

Тестировалось на Ubuntu 17.10
Необходимое ПО
- git
- python-pip
- sshpass
- pbr>=1.6
- ansible==2.4.2.0
- netaddr
- jinja2>=2.9.6

apt-get install -y git python-pip sshpass
pip install -r requirements.txt
ssh-keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub javdet@localhost

Запустить
ansible-playbook -i inventory/ -v -b -K virtualization.yml

vagrant up
Затем 
ansible-playbook -i inventory/hosts cluster.yml -b -v -K

В директории вагранта должны быть права
размер диска
по 20 на ВМ

https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.2.0/jmx_prometheus_javaagent-0.2.0.jar