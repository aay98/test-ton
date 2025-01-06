### Установка TON ноды
Выполнять согласно Инструкции: https://docs.ton.org/v3/guidelines/nodes/running-nodes/full-node#run-the-mytonctrl
    Однако перед выполнением пункта *Install the MyTonCtrl*
    А именно перед командой sudo bash install.sh
    Отредактировать файл install.sh - необходимо заменить дефолтные требования 8/16 (строки 82 и 83) ИЛИ использовать из корня репозитория.


### мониторинг
Разделен на серверную и клиентскую часть (Реализация по PULL модели)
## Серверная Часть
Grafana 
url: 185.247.17.248:8080
login: admin
pass: PQ9JMfd3aepL

Для поднятия графаны требуется:
1) Запустить докер-композ
└── monitoring
    └── server
        ├── docker-compose.yml
2) Добавить в *Home > Connections > Data sources* Источник данных Prometheus. Атентификация отключена (ИСПОЛЬЗОВАТЬ ТОЛЬКО ДЛЯ ТЕСТОВЫХ СРЕД). Добавить url прометеуса в рамках теста http://185.247.17.248:9090/
3) Добавить дашборд в * Home > Dashboards > New > Import* Указать ID *1860*. (Добавление дефолтного Node-Exporter дашборда)

## Клиентская Часть
1) Запустить докер-композ
└── monitoring
    ├── client
    │   └── docker-compose.yml