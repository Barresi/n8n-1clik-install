# Скрипт установки n8n на Ubuntu VPS

## Описание
Этот скрипт автоматически устанавливает и настраивает n8n на Ubuntu VPS с поддержкой SSL через Let's Encrypt.

## Поддерживаемые версии Ubuntu
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS

## Возможности
- ✅ Автоматическая установка Docker и Docker Compose
- ✅ Настройка домена и SSL сертификатов
- ✅ Проверка существующих контейнеров и volumes
- ✅ Создание и проверка конфигурационных файлов (docker-compose.yml, .env)
- ✅ Валидация синтаксиса Docker Compose файлов
- ✅ Настройка автозапуска при перезагрузке сервера
- ✅ Поддержка различных сценариев установки

## Использование

### Первая установка
```bash
sudo ./install-n8n.sh
```

### Управление установленным n8n
```bash
# Обновление n8n
sudo ./install-n8n.sh --update

# Остановка n8n
sudo ./install-n8n.sh --stop

# Перезапуск n8n
sudo ./install-n8n.sh --restart

# Проверка конфигурационных файлов
sudo ./install-n8n.sh --check

# Справка
sudo ./install-n8n.sh --help
```

## Требования
- Ubuntu VPS с root доступом или sudo
- Домен, указывающий на IP сервера
- Доступ к интернету

## Структура файлов
После установки создается директория `n8n-compose/` со следующими файлами:
- `docker-compose.yml` - конфигурация Docker Compose
- `.env` - переменные окружения
- `local-files/` - директория для локальных файлов

## Управление после установки

### Просмотр логов
```bash
cd n8n-compose
docker compose logs -f
```

### Управление сервисом
```bash
sudo systemctl start n8n
sudo systemctl stop n8n
sudo systemctl restart n8n
sudo systemctl status n8n
```

### Резервное копирование
```bash
cd n8n-compose
docker compose down
docker volume ls  # найти volume n8n
docker run --rm -v n8n_n8n_data:/data -v $(pwd):/backup alpine tar czf /backup/n8n-backup.tar.gz -C /data .
```

## Решение проблем

### Ошибка "cd: n8n-compose: No such file or directory"
Убедитесь, что скрипт запущен из правильной директории и что у вас есть права на создание файлов.

### Проблемы с SSL сертификатами
Если сертификаты не выдают, проверьте:
1. Корректность DNS записей
2. Доступность портов 80 и 443
3. Правильность email адреса

### Ошибки Docker
```bash
# Проверить статус Docker
sudo systemctl status docker

# Перезапустить Docker
sudo systemctl restart docker
```

## Безопасность
- Скрипт требует root прав только для установки системных пакетов
- n8n работает в изолированном Docker контейнере
- SSL сертификаты автоматически обновляются через Let's Encrypt

## Контакты
Для вопросов и предложений обращайтесь в Telegram-канал https://t.me/JumbleAI
