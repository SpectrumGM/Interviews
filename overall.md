# AI Engineer Interview — 12 Core Concepts (Master Overview)


## Core Summary

Это мета-обзор — 12 концепций, которые покрывают всё что спрашивают на AI Engineer интервью. Каждая из них раскрыта детально в отдельных файлах этого репозитория. Здесь — общая карта: что это, зачем, когда использовать, и как всё связано между собой.

---

## Key Concepts

### 1. Prompt Engineering

Управление поведением LLM через структуру входного текста — без изменения весов модели. Техники: zero-shot (без примеров), few-shot (1-5 примеров), Chain-of-Thought (пошаговое рассуждение), Tree-of-Thoughts (несколько веток рассуждений), ReAct (рассуждение + действие в цикле).

- Pros: моментальный результат, бесплатно (не нужен compute для обучения)
- Cons: зависит от модели, хрупко — маленькое изменение промпта может сломать результат
- Best for: прототипы, быстрые задачи, когда fine-tuning не нужен

📄 Подробнее: [prompt-engineering.md](prompt-engineering.md)

---

### 2. RAG (Retrieval-Augmented Generation)

LLM перед ответом ищет релевантные документы в базе знаний и использует их как контекст. Pipeline: документы → chunking → embedding → vector DB → поиск → контекст в промпт → ответ.

- Pros: актуальные знания, снижает галлюцинации, не нужно переобучать модель
- Cons: качество retrieval определяет всё — плохой поиск = плохой ответ
- Best for: Q&A по документам, knowledge bases, customer support

📄 Подробнее: [rag.md](rag.md)

---

### 3. Vector Embeddings & Vector DBs

Текст превращается в вектор (массив чисел), кодирующий смысл. Похожие тексты = близкие векторы. Vector DB (Pinecone, Weaviate, Qdrant, Chroma, PGVector) хранит эти векторы и быстро находит ближайшие.

- Pros: семантический поиск — находит по смыслу, а не по ключевым словам
- Cons: compute на индексацию, нужно следить за freshness (устаревшие embeddings)
- Best for: search, RAG, рекомендации

📄 Подробнее: [vector-databases.md](vector-databases.md)

---

### 4. Agentic AI & Tool Calling

Автономные агенты, которые сами планируют, вызывают инструменты (API, поиск, код), наблюдают результат и решают что делать дальше. Цикл: Thought → Action → Observation → Thought.

- Pros: справляется со сложными real-world задачами автоматически
- Cons: может зацикливаться, галлюцинировать действия, дорого
- Best for: автоматизация, DevOps, research, многошаговые задачи

📄 Подробнее: [ai-agents.md](ai-agents.md)

---

### 5. Chain-of-Thought & Advanced Reasoning

Принуждение модели рассуждать пошагово перед ответом. Включает: CoT (одна цепочка рассуждений), Tree-of-Thoughts (несколько параллельных веток), reflection (самокритика), self-correction (исправление своих ошибок).

- Pros: драматически улучшает качество на логических и математических задачах
- Cons: больше токенов = дороже и медленнее
- Best for: математика, planning, многошаговые рассуждения

📄 Подробнее: [prompt-engineering.md](prompt-engineering.md) (секции CoT, ToT)

---

### 6. Memory Persistence & Context Management

Системы памяти для LLM: short-term (история текущего чата), long-term (факты сохранённые в vector DB между сессиями), summarization (сжатие длинной истории).

- Pros: stateful агенты, персональные ассистенты, запоминание предпочтений
- Cons: context window лимиты, drift (память устаревает)
- Best for: длинные сессии, персональные ассистенты, агенты

📄 Подробнее: [ai-agents.md](ai-agents.md) (секция Memory Systems)

---

### 7. Streaming & Async Patterns

Streaming — отправка ответа по мере генерации (token за token). Async — параллельный вызов нескольких tools, background jobs. Критично для UX: пользователь видит прогресс, а не ждёт 30 секунд.

- Pros: отличный UX, высокий throughput
- Cons: сложный state management, error handling
- Best for: chat UI, high-concurrency системы

📄 Подробнее: [ai-agents.md](ai-agents.md) (секция Streaming & Async)

---

### 8. Inference Optimization

Ускорение и удешевление работы модели на inference (когда модель уже обучена и отвечает на запросы):

- **Quantization** — сжатие весов (32-bit → 4-bit), модель занимает меньше памяти и работает быстрее
- **Distillation** — обучение маленькой модели повторять ответы большой
- **Batching** — обработка нескольких запросов одновременно
- **vLLM** — inference сервер с PagedAttention, оптимизирует использование GPU памяти
- **Caching** — KV-cache, prompt caching для повторяющихся запросов

- Pros: 5-10x дешевле и быстрее
- Cons: минимальная потеря качества при агрессивной оптимизации
- Best for: масштабирование, контроль стоимости

---

### 9. Token & Cost Optimization

Контроль расходов на production LLM приложения:

- **Prompt compression** — сжатие промптов без потери качества (меньше токенов = дешевле)
- **Caching** — кэширование повторяющихся запросов и embedding
- **Model routing** — простые запросы → дешёвая модель (Haiku, GPT-4o-mini), сложные → сильная (Opus, GPT-4)
- **FinOps** — мониторинг и бюджетирование расходов на AI

- Pros: драматическое снижение счетов
- Cons: нужен постоянный мониторинг
- Best for: production high-volume приложения

---

