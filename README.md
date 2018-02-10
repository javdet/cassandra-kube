# Cassandra kube #

### Описание ###
Развертывание кластера Kubernetes (1 master, 3 nodes) в среде виртуализации 
VirtualBox. 

Развертывание кластера Cassandra из 3х узлов.

Развертывание Prometheus и настройка мониторинга метрик Cassandra.

### Необходимое ПО ###
- git
- python-pip
- sshpass
- pbr>=1.6
- ansible==2.4.2.0
- netaddr
- jinja2>=2.9.6

Установка:
```
sudo apt-get install -y git python-pip sshpass
sudo pip install -r requirements.txt
```

### Запуск ###

Установка необходимого ПО:
```
ansible-playbook -i inventory/ -v -b -K virtualization.yml
```
Примечание: для выполнения необходимы права sudo

После выполнения плейбука в директории запуска должен появиться Vagrantfile

Запуск создания VMs:
```
vagrant up
```
После того, как все VM созданы необходимо запустить развертывание кластера
```
ansible-playbook -i inventory/ -b -v -K cluster.yml 
```
Примечание: для выполнения необходимы права sudo

После завершения работы сценария Prometheus будет доступен по http://localhost:8080
Порт можно переопределить, см. ниже.
В разделе Graph можно выбрать интересующие метрики. 

### Настройки ###
Тестировалось физической машине (4CPU, 8GB RAM) под управлением Ubuntu 17.10
Заданные по умолчанию настройки подобраны под возможности тестовой машины.

При необходимости можно переопределить значения

| Файл                         | Переменная                | Описание                                                          | Примечание                                           |
|------------------------------|---------------------------|-------------------------------------------------------------------|------------------------------------------------------|
| inventory/hosts              | cpu                       | Число ядер ВМ                                                     |                                                      |
|                              | ram                       | Количество МБ RAM на ВМ                                           |                                                      |
| inventory/group_vars/all.yml | cassandra_requests_memory | Требуемое количество RAM на ноде kubernetes для запуска cassandra |                                                      |
|                              | cassandra_requests_cpu    | Требуемое количество CPU на ноде kubernetes для запуска cassandra |                                                      |
|                              | cassandra_heap_size       | Размер HEAP_SIZE jvm cassandra                                    |                                                      |
|                              | expose_port               | Номер порта по которому будет доступен prometheus на хосте        | Перед запуском убедиться, что укзанный порт свободен |

Для работы cassandra используется кастомный образ, его описание в images/cassandra