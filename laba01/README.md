# Лабораторная 1 по Ansible

DebianTest001 - Админский ПК: 10.0.47.3

DebianTest102 - Тестовая машина: 10.0.47.102

DebianTest101 - Тестовая машина: 10.0.47.103

### Для админского ПК была использована следующая команда:

`ansible localhost -m setup -a "filter=ansible_all_ipv4_addresses,ansible_board_name,ansible_board_vendor,ansible_fqdn,ansible_os_family,ansible_uptime_seconds,ansible_user_id"`

### Результат:

```
[WARNING]: No inventory was parsed, only implicit localhost is available
localhost | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "10.0.47.3"
        ],
        "ansible_board_name": "VirtualBox",
        "ansible_board_vendor": "Oracle Corporation",
        "ansible_fqdn": "DebianTest001.home.local",
        "ansible_os_family": "Debian",
        "ansible_uptime_seconds": 1449,
        "ansible_user_id": "adminuser"
    },
    "changed": false
}
```

### Я добавил IP адреса в inventory.ini. Также на тестовых машинах стоит другой пользователь "debian", потому это тоже надо указать в команде:

`ansible test_machines -i inventory.ini -u debian -m setup -a "filter=ansible_all_ipv4_addresses,ansible_board_name,ansible_board_vendor,ansible_fqdn,ansible_os_family,ansible_uptime_seconds,ansible_user_id"`

### Результат:

```
[WARNING]: Host '10.0.47.102' is using the discovered Python interpreter at '/usr/bin/python3.13', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.19/reference_appendices/interpreter_discovery.html for more information.
10.0.47.102 | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "10.0.47.102"
        ],
        "ansible_board_name": "VirtualBox",
        "ansible_board_vendor": "Oracle Corporation",
        "ansible_fqdn": "DebianTest102.home.local",
        "ansible_os_family": "Debian",
        "ansible_uptime_seconds": 426,
        "ansible_user_id": "debian",
        "discovered_interpreter_python": "/usr/bin/python3.13"
    },
    "changed": false
}
[WARNING]: Host '10.0.47.103' is using the discovered Python interpreter at '/usr/bin/python3.13', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.19/reference_appendices/interpreter_discovery.html for more information.
10.0.47.103 | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "10.0.47.103"
        ],
        "ansible_board_name": "VirtualBox",
        "ansible_board_vendor": "Oracle Corporation",
        "ansible_fqdn": "TestDebian101.home.local",
        "ansible_os_family": "Debian",
        "ansible_uptime_seconds": 426,
        "ansible_user_id": "debian",
        "discovered_interpreter_python": "/usr/bin/python3.13"
    },
    "changed": false
}
```
