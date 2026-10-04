# Monero Height Finder / Поиск блока Monero по дате

[English](#english) | [Русский](#russian)

---

<a id="english"></a>
## English

A fast, lightweight, standalone client-side tool to find the nearest Monero (XMR) block height and hash for any date and time using an $O(\log N)$ binary search via the public [xmrchain.net](https://xmrchain.net) API.

### Why is this needed?

When restoring a Monero wallet (such as official Monero GUI/CLI, Feather Wallet, Cake Wallet, or Monerujo) from a mnemonic seed phrase or keys, you are prompted for a **Restore Height** (or restore date).

- If you don't provide a restore height, the wallet may start scanning the entire Monero blockchain starting from the genesis block in April 2014, taking hours or even days.
- By entering the exact block height corresponding to the date your first transaction was received, synchronization begins immediately from that point, saving much time.

### Features

- **Multilingual Interface**: Instant switching between English and Russian (clean typographic `EN` / `RU` toggle).
- **Theme Switcher**: Choose between **Light**, **Dark**, and **System** (matches OS theme automatically). Remembers preference in `localStorage`.
- **Fast Binary Search**: Finds the exact block among 3.8+ million blocks in only ~22 network requests in a few seconds.
- **Quick Date Presets**: One-click selection for *Now*, *24 hours ago*, *7 days ago*, *30 days ago*, *1 year ago*, and *Genesis block (April 18, 2014)*.
- **Detailed Result Card**: Displays block height, block hash, timestamp in your local timezone and UTC, time delta, copy-to-clipboard buttons, and direct link to the block in the blockchain explorer.
- **Live Search Console**: Step-by-step terminal log showing search bounds, timestamps, and minute/hour differences in real-time. Search cancellation supported.
- **100% Client-Side & Zero Dependencies**: Single self-contained HTML file. No NodeJS, no npm packages, no build steps, and no backend server required. Runs directly in any modern browser.
- **Private & Safe**: Never asks for seeds, private keys, or wallet addresses. Only performs public block timestamp lookups over HTTPS.

### Available Versions

- **`monero-height.html`** (Main): Full-featured modern interface with dynamic language toggle (EN/RU), theme switcher (Light/Dark/System), date presets, search progress bar, formatted result card, and one-click copy buttons.
- **`minimalistic/monero-height-en.html`**: Lightweight, minimalistic English version without extra design elements (simple input, search button, and terminal output).
- **`minimalistic/monero-height-ru.html`**: Lightweight, minimalistic Russian version without extra design elements.

### How to Run

#### Option 1: Direct File Open (Recommended)
Simply double-click `monero-height.html` (or one of the files in `minimalistic/`) or open it directly in your web browser:
```bash
# On Linux
xdg-open monero-height.html

# On macOS
open monero-height.html

# On Windows
start monero-height.html
```

### How the Algorithm Works

1. **Get Current Network Height**: Requests `https://xmrchain.net/api/networkinfo` to get current top block height $H$.
2. **Binary Search**:
   - Sets boundaries: $low = 1$, $high = H$.
   - Evaluates midpoint $mid = \lfloor(low + high) / 2\rfloor$ via `https://xmrchain.net/api/block/<mid>`.
   - Compares the block's UNIX timestamp with your target timestamp.
   - Adjusts the search interval to the left or right half until the closest block is found.
3. **Complexity**: $O(\log_2 H) \approx 22$ network requests for over 3.7+ million blocks.

### API Used

- Network Information: `GET https://xmrchain.net/api/networkinfo`
- Block Information: `GET https://xmrchain.net/api/block/<height>`

### License

This project is licensed under the [MIT License](LICENSE.MIT).

---

<a id="russian"></a>
## Russian

Быстрый, легковесный и полностью автономный клиентский инструмент для поиска ближайшей высоты и хэша блока Monero (XMR) по заданной дате и времени с помощью алгоритма бинарного поиска $O(\log N)$ через публичный API [xmrchain.net](https://xmrchain.net).

### Зачем это нужно?

При создании или восстановлении кошелька Monero (официальный Monero GUI/CLI, Feather Wallet, Cake Wallet, Monerujo) из мнемонической seed-фразы или приватных ключей требуется указать **Restore Height** (высоту восстановления) или дату создания кошелька.

- Если не указать высоту восстановления, кошелёк начнёт сканировать абсолютно все блоки Monero с момента запуска сети в апреле 2014 года, что может занять многие часы или даже дни.
- Указав точную высоту блока на дату первого получения средств, вы начинаете сканирование ровно с нужного места — синхронизация занимает намного меньше времени.

### Возможности

- **Мультиязычный интерфейс**: Мгновенное переключение между русским и английским языком (аккуратный типографический переключатель `RU` / `EN`).
- **Переключатель темы оформления**: Поддержка **Светлой**, **Тёмной** и **Системной** темы (автоматически подстраивается под настройки операционной системы). Выбор сохраняется в `localStorage`.
- **Быстрый бинарный поиск**: Находит нужный блок среди более чем 3.8 млн блоков сети всего за ~22 запроса к блокчейну за пару секунд.
- **Быстрые пресеты даты**: Установка даты в один клик: *Сейчас*, *24 часа назад*, *7 дней назад*, *30 дней назад*, *1 год назад*, а также дата *генезис-блока (18 апреля 2014 г.)*.
- **Информативная карточка результата**: Отображает высоту блока, хэш, дату/время в вашем локальном часовом поясе и в UTC, погрешность во времени, кнопки быстрого копирования и прямую ссылку на блок в обозревателе.
- **Интерактивный журнал поиска**: Консоль в стиле терминала с отображением каждого шага поиска, границ интервала и разницы во времени в минутах и часах. Поддерживается остановка поиска в любой момент.
- **100% клиентское приложение без зависимостей**: Один автономный HTML-файл. Не требует Node.js, сборщиков, пакетов npm или собственного бэкенда. Работает в любом современном браузере.
- **Безопасность и приватность**: Не запрашивает seed-фразы, ключи или адреса кошельков. Выполняются только запросы публичных заголовков блоков по защищённому протоколу HTTPS.

### Доступные версии

- **`monero-height.html`** (Основная): Полнофункциональный современный интерфейс с переключателем языков (RU/EN), переключателем тем (Светлая/Тёмная/Системная), быстрыми пресетами дат, индикатором прогресса поиска, карточкой результата и кнопками копирования.
- **`minimalistic/monero-height-ru.html`**: Минималистичная легковесная версия на русском языке без лишних элементов оформления (только выбор даты, кнопка запуска и терминальный вывод).
- **`minimalistic/monero-height-en.html`**: Аналогичная минималистичная легковесная версия, полностью локализованная на английский язык.

### Как запустить

#### Способ 1: Прямое открытие файла (рекомендуется)
Дважды кликните по файлу `monero-height.html` (или одному из файлов в папке `minimalistic/`) или откройте его в любом браузере:
```bash
# В Linux
xdg-open monero-height.html

# В macOS
open monero-height.html

# В Windows
start monero-height.html
```


### Как работает алгоритм

1. **Получение высоты сети**: Запрос к `https://xmrchain.net/api/networkinfo` возвращает текущую высоту верхнего блока сети $H$.
2. **Бинарный поиск**:
   - Задаётся диапазон: $low = 1$, $high = H$.
   - Вычисляется середина $mid = \lfloor(low + high) / 2\rfloor$ и запрашивается блок `https://xmrchain.net/api/block/<mid>`.
   - Сравнивается UNIX-время блока с целевым временем пользователя.
   - Диапазон поиска делится пополам (влево или вправо) в зависимости от того, находится ли блок в прошлом или будущем относительно искомой даты.
3. **Сложность**: $O(\log_2 H) \approx 22$ запроса для блокчейна размером более 3.7 млн блоков.

### Используемый API

- Состояние сети: `GET https://xmrchain.net/api/networkinfo`
- Информация о блоке: `GET https://xmrchain.net/api/block/<height>`

### Лицензия

Проект распространяется под лицензией [MIT](LICENSE.MIT).
