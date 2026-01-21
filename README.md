# My Peak Ecosystem v2026

**DeepTech-платформа спортивной аналитики** с фокусом на производительность и GEO (Generative Engine Optimization).

---

## 🏗️ Архитектура

Проект организован как **Monorepo** с использованием:
- **pnpm Workspaces** — управление зависимостями
- **Turborepo** — оркестрация билдов и задач
- **Tailwind CSS v4** — единая дизайн-система

---

## 📁 Структура проекта

```
/my-peak-landing
├── /apps
│   ├── /web          # Astro 5.0 - Публичный лендинг (порт 5000)
│   └── /core         # Next.js 15 - SaaS Dashboard (порт 5001)
├── /apps-cms         # Payload CMS 3.0 - Админка и API (отдельный сервис)
├── /packages
│   └── /ui           # Общая дизайн-система (Tailwind v4, OKLCH цвета)
├── pnpm-workspace.yaml
├── turbo.json
└── package.json
```

---

## 🚀 Быстрый старт

### Установка зависимостей

```bash
pnpm install
```

### Запуск всех сервисов

```bash
# Запуск web + core через Turborepo
pnpm dev

# Запуск всех сервисов (web + core + cms)
pnpm dev-all
```

### Запуск отдельных сервисов

```bash
# Только Astro лендинг (порт 5000)
pnpm dev:web

# Только Next.js Dashboard (порт 5001)
pnpm dev:core

# Только Payload CMS (порт 3000 по умолчанию)
pnpm dev:cms
```

---

## 📦 Приложения

### 1. **apps/web** — Astro 5.0 (Лендинг)

**Технологии:**
- Astro 5.0 (Islands Architecture, Zero-JS by default)
- Tailwind CSS v4 через `@tailwindcss/vite`
- Schema.org разметка (Organization, SoftwareApplication)
- GEO файлы: `llms.txt`, `llms-full.txt`

**Порт:** `5000`  
**URL:** http://localhost:5000

**Команды:**
```bash
cd apps/web
pnpm dev      # Запуск dev сервера
pnpm build    # Production билд
pnpm preview   # Превью production билда
```

**Особенности:**
- Оптимизирован для SEO и производительности
- Zero-JS по умолчанию (Islands Architecture)
- Файлы для AI агентов доступны по `/llms.txt` и `/llms-full.txt`

---

### 2. **apps/core** — Next.js 15 (SaaS Dashboard)

**Технологии:**
- Next.js 15 (App Router)
- React 19
- Tailwind CSS v4
- TypeScript

**Порт:** `5001`  
**URL:** http://localhost:5001

**Команды:**
```bash
cd apps/core
pnpm dev      # Запуск dev сервера
pnpm build    # Production билд
pnpm start    # Запуск production сервера
```

**Особенности:**
- App Router архитектура
- Использует общую дизайн-систему из `packages/ui`

---

### 3. **apps-cms** — Payload CMS 3.0 (Админка и API)

**Технологии:**
- Payload CMS 3.0
- Next.js 15
- PostgreSQL (через `@payloadcms/db-postgres`)
- GraphQL API

**Порт:** `3000` (по умолчанию)  
**URL:** http://localhost:3000/admin

**Команды:**
```bash
cd apps-cms
pnpm dev              # Запуск dev сервера
pnpm build            # Production билд
pnpm generate:types   # Генерация TypeScript типов
pnpm payload         # Payload CLI команды
```

**Особенности:**
- Self-hosted CMS
- PostgreSQL база данных
- GraphQL и REST API
- Админ-панель доступна по `/admin`

**Настройка БД:**
Создай файл `.env` в `apps-cms/`:
```env
DATABASE_URI=postgresql://user:password@localhost:5432/mypeak
PAYLOAD_SECRET=your-secret-key
```

---

## 🎨 Дизайн-система (packages/ui)

**Технологии:**
- Tailwind CSS v4 (CSS-first config)
- OKLCH цвета
- Geist/Inter шрифты

