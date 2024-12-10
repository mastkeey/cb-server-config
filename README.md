# Конфигурация сервера для микросервисной архитектуры

Этот репозиторий содержит файлы конфигурации для инструментов, используемых в управлении и мониторинге микросервисов.

⚠️ **Важно:** Все конфигурационные файлы используются вручную для настройки инструментов на уже подготовленном сервере.

## Содержание

- [Обзор](#обзор)
- [Структура репозитория](#структура-репозитория)
- [Описание Docker Compose](#описание-docker-compose)
- [Описание конфигураций](#описание-конфигураций)

---

## Обзор

В репозитории собраны конфигурационные файлы и инструкции для следующих инструментов:
- **Docker Compose**: Для упрощения запуска контейнеров.
- **Prometheus**: Система мониторинга и алертинга.
- **Grafana**: Для визуализации данных и метрик.
- **Logstash**: Управление логами.
- **PostgreSQL**: База данных.
- **MinIO**: Объектное хранилище.

---

## Структура репозитория
```text
cb-server-config/
│
├── config/
│   ├── grafana/
│   │   ├── provisioning/
│   │   │   ├── dashboards/       # Настройки дашбордов Grafana
│   │   │   ├── datasources/      # Настройки источников данных Grafana
│   │   ├── Dockerfile            # Dockerfile для Grafana
│   ├── logstash.conf             # Конфигурация Logstash
│   ├── prometheus.yml            # Конфигурация Prometheus
│
├── .env                          # Файл с переменными окружения
├── .gitignore                    # Исключения для Git
├── docker-compose.yml            # Основной файл оркестрации
└── README.md                     # Описание проекта
```
---

## Описание Docker Compose

Файл `docker-compose.yml` обеспечивает удобный запуск всех контейнеров для инструментов мониторинга и управления инфраструктурой.

Сервисы:
- `cb-cloud-service`: Основной микросервис, использующий PostgreSQL и MinIO.
- `cb-bot-service`: Сервис для бота, взаимодействующий с `cb-cloud-service`.
- `prometheus`: Для сбора метрик.
- `grafana`: Для визуализации данных из Prometheus.
- `logstash`: Для обработки логов.
- `kibana` и `es`: Для управления логами через стек Elasticsearch.

Сетевые настройки и переменные окружения (файл `.env`) позволяют настраивать контейнеры под конкретное окружение.

---

## Описание конфигураций

- **`config/grafana/`**
    - Настройки для автоматического создания источников данных и дашбордов в Grafana.
- **`config/logstash.conf`**
    - Обработка логов и отправка в Elasticsearch.
- **`config/prometheus.yml`**
    - Конфигурация для сбора метрик из Docker-контейнеров.