### 10. Fine-Tuning (PEFT/LoRA/QLoRA)

Дообучение модели на своих данных для адаптации к конкретному домену. PEFT — обновление малой части параметров (1-5%). LoRA — добавление маленьких обучаемых матриц. QLoRA — LoRA поверх сжатой (4-bit) модели.

- Pros: кастомное качество, модель учит стиль и терминологию домена
- Cons: нужен GPU, качественные данные, тщательная evaluation
- Best for: вертикальные приложения, кастомный тон и стиль

📄 Подробнее: [fine-tuning.md](fine-tuning.md)

---

### 11. LLM Evaluation & Metrics

Как измерять качество LLM систем:

- **RAGAS** — автоматическая eval RAG (faithfulness, relevance, recall)
- **LLM-as-judge** — сильная модель оценивает ответы слабой
- **Hallucination scoring** — процент выдуманной информации в ответах
- **Golden datasets** — эталонные наборы вопрос-ответ для регрессионного тестирования

- Pros: измеримый прогресс, data-driven итерация
- Cons: не полностью автоматизируемо, LLM-judge имеет свои bias
- Best for: итерация, мониторинг, A/B testing

---

### 12. MLOps & Production Deployment

Инфраструктура для надёжной работы AI в production:

- **Serving** — vLLM, TGI, Triton для inference; FastAPI для API слоя
- **Monitoring** — latency, throughput, error rate, token usage, drift detection
- **Drift detection** — отслеживание деградации качества со временем
- **Rollback** — откат к предыдущей версии модели/промпта при проблемах
- **Guardrails** — защитные слои: input validation, output filtering, prompt injection defense

- Pros: надёжный customer-facing AI
- Cons: тяжёлая инфраструктурная работа
- Best for: production системы, enterprise

---

## How Everything Connects

**User Query**

⬇️ **Prompt Engineering** — формулируем запрос

⬇️ **RAG + Vector DB** — находим релевантные документы

⬇️ **Memory** — добавляем контекст из истории

⬇️ **Agent / ReAct** — если нужны действия: plan → tool call → observe

⬇️ **LLM Inference** — генерация ответа (optimized: quantization, batching, caching)

⬇️ **Guardrails** — проверка safety, hallucination, compliance

⬇️ **Streaming** — отправка пользователю в реальном времени

⬇️ **Evaluation** — метрики качества (RAGAS, LLM-judge)

⬇️ **MLOps** — мониторинг, drift detection, rollback

⬇️ **Cost Optimization** — routing, caching, compression

---

## Quick Reference Map

| Задача | Концепция |
|--------|-----------|
| Контролировать LLM без обучения | Prompt Engineering |
| Дать модели актуальные знания | RAG |
| Семантический поиск | Vector Embeddings & DB |
| Автоматизировать задачи | Agentic AI |
| Улучшить рассуждения | CoT / Advanced Reasoning |
| Запоминать между сессиями | Memory Systems |
| Быстрый отклик в UI | Streaming & Async |
| Ускорить inference | Quantization, vLLM, batching |
| Снизить расходы | Token/Cost Optimization |
| Адаптировать под домен | Fine-Tuning (LoRA/QLoRA) |
| Измерить качество | Evaluation & Metrics |
| Надёжный production | MLOps & Deployment |

---

## Actionable Learning Tasks

1. Построить полный pipeline: RAG + vector DB + agent + streaming — end-to-end
2. Сравнить стоимость: один запрос через GPT-4 vs model routing (простое → mini, сложное → GPT-4)
3. Fine-tune маленькую модель (QLoRA), подключить к RAG, сравнить с base model
4. Настроить мониторинг: latency, token usage, hallucination rate на реальном трафике
5. Реализовать guardrails pipeline: input validation → generation → output check → response

---

## Glossary

| Term | Что это |
|------|---------|
| LLM | Large Language Model — большая языковая модель (GPT-4, Claude, Llama) |
| Inference | Процесс когда обученная модель отвечает на запросы (в отличие от training) |
| Token | Минимальная единица текста для LLM (~4 символа английского, ~1-2 символа русского) |
| Context window | Максимальный объём текста, который модель видит одновременно |
| Embedding | Вектор, кодирующий смысл текста |
| RAG | Retrieval-Augmented Generation — поиск документов перед ответом |
| Vector DB | База данных для хранения и поиска по векторам |
| Agent | LLM, которая сама решает что делать и вызывает инструменты в цикле |
| Tool calling | Механизм вызова внешних функций из LLM |
| CoT | Chain-of-Thought — пошаговое рассуждение |
| LoRA/QLoRA | Методы дешёвого fine-tuning через маленькие матрицы-добавки |
| Quantization | Сжатие весов модели для экономии памяти и ускорения |
| Distillation | Обучение маленькой модели имитировать большую |
| vLLM | Высокопроизводительный сервер для inference LLM |
| Guardrails | Защитные слои: валидация, фильтрация, safety checks |
| Drift | Деградация качества модели со временем из-за изменения данных или запросов |
| Hallucination | Когда модель уверенно выдаёт ложную информацию |
| RAGAS | Framework для автоматической оценки RAG систем |
| MLOps | Практики и инструменты для управления ML моделями в production |
| FinOps | Практики контроля и оптимизации расходов на cloud/AI |
| Prompt caching | Кэширование начала промпта для ускорения повторных запросов |
| Model routing | Направление запросов к разным моделям в зависимости от сложности |
