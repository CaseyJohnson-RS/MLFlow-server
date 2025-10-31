# Использование MLflow для трекинга экспериментов

MLflow - это инструмент для управления жизненным циклом машинного обучения, который предоставляет разработчикам и исследователям возможность отслеживать, управлять и развертывать модели машинного обучения. Одной из ключевых возможностей MLflow является трекинг экспериментов.  Он позволяет записывать параметры модели, метрики и артефакты (например, веса модели) во время обучения и сохранять их. Это позволяет легко сравнивать различные модели и эксперименты, а также повторять эксперименты с теми же параметрами.


MLflow поддерживает множество фреймворков машинного обучения, включая PyTorch и Sklearn. После завершения проведения экспериментов все записанные параметры, метрики и артефакты и сами модели будут сохранены (сохранить данные можно локально на компьютере или с использованием любой базы данных). Данные можно легко просмотреть с помощью удобного веб-интерфейса MLflow или использовать API для доступа.

Варианты поднятия сервиса:

![image](https://github.com/user-attachments/assets/13cda00d-54c5-4554-a76f-9c2ce5a4eb1d)

В данной **main** ветке представлен пример №3. Как раз тут развернем объектоное хранилище и базу данных с помощью docker-compose. <br/>
Если вас интересует самый простой вариант для локальной разработки (вариант №1), то его реализацию можете найти в ветке [local_mlflow](https://github.com/Koldim2001/MLflow_tracking/tree/local_mlflow)

---

## Запуск MLFlow + Postgres + MinIO

### Установка переменных окружения

Создайте файлик `.env`, в который добавьте примерно следующее:

```bash
# Postgres configuration
PG_USER=mlflow
PG_PASSWORD=mlflow
PG_DATABASE=mlflow
PG_PORT=5432

# MLflow configuration
MLFLOW_PORT=5001
MLFLOW_BUCKET_NAME=mlflow

# MinIO access keys - these are needed by MLflow
MINIO_ACCESS_KEY=NetzYOidILbYfa31Re9w
MINIO_SECRET_ACCESS_KEY=x66YtbX5xPrDQKvvr9IS7SAUJ3zaCpbl2MqP6MGk

# MinIO configuration
MINIO_ROOT_USER: 'minio_user'
MINIO_ROOT_PASSWORD: 'minio_pwd'
MINIO_ADDRESS: ':9000'
MINIO_STORAGE_USE_HTTPS: False
MINIO_CONSOLE_ADDRESS: ':9001'
MINIO_PORT=9000
MINIO_CONSOLE_PORT=9001
```

### Запуск сервисов

Выполните:

```bash
docker compose up -d
```

Когда контейнеры стартанут, на: 

* `http://localhost:9001/` будет доступен GUI Minio (логин/пароль – переменные `MINIO_ROOT_USER`/`MINIO_ROOT_PASSWORD` в `.env`);
* на `http://localhost:5050/` будет доступен GUI MLFlow;

---

### Предостережения

1. Проверьте правила хоста на разрешение соединений
2. Не используйте прокси при подключении к MLFlow 
