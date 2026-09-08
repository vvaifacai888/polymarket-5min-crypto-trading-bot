# Polymarket 5-мин Торговый Бот

## Обзор

Это автоматический торговый бот для 5-минутных рынков Polymarket Bitcoin Up or Down. Он работает на NautilusTrader, объединяет несколько сигналов рыночной микроструктуры и фильтрует входы с помощью XGBoost-модели edge относительно цены Polymarket.

---

## Чем торгует бот

Рынки Polymarket **Bitcoin Up or Down** на 5 минут:

- Формат slug: `btc-updown-5m-{unix_start}`
- Длина окна: **300 секунд** (UTC floor: `(ts // 300) * 300`)
- Окно входа по умолчанию: секунды **180–270** каждого рынка (поздний вход)

---

## Возможности

- Мультисигнальный fusion + ML edge gate для **5-мин** рынков BTC Up/Down
- Риск-контроль (лимит размера, TP/SL, фильтр спреда, anti-chase, одна ставка на окно)
- Режимы simulation / live + терминальный UI
- Логи paper-сделок и метрики Grafana

---

## Быстрый старт

**Требуется:** Python 3.14+ · Redis · API-ключи Polymarket (для live)

```bash
git clone https://github.com/vvaifacai888/polymarket-5min-crypto-trading-bot.git
cd polymarket-5min-crypto-trading-bot

python -m venv venv
# Windows: venv\Scripts\activate
# macOS/Linux: source venv/bin/activate

pip install -r requirements.txt
cp .env.example .env   # добавьте ключи
```

```bash
python main.py --test-mode      # быстрый paper-цикл
python main.py --simulation     # 5-мин paper
python supervisor.py --live     # реальные деньги
```

Просмотр paper-сделок:

```bash
python scripts/view_trades.py
```

---

## Конфиг (основное)

| Параметр | По умолчанию | Примечание |
|-----------|---------|--------|
| `MARKET_BUY_USD` | `1.00` | USD на ордер |
| `ENABLE_STOP_LOSS` | `false` | Ранний выход по SL |
| `TAKE_PROFIT_PCT` | `0.40` | Доля take-profit |
| `MIN_ENTRY_PRICE` / `MAX_ENTRY_PRICE` | `0.25` / `0.75` | Диапазон входа |
| `TRADE_WINDOW_SEC_START` / `END` | `180` / `270` | Окно входа внутри 5-мин рынка |
| `ENTRY_COOLDOWN_SEC` | `30` | Мин. пауза между входами |
| `MAX_TRADES_PER_MARKET` | `1` | Одна ставка на 5-мин окно |
| `MIN_ML_EDGE` | `0.10` | Мин. разрыв ML vs рынок |

Полный список: [`.env.example`](.env.example)

---

## Ссылки

| | |
|---|---|
| Начать здесь | [Быстрый старт](#быстрый-старт) |
| Публичная vs Premium | [Таблица](#публичная-vs-premium) |
| Контакт | [Telegram](https://t.me/woaifacai888) · [X](https://x.com/woaifacai888) |
| Фазовые тесты | `python scripts/test_data_sources.py test` → … → `test_execution.py` |

---

## Отказ от ответственности

Торговля сопряжена с **существенным риском потерь**. ПО предназначено для **обучения и исследований**. Прибыль не гарантируется. Прошлые результаты ≠ будущие. Начинайте с симуляции; используйте только капитал, полную потерю которого можете принять.

---

## Лицензия

MIT — см. [`LICENSE`](LICENSE)
