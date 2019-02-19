# promon

## Как это использовать

Есть 2 роли: 
`slave` - устанавливается на ноды на которых работают только экспортеры
`master` - устанавливает основные компоненты Prometheus и Grafana

### Slave

В данный момент ставит только `node-exporter`

Что можно исправить

`./slave/.env`

```.env
NODE_EXPORTER_VERSION=v0.17.0
NODE_EXPORTER_PORT=9100
REPO=myrepo/
```
В итоге получим: `myrepo/prom/node-exporter:v0.17.0`

### Master

Что можно исправить

`./master/.env`

```.env
REPO=

# Prometheus
PROMETHEUS_PORT= 9090
PROMETHEUS_VERSION=v2.7.1
PROMETHEUS_DATA=/data/prometheus

#Grafana
GRAFANA_PORT=3000
GRAFANA_VERSION=5.4.3
GRAFANA_DATA=/data/grafana

#Pushgateway
PUSH_GATEWAY_PORT=9091
PUSHGATEWAY_VERSION=v0.7.0

#Nodeexporter
NODE_EXPORTER_PORT=9100
NODE_EXPORTER_VERSION=v0.17.0

#Alert manager
ALERTMANAGER_PORT=9093
ALERTMANAGER_VERSION=v0.16.1

```

#### Что нужно дополнить
---

`./master/prometheus/prometheus.yml`

Адреса машин

`./master/prometheus/target.json`

Можно добавлять адреса приложений без перезапуска Prometheus

`./master/grafana/datasource/Prometheus.yml`

Путь до Prometheus

`./master/alertmanager/config.yml`

Настроить инструменты для Нотификации

## Как собрать
```bash
./gradlew build
```

Очистить

```bash
./gradlew clean
```

## Как запустить

```bash
docker-compose --file slave/docker-compose.yml up
docker-compose --file master/docker-compose.yml up
```