## Important Tools / Frameworks

| Tool | Purpose |
|------|---------|
| DSPy | Программная оптимизация промптов, автоматический few-shot selection |
| LangChain | Prompt chaining, agent loops, memory management |
| LangSmith | Tracing, debugging, evaluation промптов в production |
| RAGAS | Evaluation framework для RAG pipeline |
| G-Eval | LLM-based evaluation с chain-of-thought scoring |
| Guidance (Microsoft) | Structured generation, constrained output |
| LMQL | Query language для LLM — контроль структуры output |
| NeMo Guardrails (NVIDIA) | Programmable guardrails поверх LLM |

## Examples

**Пример 1 — Customer support bot:**
- System prompt: role = support agent, tone = friendly, language = user's language
- Few-shot: 3 примера хороших ответов
- ReAct: если нужно проверить статус заказа → tool call к API
- Defensive: "Never share internal pricing", "If unsure, escalate to human"

**Пример 2 — Code review pipeline:**
- Chain: Extract code → Analyze bugs (CoT) → Suggest fixes → Format as PR comment
- Evaluation: LLM-as-judge проверяет что suggestions компилируются
- Optimization: сжать system prompt с 500 до 200 токенов без потери качества

## Why This Matters

Prompt engineering — самый дешёвый способ улучшить LLM систему. Не нужен fine-tuning, не нужен retraining. В production 80% качества определяется промптом, а не выбором модели. Компании нанимают prompt engineers на $150–250k потому что разница между хорошим и плохим промптом = разница между рабочим продуктом и галлюцинирующим мусором.

## Actionable Learning Tasks

1. Реализовать ReAct агента с нуля (без LangChain) — только API calls + цикл
2. Сравнить zero-shot vs 3-shot vs CoT на одной задаче, замерить accuracy и token cost
3. Построить prompt chain из 3 шагов, добавить логирование каждого шага
4. Написать defensive prompt для chatbot и попробовать его сломать (red teaming)
5. Попробовать DSPy — автоматическая оптимизация промпта на датасете

## Glossary

| Term | Definition |
|------|-----------|
| In-context learning | Способность LLM учиться из примеров в промпте без обновления весов |
| Token | Минимальная единица текста для LLM (~4 символа английского текста) |
| Prompt injection | Атака: пользователь вставляет инструкции, переопределяющие system prompt |
| Jailbreak | Обход safety ограничений модели через специальные промпты |
| Backtracking | Возврат к предыдущему шагу рассуждения при обнаружении тупика (в ToT) |
| Guardrails | Программные ограничения на input/output LLM |
| Scratch pad | Использование output модели как рабочей памяти для промежуточных вычислений |
| Latency | Время от запроса до получения полного ответа |

