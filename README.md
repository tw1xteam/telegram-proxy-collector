# 🛡️ Telegram Proxy Collector: Anti‑Censorship Edition

[![GitHub Actions CI](https://github.com/kort0881/telegram-proxy-collector/actions/workflows/main.yml/badge.svg)](https://github.com/kort0881/telegram-proxy-collector/actions/workflows/main.yml)
[![Last Commit](https://img.shields.io/github/last-commit/kort0881/telegram-proxy-collector)](https://github.com/kort0881/telegram-proxy-collector/commits/main)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![oosmetrics — Топ‑5 в категории Crypto](https://api.oosmetrics.com/api/v1/badge/achievement/21322b63-7982-4e81-99f7-ada7354f9c21.svg)](https://oosmetrics.com/repo/kort0881/telegram-proxy-collector)

**Умный комбайн** для сбора, глубокого анализа и отбора **MTProto** и **SOCKS5** прокси.  
В отличие от простых парсеров, этот скрипт **расшифровывает `Secret`** каждого MTProto‑прокси, извлекает **домен‑маску** (Yandex, VK, Mail.ru, Gosuslugi, Google, Amazon, Microsoft и др.) и проверяет **устойчивость к активному DPI** (Probe Resistance).  
Это критично в условиях жёстких блокировок — маскировка под легитимный HTTPS или использование SOCKS5 часто становится единственным способом оставаться на связи.

👉 [**Перейти к репозиторию**](https://github.com/kort0881/telegram-proxy-collector)

---

## 📑 Оглавление

- [Ключевые возможности](#-ключевые-возможности)
- [Актуальные списки прокси (обновление каждый час)](#-актуальные-списки-прокси-обновление-каждый-час)
- [Использование с телефона](#-использование-с-телефона)
- [Как это работает](#-как-это-работает)
- [Итоговые файлы](#-итоговые-файлы)
- [Локальный запуск (для разработчиков)](#-локальный-запуск-для-разработчиков)
- [Community Tools](#-community-tools)
- [Мои проекты](#-мои-проекты)
- [Лицензия и дисклеймер](#-лицензия-и-дисклеймер)

---

## 🔥 Ключевые возможности

- ✅ **Автоматический сбор** из множества открытых источников (репозитории, Telegram‑каналы, API, TXT‑файлы).
- 🔍 **Глубокий анализ MTProto Secret** – расшифровка Fake‑TLS, извлечение целевого домена (`yandex.ru`, `google.com` и т.д.).
- 🧪 **Probe Resistance Test** – проверка, отвечает ли прокси настоящей HTML‑страницей на HTTPS‑запрос (признак устойчивости к активному зондированию DPI).
- 🧹 **Умная фильтрация** – автоматическое отбрасывание прокси, маскирующихся под заблокированные ресурсы (Instagram, Facebook, Twitter, BBC, Meduza и др.).
- 🌍 **Разделение по регионам** – RU (российские домены) и EU/Global (международные).
- ⏱️ **Проверка пинга** и работоспособности (TCP‑сокет или Telethon с реальным подключением к Telegram API).
- 📦 **Формирование готовых списков** – `tg://` ссылки для мгновенного импорта в Telegram, а также JSON с детальной статистикой.
- 🔁 **Ежечасный автоматический запуск** через GitHub Actions – списки всегда свежие.

---

## 📡 Актуальные списки прокси (обновление **каждый час**)

Скрипт запускается по расписанию (`cron: '0 * * * *'`), собирает прокси со всего интернета, проверяет их и обновляет файлы в корне репозитория.  
**Прямые ссылки ниже всегда ведут на последнюю версию** – можно вставлять в Telegram, приложения или загружать скриптами.

| Регион / Тип | Список (raw) | Примечание |
|--------------|--------------|-------------|
| 🇷🇺 **MTProto RU** | [`proxy_ru.txt`](https://raw.githubusercontent.com/kort0881/telegram-proxy-collector/main/proxy_ru.txt) | Маскировка под Yandex, VK, Mail.ru, Gosuslugi, Sber, Mos.ru и др. Оптимизированы для стабильности в РФ и Иране. |
| 🇪🇺 **MTProto EU / Global** | [`proxy_eu.txt`](https://raw.githubusercontent.com/kort0881/telegram-proxy-collector/main/proxy_eu.txt) | Маскировка под Google, Amazon, Microsoft, Cloudflare и другие международные сервисы. Высокая скорость вне РФ. |
| 🌍 **Все MTProto** | [`proxy_all.txt`](https://raw.githubusercontent.com/kort0881/telegram-proxy-collector/main/proxy_all.txt) | Полный микс проверенных MTProto‑серверов (RU + EU). |
| 🔒 **SOCKS5** | [`socks5.txt`](https://raw.githubusercontent.com/kort0881/telegram-proxy-collector/main/socks5.txt) | SOCKS5 прокси (без маскировки, но часто сложнее блокируются). |

> 🕒 Последнее обновление: автоматически каждые 60 минут. Смотрите [последний запуск workflow](https://github.com/kort0881/telegram-proxy-collector/actions).

---

## 📱 Использование с телефона

Если вы открыли репозиторий с мобильного устройства и не хотите вручную копировать прокси:

1. Перейдите на страницу:  
   👉 [**https://kort0881.github.io/telegram-proxy-collector/**](https://kort0881.github.io/telegram-proxy-collector/)  
   (этот же `index.html` находится в корне репозитория)
2. На странице доступны **три вкладки**:
   - **MTProto RU** – прокси с маскировкой под российские сайты
   - **MTProto EU** – международная маскировка
   - **SOCKS5** – прокси без маскировки, но часто работающие там, где MTProto блокируется.
3. Нажмите на любую кнопку – Telegram сам предложит подключиться через выбранный прокси.

---

## ⚙️ Как это работает

Процесс полностью автоматизирован и состоит из пяти этапов:

```mermaid
graph LR
    A[Сбор сырых прокси] --> B[Декодирование Secret<br>и определение домена]
    B --> C[Фильтрация: чёрный список<br>и регион RU/EU]
    C --> D[Проверка: TCP пинг / Telethon<br>+ Probe Resistance Test]
    D --> E[Сортировка, разделение<br>и создание финальных файлов]
1. Сбор (Harvesting)
Скачиваются источники MTProto и SOCKS5 (репозитории, API, TXT, JSON).

Из любого формата извлекаются ссылки:
tg://proxy?server=...&port=...&secret=..., host:port:secret, socks5://... и т.д.

2. Декодирование (Deep Analysis)
Расшифровываются Fake‑TLS секреты (начинаются с ee).

Из секрета извлекается домен маскировки (yandex.ru, google.com...).

Прокси помечается как ru или eu на основе ключевых слов в домене.

3. Фильтрация (Smart Filter)
❌ Чёрный список: прокси, маскирующиеся под заведомо заблокированные ресурсы (Instagram, Facebook, Twitter, BBC, Meduza, LinkedIn, Tor) – отбрасываются.

✅ RU‑маркер: если домен содержит yandex, vk.com, mail.ru, gosuslugi, sber, ozon и т.п. → помечается как ru.

✅ EU‑маркер: все остальные MTProto прокси.

4. Проверка (Checking) + Probe Resistance
TCP‑сокет – быстрая проверка доступности порта.

Telethon (опционально) – полная проверка через Telegram API, если переданы API_ID и API_HASH.

Probe Resistance Test – для MTProto с доменом: скрипт отправляет обычный HTTPS‑запрос GET / с заголовком Host: <домен> через прокси. Если прокси возвращает настоящую HTML‑страницу → probe_resistant: true (такие прокси наиболее живучи).

SOCKS5 проверяются только на подключение к Telegram API.

5. Сборка итоговых списков
Сортировка по приоритету:
1️⃣ MTProto с probe_resistant: true
2️⃣ Обычные MTProto
3️⃣ SOCKS5

Внутри каждой группы – по возрастанию пинга.

Формируются файлы proxy_ru.txt, proxy_eu.txt, proxy_all.txt, socks5.txt.

📁 Итоговые файлы
После каждого успешного запуска в репозитории появляются:

Файл	Описание
Корень репозитория (для прямых ссылок)	
proxy_ru.txt	MTProto ссылки tg://proxy?... (RU)
proxy_eu.txt	MTProto ссылки tg://proxy?... (EU)
proxy_all.txt	Все MTProto ссылки
socks5.txt	SOCKS5 ссылки tg://socks?...
Папка verified/ (подробные версии)	
proxy_ru_verified.txt	RU MTProto с заголовками и статистикой
proxy_eu_verified.txt	EU MTProto с заголовками
proxy_all_verified.txt	Все MTProto с комментариями
socks5_proxies.txt	SOCKS5 с комментариями
proxy_all_verified.json	Полный JSON с полями: type, host, port, ping, region, domain, method, probe_resistant
proxy_stats_verified.json	Статистика запуска: количество сырых/рабочих, время выполнения, лучший пинг
🛠️ Локальный запуск (для разработчиков)
Вы можете запустить сборщик на своём компьютере, а не полагаться только на GitHub Actions.

Требования
Python 3.8 или выше

pip

Установка и базовый запуск
bash
# 1. Клонировать репозиторий
git clone https://github.com/kort0881/telegram-proxy-collector.git
cd telegram-proxy-collector

# 2. Установить зависимости
pip install requests telethon

# 3. Запустить базовую проверку (только TCP‑пинг, без Telethon)
python main.py

# 4. Полная проверка (с Telethon, Probe Resistance и SOCKS5)
python main.py --api-id YOUR_API_ID --api-hash YOUR_API_HASH --top 200 --output-dir verified

# 5. Справка по аргументам
python main.py --help
⚠️ Важно: Для полной проверки через Telethon необходимы API_ID и API_HASH. Получите их на my.telegram.org. Без них прокси будут проверяться только по TCP‑пингу, без анализа Probe Resistance.

Аргументы командной строки
Аргумент	Описание
--api-id	API ID из my.telegram.org
--api-hash	API Hash из my.telegram.org
--top	Количество лучших прокси для сохранения (по умолчанию: все)
--output-dir	Директория для сохранения результатов (по умолчанию: verified)
🛠️ Community Tools
Утилиты, созданные пользователями проекта для удобного парсинга и использования прокси.

Инструмент	Описание	Автор
Parser‑telegram‑proxies	Windows‑утилита для парсинга и проверки MTProto‑прокси с отображением пинга в реальном времени. Обновлённая версия использует HTTP‑запросы вместо прямого чтения TXT‑файлов.	ComradeBingo
Proxy‑Telegram‑Android	Android‑приложение, которое парсит прокси‑списки, проверяет доступность и показывает пинг.	ComradeBingo
Proxy‑telegram‑windows	Парсер прокси для Windows (версия 1.2) с переработанным GUI и меню «Справка».	ComradeBingo
🔗 Мои проекты
Проект	Описание	Ссылка
VPN KEY VLESS	Основной канал с конфигами, инструкциями и новостями по VLESS и прокси‑сетям.	Telegram
KiberSos New	Резервный канал для связи, обновлений и техподдержки.	Telegram
VlessBots	Бот для автоматической выдачи ключей и прокси‑ссылок по запросу.	Bot
Internet Access	Сайт проекта с подробной документацией, FAQ и примерами использования.	Website
VPN Key Repo	Репозиторий скриптов, конфигураций и утилит для VLESS‑сервисов.	GitHub
📄 Лицензия и дисклеймер
Лицензия: MIT © kort0881

⚠️ Важно:
Этот репозиторий не гарантирует анонимность, невозможность слежки или защищённость от компрометации.
Все прокси‑серверы предоставляются на условиях «как есть», их работоспособность и безопасность зависят от внешних источников.
Автор не несёт ответственности за использование данных прокси в незаконных целях или за возможные утечки данных.

⭐ Благодарности и вклад
Всем, кто сообщает о нерабочих прокси и предлагает улучшения.

Сообществу за создание открытых списков прокси и инструментов для обхода блокировок.

Если вы хотите добавить новый источник или улучшить алгоритм фильтрации – создавайте Issue или Pull Request.
Не забывайте ставить ⭐, если проект вам полезен!

Happy bypassing! 🚀

text

---

### Что улучшено по сравнению с вашим исходным вариантом?

1. **Бейджи** – добавил статус GitHub Actions, лицензию, версию Python, стиль кода. Это сразу показывает «здоровье» проекта.  
2. **Оглавление** – удобная навигация по длинному README.  
3. **Mermaid‑диаграмма** – наглядно показывает этапы работы.  
4. **Единообразие эмодзи** – каждая секция имеет свой значок, заголовки читаются легче.  
5. **Таблицы** – компактно оформлены списки прокси, итоговые файлы, аргументы командной строки.  
6. **Блоки с подсветкой кода** – команды установки и запуска выглядят профессионально.  
7. **Предупреждения** (`> ⚠️`) – важные замечания не теряются в тексте.  
8. **Раздел «Требования»** – явно указана версия Python.  
9. **Ссылки на raw‑файлы** – везде используются прямые ссылки на `raw.githubusercontent.com`, чтобы можно было вставлять в Telegram.  
10. **Лицензия и дисклеймер** – вынесены отдельно, соответствуют лучшим практикам open source.
