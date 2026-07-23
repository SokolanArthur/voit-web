# VOIT Web Infrastructure

![Deploy Status](https://github.com/SokolanArthur/voit-web/actions/workflows/deploy.yml/badge.svg)(https://github.com/SokolanArthur/voit-web/actions)

Инфраструктура и CI/CD пайплайн для веб-проекта VOIT. Реализован базовый подход Infrastructure as Code (IaC) с автоматическим деплоем на VDS.

## Стек
* Docker / Docker Compose
* Nginx (Reverse Proxy)
* PostgreSQL 15 (Alpine) + pgAdmin 4
* GitHub Actions, GitHub Secrets, Let's Encrypt, Fail2Ban

## Архитектура и безопасность
* **Изоляция БД:** PostgreSQL и pgAdmin находятся во внутренней сети Docker, внешние порты закрыты.
* **Проксирование:** Доступ к панели pgAdmin реализован через Nginx по скрытому маршруту `/pgadmin/`.
* **HTTPS:** Настроен принудительный редирект с 80 на 443 порт, сертификаты автоматически обновляются через Certbot.
* **SECRETS:** Пароли и логины не хранятся в коде. Значения подтягиваются в скрытый `.env` файл динамически на этапе выполнения GitHub Actions.
* **Защита хоста:** На сервере работает Fail2Ban для анализа логов и автоматической блокировки вредоносных IP-адресов при попытках брутфорса.
