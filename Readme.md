# Домашнее задание к занятию "8.4 Работа с Roles"  

Данный плейбук производит установку и базовую настройку Elasticsearch, Kibana и Filebeat при помощи соответствующих ролей Ansible.  

Структура плейбука:  
```
├── inventory
│   └── prod
│       ├── group_vars
│       │   └── all.yml
│       └── hosts.yml
└── playbooks
    ├── site.yml
    └── requirements.yml
```

В inventory объявлены 3 группы хостов - elasticsearch, kibana, filebeat.
Установка Elasticsearch и Kibana производится на отдельные хосты, Filebeat - на хосты, с которых нужно собирать логи.  
Возможна установка на ОС семейства Debian и RHEL.  
Если скачать дистрибутивы напрямую с сайта производителя нельзя из-за ограничений, параметры elastic_rpm_url, kibana_rpm_url, filebeat_rpm_url
позволяют задать альтернативные ссылки для скачивания. Возможно указание конкретных версий ПО с помощью параметра `elk_stack_version`.  
**Для корректной работы необходимо подставить IP-адреса соответствующих хостов в файл invenory/prod/hosts.yml**  

Файл requirements.yml содержит параметры установки ролей elastic-role, kibana-role, filebeat-role. Для установки запустите  
`ansible-galaxy install -r requirements.yml`

Собственно плейбук site.yml применяет установленные роли к хостам в inventory.

Для запуска вылоните: `ansible-playbook -i inventory/prod/hosts.yml playbooks/site.yml`

