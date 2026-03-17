# GeoInfo — Deploy Guide

## Структура проекту
```
geoinfo/
├── index.html       ← головна сторінка
├── admin.html       ← адмінка (тільки для тебе)
├── geos.json        ← база даних усіх GEO
├── netlify.toml     ← конфіг Netlify
└── README.md
```

---

## Як це працює

```
geos.json  ←──── ти редагуєш через admin.html
    ↓
GitHub repo  ←── пушиш зміни
    ↓
Netlify  ←────── авто-деплой за ~30 сек
    ↓
yoursite.com  ←── сайт оновлений
```

---

## Деплой на Netlify (перший раз)

### 1. Створи GitHub репо
```bash
git init
git add .
git commit -m "init geoinfo"
git remote add origin https://github.com/YOUR_USER/geoinfo.git
git push -u origin main
```

### 2. Підключи до Netlify
1. Іди на [netlify.com](https://netlify.com) → "Add new site"
2. "Import an existing project" → GitHub
3. Вибери репо `geoinfo`
4. Build command: (залиш пустим)
5. Publish directory: `.`
6. Deploy!

### 3. Налаштуй домен
- Безкоштовний: `yourname.netlify.app`
- Власний: Site settings → Domain management → Add domain

---

## Як додати нове GEO

### Варіант A — через admin.html (рекомендую)
1. Відкрий `yoursite.com/admin.html`
2. Введи пароль: `geoinfo2025` *(змін його в коді!)*
3. Натисни "Add new GEO" → заповни форму
4. Збережи → перейди в "Export JSON"
5. Натисни "Download geos.json"
6. Заміни файл в GitHub → Netlify деплоїть автоматично

### Варіант B — прямо в GitHub
1. Відкрий `geos.json` на github.com
2. Натисни "Edit" (олівець)
3. Додай новий об'єкт в масив
4. "Commit changes" → деплой автоматично

### Варіант C — локально
```bash
# Відредагуй geos.json
git add geos.json
git commit -m "add new geo: PL"
git push
# Netlify деплоїть автоматично
```

---

## Зміна пароля адмінки

В файлі `admin.html` знайди рядок:
```javascript
const ADMIN_PASSWORD = 'geoinfo2025';
```
Замін на свій пароль.

---

## Структура одного GEO в geos.json

```json
{
  "id": "gb",                          // унікальний ID (lowercase)
  "name": "United Kingdom",            // повна назва
  "code": "GB",                        // ISO код
  "flag": "🇬🇧",                       // emoji прапор
  "tier": 1,                           // 1, 2 або 3
  "region": "Europe",
  "language": "English",
  "capital": "London",
  "currency": "British Pound",
  "currencyCode": "GBP",
  "currencySymbol": "£",
  "population": "67M",
  "avgSalary": "$35,000",
  "midCost": "$1,500",
  "internetPenetration": "95%",
  "smartphoneUsage": "88%",
  "avgCpm": "$4.50",
  "fbCpm": "$4.50",
  "googleCpm": "$7.10",
  "tiktokCpm": "$2.80",
  "banks": ["HSBC", "Barclays", "Lloyds"],
  "operators": ["EE", "Vodafone", "O2"],
  "globalPayments": ["Visa", "Mastercard", "PayPal"],
  "localPayments": ["Open Banking", "Revolut"],
  "verticals": ["Gambling", "Nutra", "Finance"],
  "restrictions": [
    { "name": "Gambling Ads", "status": "limited" },
    { "name": "Crypto Ads", "status": "allowed" }
  ],
  "trafficSources": ["Facebook Ads", "Google Ads"],
  "adNetworks": ["Taboola", "PropellerAds"]
}
```

---

## Важливо про localStorage

Адмінка зберігає зміни в `localStorage` браузера.
Це тимчасово — для постійного збереження **обов'язково** роби Export → commit на GitHub.
