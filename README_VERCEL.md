# Игорёк Clicker — подготовка под Vercel

Проект теперь подготовлен как статическая браузерная игра + serverless API Vercel.

## Что добавлено

- Логин игрока при первом запуске.
- Уникальный ID игрока генерируется на клиенте при первом входе и сохраняется.
- Онлайн-таблица лидеров по кубкам.
- API для сохранения публичных данных игрока.
- Подготовка под базу данных Vercel Postgres / Neon.

## Структура

```text
index.html
style.css
js/game.js
js/vercel-api.js
api/db.js
api/player.js
api/leaderboard.js
assets/
sounds/
data/
```

## API

### POST /api/player

Сохраняет/обновляет игрока в базе.

Поля:

```json
{
  "playerId": "IG-ABCD-123456",
  "username": "IgorekPro",
  "cups": 10,
  "level": 12,
  "coins": 5000,
  "currentSkin": "Defaut",
  "save": {}
}
```

### GET /api/player?playerId=...

Получить игрока по ID.

### GET /api/leaderboard?limit=25

Получить топ игроков по кубкам.

## База данных

Используется `@vercel/postgres`.

На Vercel нужно подключить Postgres Storage или Neon и добавить переменные окружения, которые Vercel создаёт автоматически:

```text
POSTGRES_URL
POSTGRES_PRISMA_URL
POSTGRES_URL_NON_POOLING
POSTGRES_USER
POSTGRES_HOST
POSTGRES_PASSWORD
POSTGRES_DATABASE
```

Таблица создаётся автоматически при первом API-запросе:

```sql
CREATE TABLE IF NOT EXISTS igorek_players (...)
```

## Как запустить локально

Статический тест без API:

```bash
python3 -m http.server 8000
```

Полный тест Vercel API:

```bash
npm install
npx vercel dev
```

Для локальной базы нужны переменные Postgres в `.env.local`.

## Как залить на Vercel

1. Создай проект на Vercel.
2. Загрузи папку проекта или подключи GitHub.
3. Подключи Vercel Postgres / Neon Storage.
4. Сделай Deploy.
5. Проверь `/api/leaderboard`.

Если база ещё не подключена, игра всё равно запускается, но лидерборд будет в локальном fallback-режиме.
