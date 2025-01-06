
# Установка и настройка TON ноды с мониторингом

## Установка TON ноды

Выполняйте все шаги согласно [официальной инструкции](https://docs.ton.org/v3/guidelines/nodes/running-nodes/full-node#run-the-mytonctrl).

Однако, перед выполнением пункта **Install the MyTonCtrl**, а именно перед командой:

```bash
sudo bash install.sh
```

Необходимо отредактировать файл `install.sh`. Замените дефолтные требования на `8/16` (строки 82 и 83), ИЛИ используйте настройки из корня репозитория.


## Установка API для TON ноды

1. Необходимо склонить репу к проектом:

```bash
git clone https://github.com/toncenter/ton-http-api.git
cd ton-http-api
```
В случае сетевой недоступности репозитория склонирован в текущую репу. 06.01.2025

2. Создать приватную папку и скачать туда ТОN-конфиги:

```bash
mkdir private
curl -sL https://ton-blockchain.github.io/global.config.json > private/mainnet.json
curl -sL https://ton-blockchain.github.io/testnet-global.config.json > private/testnet.json
```

3. Запустить **./configure.py** для создания  **.env** файла с переменным среды окружения.

4. Запустить докер-композ файл командой **docker compose up -d --build**

```bash
└── ton-http-api
    └── docker-compose.yaml
```

5. API будет доступно на порту 80 текущего IP.
В рамках тестов API доступно по адресу:
- **URL**: [161.35.220.86:80](http://161.35.220.86:80)
---

## Мониторинг

Мониторинг разделен на **серверную** и **клиентскую** часть. Используется **PULL модель** для сбора метрик.

### Серверная Часть

#### Grafana

- **URL**: [185.247.17.248:8080](http://185.247.17.248:8080)
- **Login**: `admin`
- **Password**: `PQ9JMfd3aepL`

#### Для поднятия Grafana требуется:

0. Скопируйте папку monitoring/server на сервер где будет запущена серверная часть

1. Запустите Docker Compose:

   ```bash
   └── monitoring
       └── server
           ├── docker-compose.yml
   ```

2. В Grafana добавьте источник данных Prometheus:
   - Перейдите в **Home > Connections > Data sources**.
   - Отключите аутентификацию (используйте только для тестов).
   - В поле **URL** укажите адрес Prometheus: `http://185.247.17.248:9090/`.

3. Добавьте дашборд:
   - Перейдите в **Home > Dashboards > New > Import**.
   - Укажите ID дашборда: `1860` (это дефолтный дашборд для **Node Exporter**).

---

### Клиентская Часть

0. Скопируйте папку monitoring/client на сервер где будет запущена клиентская часть

1. Запустите Docker Compose для клиентской части:

   ```bash
   └── monitoring
       ├── client
       │   └── docker-compose.yml
   ```

---

Теперь ваш мониторинг будет настроен и работать через Grafana, с данными из Prometheus и метриками с **Node Exporter**.
