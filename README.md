# 🔒 PrivateGPT 📑

> Документация по установке и использованию: https://docs.privategpt.dev/
>
> Присоединяйтесь к сообществу: [Twitter](https://twitter.com/ZylonPrivateGPT) и [Discord](https://discord.gg/bK6mRVpErU)

![Gradio UI](/fern/docs/assets/ui.png?raw=true)

PrivateGPT — это готовый к использованию проект ИИ, который позволяет вам задавать вопросы о ваших документах, используя мощь
Больших языковых моделей (LLM), даже в сценариях без подключения к Интернету. 100% конфиденциальность, никакие данные не покидают вашу
среду выполнения в любой момент.

Проект предоставляет API, предлагающий все примитивы, необходимые для создания частных, контекстно-зависимых приложений ИИ.
Он следует и расширяет [стандарт API OpenAI](https://openai.com/blog/openai-api),
и поддерживает как обычные, так и потоковые ответы.

API делится на два логических блока:

**API высокого уровня**, который абстрагирует всю сложность реализации конвейера RAG (Retrieval Augmented Generation):
- Прием документов: внутреннее управление анализом документов,
разделением, извлечением метаданных, генерацией и хранением встраивания.

- Чат и дополнения с использованием контекста из вставленных документов:
абстрагирование извлечения контекста, проектирования подсказок и генерации ответов.

**API низкого уровня**, который позволяет продвинутым пользователям реализовывать собственные сложные конвейеры:
- Генерация встраиваний: на основе фрагмента текста.
- Контекстное извлечение фрагментов: по запросу возвращает наиболее релевантные фрагменты текста из вставленных документов.

В дополнение к этому, рабочий [Gradio UI](https://www.gradio.app/)
клиент предоставляется для тестирования API вместе с набором полезных инструментов, таких как скрипт массовой загрузки модели, скрипт приема, отслеживание папок документов и т. д.

> 💡 Если вы ищете **готовое к использованию на предприятии, полностью частное рабочее пространство ИИ**
> посетите [сайт Zylon](https://zylon.ai) или [запросите демонстрацию](https://cal.com/zylon/demo?source=pgpt-readme).
> Созданный командой PrivateGPT, Zylon является лучшим в своем классе совместным
> рабочим пространством ИИ, которое можно легко развернуть локально (в центре обработки данных, на физическом сервере...) или в вашем частном облаке (AWS, GCP, Azure...).

## 🎞️ Обзор
ОТКАЗ ОТ ОТВЕТСТВЕННОСТИ: Этот README обновляется не так часто, как [документация](https://docs.privategpt.dev/).
Пожалуйста, ознакомьтесь с ним для получения последних обновлений!

### Мотивация PrivateGPT
Генеративный ИИ — это переломный момент в нашем обществе, но его внедрение в компаниях всех размеров и в чувствительных к данным

доменах, таких как здравоохранение или юриспруденция, ограничено четкой проблемой: **конфиденциальность**.

Невозможность гарантировать, что ваши данные полностью находятся под вашим контролем при использовании сторонних инструментов ИИ
— это риск, на который эти отрасли не могут пойти.

### Первичная версия
Первая версия PrivateGPT была запущена в мае 2023 года как новый подход к решению проблем конфиденциальности

путем использования LLM полностью в автономном режиме.

Эта версия, которая быстро стала проектом для конфиденциальных настроек и послужила основой для тысяч локально ориентированных проектов генеративного ИИ, стала основой того, чем PrivateGPT становится в настоящее время;

таким образом, более простая и более образовательная реализация для понимания основных концепций, необходимых
для создания полностью локального - и, следовательно, приватного - инструмента, похожего на chatGPT.

Если вы хотите продолжить экспериментировать с ним, мы сохранили его в
[первичной ветке](https://github.com/zylon-ai/private-gpt/tree/primordial) проекта.

> Настоятельно рекомендуется сделать чистый клон и установить эту новую версию
PrivateGPT, если вы перешли с предыдущей, первичной версии.

### Настоящее и будущее PrivateGPT
PrivateGPT сейчас развивается в сторону того, чтобы стать шлюзом для генеративных моделей и примитивов ИИ, включая
дополнения, прием документов, конвейеры RAG и другие низкоуровневые строительные блоки.
Мы хотим упростить для любого разработчика создание приложений и приложений ИИ, а также предоставить
подходящую обширную архитектуру для сообщества, чтобы оно могло продолжать вносить свой вклад.

Следите за нашими [релизами](https://github.com/zylon-ai/private-gpt/releases), чтобы ознакомиться со всеми новыми функциями и изменениями.

## 📄 Документация
Полную документацию по установке, зависимостям, настройке, запуску сервера, параметрам развертывания,
приему локальных документов, сведениям об API и функциям пользовательского интерфейса можно найти здесь: https://docs.privategpt.dev/

## 🧩 Архитектура
Концептуально PrivateGPT — это API, который оборачивает конвейер RAG и раскрывает его
примитивы.
* API создан с использованием [FastAPI](https://fastapi.tiangolo.com/) и следует
[схеме API OpenAI](https://platform.openai.com/docs/api-reference).
* Конвейер RAG основан на [LlamaIndex](https://www.llamaindex.ai/).

Конструкция PrivateGPT позволяет легко расширять и адаптировать как API, так и
реализацию RAG. Некоторые ключевые архитектурные решения:
* Внедрение зависимостей, разделяющее различные компоненты и слои.
* Использование абстракций LlamaIndex, таких как `LLM`, `BaseEmbedding` или `VectorStore`,
позволяющее немедленно изменять фактические реализации этих абстракций.
* Простота, добавление как можно меньшего количества слоев и новых абстракций
* Готов к использованию, предоставляя полную реализацию API и RAG
конвейера.

Основные строительные блоки:
* API определены в `private_gpt:server:<api>`. Каждый пакет содержит
`<api>_router.py` (слой FastAPI) и `<api>_service.py` (реализация
сервиса). Каждый *Сервис* использует базовые абстракции LlamaIndex вместо

конкретных реализаций,
отделяя фактическую реализацию от ее использования.
* Компоненты помещены в
`private_gpt:components:<component>`. Каждый *Компонент* отвечает за предоставление
фактических реализаций базовых абстракций, используемых в Сервисах, например
`LLMComponent` отвечает за предоставление фактической реализации `LLM`
(например, `LlamaCPP` или `OpenAI`).

## 💡 Внесение вклада
Внесение вклада приветствуется! Чтобы обеспечить качество кода, мы включили несколько проверок формата и
опечатки, просто запустите `make check` перед фиксацией, чтобы убедиться, что ваш код в порядке.
Не забудьте протестировать свой код! Вы найдете папку тестов с помощниками, и вы можете запустить
тесты с помощью команды `make test`.

Не знаете, что предложить? Вот публичная
[доска проекта](https://github.com/users/imartinez/projects/3) с несколькими идеями.

Перейдите на канал Discord
#contributors и попросите разрешения на запись в этот проект GitHub.

## 💬 Сообщество
Присоединяйтесь к обсуждению PrivateGPT на нашем:
- [Twitter (он же X)](https://twitter.com/PrivateGPT_AI)
- [Discord](https://discord.gg/bK6mRVpErU)

## 📖 Цитирование
Если вы используете PrivateGPT в статье, проверьте [файл цитирования](CITATION.cff) для правильного цитирования.
Вы также можете использовать кнопку «Ссылаться на этот репозиторий» в этом репозитории, чтобы получить цитирование в разных форматах.

Вот несколько примеров:

#### BibTeX
```bibtex
@software{Zylon_PrivateGPT_2023,
author = {Zylon by PrivateGPT},
license = {Apache-2.0},
month = may,
title = {{PrivateGPT}},
url = {https://github.com/zylon-ai/private-gpt},
year = {2023}
}
```

#### APA
```
Zylon by PrivateGPT (2023). PrivateGPT [Компьютерное программное обеспечение]. https://github.com/zylon-ai/private-gpt
```

## 🤗 Партнеры и сторонники
PrivateGPT активно поддерживается следующими командами:
* [Qdrant](https://qdrant.tech/), предоставляющими базу данных векторов по умолчанию
* [Fern](https://buildwithfern.com/), предоставляющими документацию и SDK
* [LlamaIndex](https://www.llamaindex.ai/), предоставляющими базовую структуру RAG и абстракции

Этот проект был сильно поддержан и поддержан другими замечательными проектами, такими как
[LangChain](https://github.com/hwchase17/langchain),
[GPT4All](https://github.com/nomic-ai/gpt4all),
[LlamaCpp](https://github.com/ggerganov/llama.cpp),
[Chroma](https://www.trychroma.com/)
и [SentenceTransformers](https://www.sbert.net/).


# Инстолляция с выбранными опциями

Пример командной строки для установки `PrivatGPT` с выбранными опциями:


```
poetry install --extras "ui llms-ollama embeddings-ollama vector-stores-qdrant"

```

```
poetry install --extras "ui llms-ollama nomic-embed-text vector-stores-qdrant"
```

```
poetry install --extras "ui llms-llama-cpp embeddings-huggingface vector-stores-qdrant"

```

**LLM**

 * `llms-ollama` - Adds support for Ollama LLM, requires Ollama running locally
 * `llms-llama-cpp` - Adds support for local LLM using LlamaCPP

**Embeddings**

 * `embeddings-ollama` - Adds support for Ollama Embeddings, requires Ollama running locally
 * `embeddings-huggingface` - Adds support for local Embeddings using HuggingFace 

**Vector Stores**

 * `vector-stores-qdrant` - Adds support for Qdrant vector store
 * `vector-stores-milvus`- Adds support for Milvus vector store
 * `vector-stores-chroma`- Adds support for Chroma DB vector store
 * `vector-stores-postgres`- Adds support for Postgres vector store
 * `vector-stores-clickhouse`- Adds support for Clickhouse vector store

 **UI**

  * `ui` - Adds support for UI using Gradio

  > Для тестирования API предоставляется рабочий клиент Gradio UI вместе с набором полезных инструментов, таких как скрипт массовой загрузки модели, скрипт приема, просмотр папок с документами и т.д. Пожалуйста, обратитесь к странице с альтернативами пользовательского интерфейса для получения дополнительных [альтернатив пользовательского интерфейса](https://docs.privategpt.dev/manual/user-interface/alternatives).

# Установка `Ollama`

Сайт `Ollama` по [ссылке](https://ollama.com/)

Загрузка моделей:
* [llama3.1](https://ollama.com/library/llama3.1) - _Llama 3.1 is a new state-of-the-art model from Meta available in 8B, 70B and 405B parameter sizes._
    * запуск с этой моделью - `ollama run llama3.1`
* [phi3](https://ollama.com/library/phi3) - _Phi-3 is a family of lightweight 3B (Mini) and 14B (Medium) state-of-the-art open models by Microsoft._
    * запуск - `ollama run phi3`
* [mistral](https://ollama.com/library/mistral) - _The 7B model released by Mistral AI, updated to version 0.3._
    * запуск - `ollama run mistral`
* [gemma2](https://ollama.com/library/gemma2) - _Google Gemma 2 is a high-performing and efficient model by now available in three sizes: 2B, 9B, and 27B._
    * запуск `ollama run gemma2:2b`, `ollama run gemma2` (9B parametres), `ollama run gemma2:27b`

