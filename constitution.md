# **PRD: Развертывание DeepTech-экосистемы "My Peak" (v.2026)**

Роль: Ты — Senior Fullstack Engineer и Архитектор Cloud-решений.  
Контекст: Мы создаем платформу спортивной аналитики My Peak. Нам нужно развернуть масштабируемую архитектуру (Monorepo) с фокусом на производительность и GEO (Generative Engine Optimization).

## **1\. Технологический Стек ("The Golden Stack 2026")**

* **Package Manager:** pnpm (обязательно использование Workspaces).  
* **Monorepo Tool:** Turborepo.  
* **Frontend (Public Web):** Astro 5.0 (Islands Architecture, Zero-JS by default).  
* **Frontend (SaaS App):** Next.js 15 \+ React Compiler (для Dashboard).  
* **CMS/Backend:** Payload CMS 3.0 (Self-hosted, PostgreSQL).  
* **Styling:** Tailwind CSS v4 (CSS-first config).  
* **UI Components:** Дизайн-система на базе Shadcn/ui \+ Magic UI (Bento Grid эстетика).

## **2\. Структура проекта (Monorepo)**

Структура проекта организована следующим образом:

Plaintext

/my-peak-ecosystem  
  ├── /apps  
  │    ├── /web (Astro 5.0 \- Лендинг, порт 5000)  
  │    └── /core (Next.js 15 \- Личный кабинет, порт 5001)  
  ├── /apps-cms (Payload 3.0 \- Админка и API, отдельный сервис)  
  ├── /packages  
  │    └── /ui (Общая дизайн-система Tailwind v4)  
  ├── pnpm-workspace.yaml  
  ├── turbo.json  
  └── package.json (Root)

**Примечание:** Payload CMS находится в отдельной папке `apps-cms/` для удобства разработки и может быть запущен независимо.

## **3\. Пошаговые задачи для выполнения**

### **Задача 1: Инициализация Monorepo**

1. Инициализируй корень через pnpm init.  
2. Настрой pnpm-workspace.yaml для папок apps/\* и packages/\*.  
3. Установи и настрой turbo глобально для оркестрации билдов.

### **Задача 2: Установка приложений (Scaffolding)**

1. **apps/web:** Установи Astro 5.0 (empty template). Добавь интеграцию @astrojs/tailwind (Tailwind v4).  
2. **apps/core:** Установи Next.js 15 (App Router, TS, Tailwind v4).  
3. **apps/cms:** Установи Payload 3.0 с адаптером db-postgres.

### **Задача 3: Настройка Дизайн-системы (Shared UI)**

1. В packages/ui создай базовую конфигурацию Tailwind CSS v4.  
2. Используй **OKLCH** цвета. Основная палитра: Темный фон (\#050505), Акцентный изумрудный (Emerald 500), Текст (Slate 200).  
3. Настрой общие шрифты (Inter или Geist).

### **Задача 4: GEO & Agent Readiness**

1. В apps/web/public создай файл llms.txt и llms-full.txt.  
2. Добавь в Astro базовую разметку Schema.org (тип Organization и SoftwareApplication).

### **Задача 5: Скрипты запуска и Деплоя**

1. В корневом package.json создай следующие скрипты:
   - `dev`: запуск всех приложений через Turborepo (apps/web + apps/core)
   - `dev-all`: запуск всех сервисов включая CMS
   - `dev:web`: запуск только Astro лендинга
   - `dev:core`: запуск только Next.js приложения
   - `dev:cms`: запуск только Payload CMS
2. Настрой конфиг для расширения **Natizyskunk SFTP** в .vscode/sftp.json для автоматизации выгрузки папки apps/web/dist на хостинг Reg.ru (IP: 31.31.197.38).

## **4\. Критерии приемки (Definition of Done)**

1. Команда `pnpm dev` запускает web и core без ошибок.  
2. Команда `pnpm dev-all` запускает все сервисы (web + core + cms) без ошибок.  
3. Отдельные скрипты (`dev:web`, `dev:core`, `dev:cms`) работают независимо.  
4. Astro (web) выдает 100/100 в Lighthouse (Performance/SEO).  
5. Payload CMS доступен по локальному порту и готов к созданию коллекций.  
6. Файл llms.txt доступен по адресу localhost:5000/llms.txt.
