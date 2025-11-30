# Ansible Role: lighthouse-role

Ansible роль для установки и настройки Lighthouse - инструмента анализа производительности веб-приложений от VKCOM.

## Описание

Эта роль устанавливает веб-сервер Nginx, скачивает статические файлы Lighthouse с GitHub и настраивает Nginx для их обслуживания.

## Требования

- Ansible >= 2.9
- Система на базе Debian/Ubuntu
- Права root или sudo
- Интернет-соединение для скачивания файлов Lighthouse

## Переменные роли

### Переменные по умолчанию

| Переменная | Значение по умолчанию | Описание |
|-----------|----------------------|----------|
| `lighthouse_download_url` | `"https://github.com/VKCOM/lighthouse/archive/refs/heads/master.zip"` | URL для скачивания архива Lighthouse |
| `lighthouse_archive_path` | `/tmp/lighthouse.zip` | Локальный путь, куда будет скачан архив |
| `lighthouse_extracted_path` | `/tmp/lighthouse-master` | Путь к распакованной директории Lighthouse |
| `lighthouse_web_root` | `/var/www/lighthouse` | Корневая директория веб-сервера |
| `lighthouse_web_server` | `nginx` | Имя пакета веб-сервера |
| `lighthouse_nginx_config_path` | `/etc/nginx/sites-available/lighthouse` | Путь к файлу конфигурации Nginx |
| `lighthouse_nginx_site_enabled_path` | `/etc/nginx/sites-enabled/lighthouse` | Путь к включенному сайту Nginx |
| `lighthouse_nginx_default_site_path` | `/etc/nginx/sites-enabled/default` | Путь к сайту Nginx по умолчанию |
| `lighthouse_download_timeout` | `300` | Таймаут скачивания в секундах |
| `lighthouse_apt_cache_valid_time` | `3600` | Время валидности кэша APT в секундах |

### Пример Playbook

```yaml
---
- hosts: lighthouse
  become: true
  roles:
    - lighthouse-role
```

### Настройка переменных

Вы можете переопределить переменные по умолчанию:

```yaml
---
- hosts: lighthouse
  become: true
  vars:
    lighthouse_web_root: /var/www/html/lighthouse
    lighthouse_web_server: nginx
  roles:
    - lighthouse-role
```

## Зависимости

Нет

## Что делает эта роль

1. Обновляет кэш APT
2. Устанавливает пакеты Nginx и unzip
3. Создает корневую директорию веб-сервера
4. Скачивает статические файлы Lighthouse с GitHub
5. Распаковывает архив
6. Копирует файлы в корневую директорию веб-сервера
7. Настраивает Nginx для обслуживания Lighthouse
8. Включает сайт Lighthouse
9. Удаляет сайт Nginx по умолчанию
10. Запускает и включает сервис Nginx

## Пример использования

```yaml
---
- name: Установка Lighthouse
  hosts: lighthouse
  become: true
  roles:
    - lighthouse-role
```

После установки Lighthouse будет доступен по адресу `http://<ip-адрес-хоста>/`

## Лицензия

MIT

## Информация об авторе

Эта роль была создана в рамках проекта курса Ansible.
