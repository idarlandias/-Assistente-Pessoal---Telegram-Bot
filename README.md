# J.A.R.V.I.S. Core V3 - Assistente Pessoal Inteligente

![Python Version](https://img.shields.io/badge/python-3.11-blue)
![Architecture](https://img.shields.io/badge/Architecture-Asynchronous_Microservices-success)
![LLM](https://img.shields.io/badge/AI-Google_Gemini_Function_Calling-orange)
![Docker](https://img.shields.io/badge/Deploy-Docker_Compose-2496ED)

## 💡 Sobre o Projeto

Este é o repositório do **J.A.R.V.I.S. v3**, um assistente pessoal inteligente projetado para gerenciar rotinas de estudos, finanças e produtividade via Telegram. O projeto evoluiu de um script monolítico para uma **arquitetura de microsserviços assíncrona, escalável e conteinerizada**.

_⚠️ Este é um repositório de portfólio. As chaves de API, banco de dados de uso real e arquivos sensíveis foram propositalmente omitidos (`.gitignore`)._

## 🏗️ Arquitetura do Sistema (V3 Update)

O sistema foi redesenhado focando em **Alta Performance (AsyncIO)** e **Inteligência Centralizada**, dividindo a aplicação em camadas claras:

- **Interface Layer (`handlers/`)**: Recebe e processa os comandos de entrada de forma assíncrona utilizando `aiogram 3.x`.
- **Core Layer (`core/`)**: Orquestrador central impulsionado por **Google Gemini Function Calling**. O bot abandonou Regexes rígidas; agora a IA decide nativamente qual ferramenta usar baseada na intenção do usuário (`tools_definitions.py`).
- **Service Layer (`services/`)**: Módulos especialistas independentes (Finanças, Agenda, Voz, IA, Estudos, Dashboards).
- **Security & Privacy Layer (`security/`)**: Responsável por mascarar dados sensíveis.
- **Data Layer (`data/`, `local_data/`)**: Persistência local com SQLite atrelado a volumes do Docker para segurança de dados entre deploys.

### Engine de Roteamento Assíncrono

O ecossistema não bloqueia mais threads. O `TelegramHandlerV3` despacha eventos via `asyncio`, enquanto agendamentos pró-ativos rodam na engine leve provida pelo `APScheduler`.

## ✨ Principais Funcionalidades

- **Coach de Estudos Interativo**: Painéis dinâmicos que conectam metas cruzadas com horas diárias, sugerindo automaticamente a próxima matéria baseada na curva de esquecimento.
- **Sessões de Notebook (PDFs)**: Roteiros de chat onde o usuário envia PDFs e o bot extrai flashcards, resumos e questões, interagindo através da API do Gemini.
- **Inteligência Artificial por Function Calling**: Requisições de linguagem natural ("Paguei 50 no Ifood") são mapeadas e executadas nativamente pelas ferramentas do bot (Expense Injection).
- **Gestão Financeira Dinâmica**: Integração com Google Sheets utilizando _Cache Layers_ locais para reduzir latência.
- **Notificações Pró-Ativas**: O `SchedulerTasksV3` dispara briefings focais, Lembretes financeiros e relatórios de métricas.

## 🚀 Como a Arquitetura Funciona na Prática

- O Docker inicializa o contêiner `jarvis_v3` baseado num alpine/slim image do Python 3.11.
- O `run_jarvis_v3.py` atua como o entrypoint assíncrono, instanciando os serviços (`FinanceService`, `TaskService`, `StudyCoachService`, etc.).
- Variáveis locais sensíveis residem fora do container e são injetadas no Compose via `volumes` com privilégios restritos.

## 🛠️ Tecnologias Utilizadas

- **Python 3.11+** (`aiogram`, `APScheduler`, `sqlite3`, `asyncio`)
- **Docker / Docker-Compose** (Containerization & Deployment)
- **Google Cloud APIs** (Sheets, Calendar, Classroom, Drive)
- **Google Gemini API** (Function Calling, NLP)

## ✉️ Contato

Projeto desenvolvido para otimização de rotinas pessoais e aprendizado prático avançado em Engenharia de Software e Deployments Cloud-Native.