**Цветовая палитра:**
- **Background:** `oklch(12.72% 0.01 285.63)` — темный фон (#050505)
- **Foreground:** `oklch(89.33% 0.01 249.58)` — текст (Slate 200)
- **Accent:** `oklch(70.5% 0.15 162.5)` — изумрудный (Emerald 500)

**Использование:**
```css
@import "@my-peak/ui/styles";
```

Или через относительный путь:
```css
@import "../../../packages/ui/src/styles/globals.css";
```

---

## 🔧 Конфигурация

### Порты

- **Astro (web):** `5000`
- **Next.js (core):** `5001`
- **Payload CMS:** `3000` (по умолчанию)

### Workspace зависимости

Все приложения используют общий пакет `@my-peak/ui` через workspace protocol:
```json
{
  "dependencies": {
    "@my-peak/ui": "workspace:*"
  }
}
```

---

## 📤 Деплой

### SFTP деплой (Reg.ru)

Конфигурация находится в `.vscode/sftp.json`:
- **Хост:** `31.31.197.38`
- **Путь:** `/www/mypeak.ru`
- **Контекст:** `./apps/web/dist` (после `pnpm build` в apps/web)

**Использование:**
1. Собери проект: `cd apps/web && pnpm build`
2. Используй расширение SFTP в VS Code для загрузки `dist/` на сервер

---

## 🧪 Тестирование

### Lighthouse (Performance/SEO)

```bash
# После запуска apps/web
npx lighthouse http://localhost:5000 --view
```

**Цель:** 100/100 по Performance и SEO

---

## 📋 Скрипты (корневой package.json)

| Команда | Описание |
|---------|----------|
| `pnpm dev` | Запуск web + core через Turborepo |
| `pnpm dev-all` | Запуск всех сервисов (web + core + cms) |
| `pnpm dev:web` | Только Astro лендинг |
| `pnpm dev:core` | Только Next.js Dashboard |
| `pnpm dev:cms` | Только Payload CMS |
| `pnpm build` | Билд всех приложений |
| `pnpm build:web` | Билд только web |
| `pnpm build:core` | Билд только core |
| `pnpm build:cms` | Билд только cms |
| `pnpm lint` | Линтинг всех приложений |

---

## 🔍 GEO & Agent Readiness

### Файлы для AI агентов

- **`/llms.txt`** — краткая информация о проекте
- **`/llms-full.txt`** — полная документация для AI агентов

**Доступ:** http://localhost:5000/llms.txt

### Schema.org разметка

В `apps/web/src/layouts/Layout.astro` добавлена разметка:
- **Organization** — информация о компании
- **SoftwareApplication** — информация о приложении

---

## 🐛 Troubleshooting

### Проблема: CSS не резолвится в Next.js

**Решение:** Используй относительный путь вместо workspace alias:
```css
@import "../../../../packages/ui/src/styles/globals.css";
```

### Проблема: Payload CMS не запускается

**Проверь:**
1. Наличие `.env` файла с `DATABASE_URI`
2. Доступность PostgreSQL базы данных
3. Правильность порта (может быть занят)

### Проблема: Порты заняты

Измени порты в соответствующих `package.json`:
- `apps/web/package.json` → `"dev": "astro dev --port 5000"`
- `apps/core/package.json` → `"dev": "next dev -p 5001"`

---

## 📚 Дополнительная документация

- **PRD/Constitution:** `constitution.md`
- **Astro Docs:** https://docs.astro.build
- **Next.js Docs:** https://nextjs.org/docs
- **Payload CMS Docs:** https://payloadcms.com/docs
- **Turborepo Docs:** https://turbo.build/repo/docs

---

## 👥 Разработка

### Git Workflow

Репозиторий: `git@gitlab.com:mypeak/my-peak-website.git`

**Ветки:**
- `main` — production-ready код
- `develop` — разработка новых фич

### Code Style

- **TypeScript** — строгая типизация
- **ESLint** — линтинг кода
- **Prettier** — форматирование (где применимо)

---

## 📝 Changelog

### v2026.1 (Текущая версия)

- ✅ Monorepo структура с pnpm Workspaces
- ✅ Astro 5.0 лендинг с Tailwind v4
- ✅ Next.js 15 Dashboard
- ✅ Payload CMS 3.0 интеграция
- ✅ Общая дизайн-система (packages/ui)
- ✅ GEO файлы и Schema.org разметка
- ✅ SFTP деплой конфигурация

---

**Built with ❤️ for My Peak Team**
