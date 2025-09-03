<div align="center">

# AIRESTO — система управления бронированиями ресторана

[![Vue 3](https://img.shields.io/badge/Vue_3-42b883?style=for-the-badge&logo=vue.js&logoColor=white)](https://vuejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178c6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vite.dev/)
[![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-2088FF?style=for-the-badge&logo=github&logoColor=white)](https://pages.github.com/)
[![Render](https://img.shields.io/badge/Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)](https://render.com/)

</div>

<p align="center">
  <a href="https://danula-ded.github.io/ariesto/" target="_blank">
    <img alt="Open site" src="https://img.shields.io/badge/ОТКРЫТЬ_САЙТ-GitHub_Pages-2ea44f?style=for-the-badge&logo=github&logoColor=white" />
  </a>
</p>

## Live

- Фронтенд (GitHub Pages): https://danula-ded.github.io/ariesto/
- Бэкенд (Render): https://ariesto.onrender.com

## Описание

Веб‑приложение для просмотра и управления бронированиями и заказами в ресторане. Интерфейс представляет сетку по столам и времени с возможностью создавать записи (drag‑to‑create) и быстро фильтровать данные.

## Функциональность

- Просмотр бронирований и заказов в виде тайм‑линии по столам
- Переключение дат (список доступных дат формируется автоматически)
- Фильтрация по зонам (1 этаж, 2 этаж, Банкетный зал)
- Создание заказа перетаскиванием мыши (Drag To Create)
- Фиксированные заголовки (столы и время) при прокрутке

## Основные эндпоинты (для проверки)

Базовый URL API: `https://ariesto.onrender.com`

- GET `/api/available-days` — список доступных дат (на 7 дней вперёд)
- GET `/api/restaurant` — информация о ресторане (id, таймзона, название)
- GET `/api/reservations/:date` — сводка по столам на дату `YYYY-MM-DD`
  - пример: https://ariesto.onrender.com/api/reservations/2025-01-01
- GET `/api/orders/:date` — все заказы на дату `YYYY-MM-DD`
  - пример: https://ariesto.onrender.com/api/orders/2025-01-01
- GET `/api/reservations/search/:query` — поиск по имени/статусу
  - пример: https://ariesto.onrender.com/api/reservations/search/ivan
- POST `/api/orders` — создание заказа (JSON тело)
- DELETE `/api/orders/:id` — удаление заказа

> Примечание: сервис хранит данные в файловом persistence на стороне бэкенда, при первом запуске генерирует демонстрационные записи на текущий день.

## Макет и Swagger

- Макет: см. раздел задания (pdf/figma, прилагается к проекту)
- Swagger (если подключён): `https://ariesto.onrender.com/api-docs`

## Технологии

- Vue 3 (Composition API), TypeScript, Vite
- Express 5, Node.js 20, CORS
- CSS (Grid, Flexbox)

## Локальный запуск

Корневые скрипты:

```bash
# установить зависимости для корня, фронта и бэка
npm run install:all

# запустить фронт и бэк вместе (разработка)
npm run dev
```

Переменные окружения фронта (опционально через `.env`):

- `VITE_API_BASE_URL_PROD` — продовый адрес API (по умолчанию `https://ariesto.onrender.com`)
- `VITE_API_BASE_URL_DEV` — адрес API в dev (по умолчанию `http://localhost:3000`)

## Деплой

### Фронтенд → GitHub Pages

В корне проекта:

```bash
npm run deploy:frontend   # установит зависимости фронта, соберёт и задеплоит
```

Настройки в репозитории: Settings → Pages → Branch = `gh-pages`.

### Бэкенд → Render

В корне уже есть `render.yaml`, который:

```yaml
services:
  - type: web
    name: ariesto-backend
    env: node
    plan: free
    buildCommand: cd backend && npm install && npm run build
    startCommand: cd backend && npm start
    envVars:
      - key: NODE_ENV
        value: production
      - key: PORT
        value: 3000
```

Создайте сервис из репозитория — Render подхватит конфигурацию автоматически.

## Структура проекта

```
backend/   # Express API
frontend/  # Vue 3 + Vite
```

## Лицензия

MIT
