 Ansible Infra — 3-node managed environment

Управление тремя серверами (load balancer, app server, db server) через Ansible с единой control-машины.

 Стек
- Ansible, control node — отдельная VM на хосте
- Ubuntu (app/db/lb nodes)
- SSH key-based auth, `deployer` remote_user

 Inventory
​```ini
[balancers]
vm-lb ansible_host=192.168.1.48

[appservers]
vm-app ansible_host=192.168.1.49

[dbservers]
vm-db ansible_host=192.168.1.50

[production:children]
balancers
appservers
dbservers
​```

Что настроено
- appservers: git, базовая директория приложения
- balancers: nginx
- dbservers: postgresql

 Запуск
​```bash
ansible-playbook site.yml --check
ansible-playbook site.yml
​```

Структура
​```
ansible-project/
├── ansible.cfg
├── hosts
├── site.yml
├── group_vars/
│   └── all.yml
└── roles/          # roadmap
​```
