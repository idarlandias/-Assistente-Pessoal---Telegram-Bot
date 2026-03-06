# 🤖 J.A.R.V.I.S. — Assistente Pessoal via Telegram

> _"Just A Rather Very Intelligent System"_

Um assistente pessoal completo integrado ao Telegram, com IA (Google Gemini), Google Workspace, automações inteligentes e arquitetura modular em produção na nuvem.

---

## 📋 Sumário

- [Visão Geral](#-visão-geral)
- [Tecnologias](#-tecnologias)
- [Arquitetura v3](#-arquitetura-v3)
- [Funcionalidades](#-funcionalidades)
- [Comandos](#-comandos)
- [Automações](#-automações)
- [Infraestrutura](#-infraestrutura)
- [Configuração](#-configuração)
- [Autor](#-autor)

---

## 🎯 Visão Geral

O J.A.R.V.I.S. transforma o Telegram em uma central de produtividade pessoal completa, combinando:

- 🧠 **Inteligência Artificial** para conversação natural, transcrição de voz, leitura de imagens e PDFs
- 📅 **Google Workspace** integrado (Calendar, Tasks, Classroom, Sheets, Drive)
- 💰 **Controle Financeiro** com categorização automática por IA
- 📚 **Módulos de Estudo** com coach, repetição espaçada, cronômetro e diário de erros
- 💪 **Saúde e Bem-estar** com personal trainer, coach de corrida e hábitos com streaks
- 🔒 **Privacidade** com camada de anonimização antes de enviar dados para a IA
- ☁️ **Infraestrutura profissional** com Docker, GCP e backup automático diário

---

## ⚡ Tecnologias

| Tecnologia | Uso |
|---|---|
| 🐍 Python 3.11 | Linguagem principal |
| ✈️ aiogram 3.x | Interface assíncrona com Telegram |
| 🧠 Google Gemini 2.5 Flash | IA multimodal (texto, áudio, imagem, PDF) |
| 📅 Google Calendar API | Agenda e eventos |
| ✅ Google Tasks API | Tarefas |
| 🎓 Google Classroom API | Atividades e notas acadêmicas |
| 📊 Google Sheets API | Controle financeiro |
| 💾 Google Drive API | Backup de arquivos |
| 🗄️ SQLite | Banco de dados local persistente |
| ⏱️ APScheduler | Agendamento assíncrono de tarefas |
| 🔊 edge-tts | Síntese de voz (Text-to-Speech) |
| 🌦️ Open-Meteo API | Previsão do tempo |
| 🐳 Docker + Docker Compose | Containerização e deploy |
| ☁️ Google Cloud Platform | Hospedagem em nuvem (Always Free) |

---

## 🏗️ Arquitetura v3

O projeto evoluiu de um arquivo monolítico (1200+ linhas) para uma arquitetura modular em camadas:

```
jarvis/
├── run_jarvis_v3.py               # 🚀 Entry point
├── scheduler_v3.py                # ⏰ Scheduler assíncrono (APScheduler)
├── scheduler_tasks.py             # 📋 Tarefas agendadas
│
├── core/                          # 🧩 Camada central
│   ├── orchestrator.py            # 🎯 Orquestrador principal
│   ├── config.py                  # ⚙️ Configurações centralizadas e tipadas
│   ├── contracts.py               # 📜 Protocolos e interfaces
│   └── container.py               # 🔧 Injeção de dependências
│
├── handlers/                      # 📥 Camada de entrada
│   └── telegram_handler_v3.py
│
├── services/                      # 🔌 Integrações externas
│   ├── ai_service.py              # 🧠 Google Gemini
│   ├── calendar_service.py        # 📅 Google Calendar
│   ├── finance_service.py         # 💰 Google Sheets (financeiro)
│   ├── task_service.py            # ✅ Google Tasks
│   ├── classroom_service.py       # 🎓 Google Classroom
│   ├── voice_service.py           # 🔊 TTS assíncrono
│   ├── habit_service.py           # 🔥 Hábitos e streaks
│   ├── study_coach_service.py     # 📚 Coach de estudos com IA
│   ├── spaced_repetition_service.py  # 🔁 Repetição espaçada
│   ├── personal_trainer_service.py   # 💪 Personal trainer
│   ├── running_coach_service.py      # 🏃 Coach de corrida
│   ├── notebook_service.py           # 📓 Caderno digital
│   ├── exam_service.py               # 📝 Módulo de provas
│   ├── error_diary_service.py        # ❌ Diário de erros
│   ├── pomodoro_service.py           # 🍅 Timer Pomodoro
│   ├── study_timer_service.py        # ⏱️ Cronômetro de estudo
│   ├── routine_service.py            # 🗓️ Rotinas personalizadas
│   ├── dashboard_service.py          # 📊 Dashboard geral
│   └── local_agenda_service.py       # 📆 Agenda local offline
│
├── security/                      # 🔒 Camada de privacidade
│   ├── privacy_layer.py           # 🛡️ Anonimização antes da IA
│   ├── data_classifier.py         # 🔍 Classificação de dados sensíveis
│   └── anonymizer.py              # 🎭 Motor de anonimização
│
├── data/
│   └── db.py                      # 🗄️ Camada de acesso ao SQLite
│
├── local_data/                    # 💿 Dados persistentes (volume Docker)
│   ├── jarvis.db                  # Banco SQLite principal
│   ├── ai_memory.json             # Memória de longo prazo da IA
│   └── dados_dashboard.json       # Cache do dashboard
│
├── Dockerfile
└── docker-compose.yml
```

### 🔄 Fluxo de uma mensagem

```
👤 Usuário (Telegram)
        |
        ▼
📥 TelegramHandler (aiogram)
        |
        ▼
🎯 Orchestrator
        |── Comando direto (/agenda) ──► 🔌 Service específico
        |
        └── Texto natural ─────────────► 🧠 AIService
                                                |
                                                ▼
                                         🛡️ PrivacyLayer
                                         (anonimiza dados sensíveis)
                                                |
                                                ▼
                                         🤖 Google Gemini
                                                |
                                                ▼
                                         💬 Resposta (texto ou áudio TTS)
```

---

## ✨ Funcionalidades

### 📥 Entrada de Dados

| Tipo | Suporte |
|---|---|
| 💬 Texto | Comandos e conversação natural |
| 🎙️ Voz | Transcrição automática via Gemini |
| 📷 Foto | Leitura de recibos com OCR por IA |
| 📄 Documento/PDF | Backup no Drive + resumo por IA |

### 📅 Google Agenda

- 🗓️ Visualizar compromissos do dia
- ➕ Criar eventos por texto ou voz
- ⚠️ Alertas automáticos 30, 15 e 10 minutos antes do evento

### ✅ Google Tasks

- 📋 Listar e criar tarefas por texto ou voz

### 🎓 Google Classroom

- 📚 Visualizar atividades pendentes
- 🔔 Alerta automático ao lançar nota
- 📨 Notificação ao entregar atividade
- 📬 Aviso ao devolver atividade corrigida

### 💰 Controle Financeiro

| Recurso | Descrição |
|---|---|
| 💳 Registro de gastos | Texto, voz ou foto de recibo |
| 🤖 Categorização automática | IA classifica o tipo de gasto |
| 🎯 Meta mensal | Defina limite e acompanhe em tempo real |
| 📊 Barra de progresso | Visual percentual do mês |
| 🌙 Fechamento diário | Resumo automático às 23:59 |
| 📈 Relatório semanal | Todo domingo às 20h |

### 📚 Módulo de Estudos

| Recurso | Descrição |
|---|---|
| 🧑‍🏫 Study Coach | Planejamento e orientação de estudos com IA |
| 🔁 Repetição Espaçada | Algoritmo para revisão otimizada de conteúdo |
| ⏱️ Cronômetro de Estudo | Registro de tempo por disciplina |
| ❌ Diário de Erros | Registro e análise de erros em provas |
| 📝 Módulo de Provas | Simulados e acompanhamento de desempenho |
| 🧩 Quiz | Perguntas e respostas interativas |
| 📓 Caderno Digital | Anotações organizadas por tópico |
| 🍅 Pomodoro | Timer com alertas de pausa |

### 💪 Saúde e Bem-estar

| Recurso | Descrição |
|---|---|
| 🏋️ Personal Trainer | Treinos personalizados com IA |
| 🏃 Running Coach | Planejamento e acompanhamento de corridas |
| 🔥 Hábitos com Streaks | Criação, acompanhamento e sequências diárias |
| 💧 Hidratação | Lembrete de água a cada 2h (8h às 22h) |

### 🔒 Privacidade e Segurança

- 🛡️ **Privacy Layer**: dados sensíveis (consultas médicas, psicólogos, CPF) são anonimizados antes de qualquer envio para a IA
- 🔍 **Classificador de dados**: identifica automaticamente informações que não devem sair do dispositivo
- 📋 **Logs sanitizados**: informações pessoais mascaradas nos registros do sistema

### 🧠 Memória de Longo Prazo

- 💾 Salve informações importantes via comando
- 🔄 A IA recupera o contexto automaticamente nas conversas
- 🕐 Histórico com data e hora

### ☁️ Google Drive

- 📤 Backup automático de documentos enviados
- 📁 Organização em pasta dedicada

---

## 🎮 Comandos

### 🗺️ Menu e Navegação

| Comando | Descrição |
|---|---|
| `/start` | 🚀 Inicia o bot |
| `/menu` | 📋 Menu interativo com botões |
| `/ajuda` | ❓ Lista de comandos |

### 📅 Agenda e Tarefas

| Comando | Descrição |
|---|---|
| `Adicionar evento [nome]` | 📅 Cria evento no Calendar |
| `Nova tarefa [nome]` | ✅ Cria tarefa no Tasks |

### 💰 Financeiro

| Comando | Descrição |
|---|---|
| `Gastei [valor] [descrição]` | 💳 Registra gasto |
| `/meta [valor]` | 🎯 Define meta mensal |
| `/meta` | 📊 Ver progresso da meta |

### 📚 Estudos

| Comando | Descrição |
|---|---|
| `/estudo` | 📚 Abre módulo de estudos |
| `/pomodoro [min] [tarefa]` | 🍅 Inicia timer Pomodoro |
| `/quiz` | 🧩 Inicia sessão de quiz |
| `/erros` | ❌ Abre diário de erros |
| `/caderno` | 📓 Abre caderno digital |

### 💪 Hábitos e Saúde

| Comando | Descrição |
|---|---|
| `/habito [nome]` | ➕ Cria um hábito |
| `/fiz [nome]` | ✅ Marca hábito como feito hoje |
| `/habitos` | 🔥 Lista todos com streaks |
| `/treino` | 🏋️ Abre módulo de personal trainer |
| `/corrida` | 🏃 Abre módulo de running coach |

### 🧠 Memória

| Comando | Descrição |
|---|---|
| `/lembrar [texto]` | 💾 Salva na memória da IA |
| `/memoria` | 📋 Lista memórias salvas |

### 📂 Arquivos

| Comando | Descrição |
|---|---|
| `/resumir` | 📄 Resume o último PDF enviado |
| Enviar documento | ☁️ Salva automaticamente no Google Drive |
| Enviar foto de recibo | 🤖 IA lê e registra o gasto |

---

## 🔄 Automações

### ⏰ Agendamentos Fixos

| Horário | Ação |
|---|---|
| ☀️ 08:00 | Bom dia + Agenda do dia + Clima + Tarefas pendentes |
| 💧 8h, 10h, 12h, 14h, 16h, 18h, 20h, 22h | Lembrete de hidratação |
| 🌙 23:59 | Fechamento financeiro do dia |
| 📊 Domingo 20:00 | Relatório semanal de gastos |

### 👁️ Monitoramentos Contínuos

| Intervalo | Ação |
|---|---|
| ⚡ 1 minuto | Verifica alertas de eventos (30/15/10 min antes) |
| 🎓 10 minutos | Verifica novas notas e entregas no Classroom |

---

## ☁️ Infraestrutura

### 🖥️ Produção — Google Cloud Platform

| Item | Detalhe |
|---|---|
| ☁️ Provedor | Google Cloud Platform |
| 💻 VM | e2-micro (Always Free tier) |
| 🌎 Região | us-east1 — Carolina do Sul |
| 🐧 SO | Debian 12 (Bookworm) |
| 💵 Custo | $0/mês (dentro da cota gratuita) |
| ⚡ Uptime | 24/7 com restart automático via Docker |

### 🐳 Containerização

```yaml
# docker-compose.yml (resumido)
services:
  jarvis_v3:
    build: .
    restart: always
    env_file: .env
    volumes:
      - ./local_data:/app/local_data       # dados persistentes
      - ./security/keys:/app/security/keys  # credenciais Google
      - ./services:/app/services            # hot-deploy sem rebuild
      - ./core:/app/core
      - ./handlers:/app/handlers
```

> 🚀 O mapeamento de volumes permite **hot-deploy**: atualizar um arquivo e reiniciar o container sem rebuildar a imagem completa.

### 💾 Backup Automático

- 🗓️ Script agendado diariamente via Windows Task Scheduler
- 📦 Copia `jarvis.db`, `ai_memory.json` e dados do dashboard para o PC local
- ✅ Executa checkpoint SQLite antes de copiar para garantir consistência do banco
- 🗃️ Retenção de 30 dias de histórico local

---

## ⚙️ Configuração

### 🔑 Variáveis de Ambiente (.env)

```env
TELEGRAM_API_TOKEN=seu_token_aqui
GEMINI_API_KEY=sua_chave_gemini
TELEGRAM_CHAT_ID=seu_chat_id
```

### 📁 Arquivos Necessários

| Arquivo | Descrição |
|---|---|
| `security/keys/credentials.json` | 🔐 Credenciais OAuth Google |
| `security/keys/token.json` | 🎫 Token de autenticação (gerado automaticamente) |
| `.env` | ⚙️ Variáveis de ambiente |

### 🔓 Escopos Google OAuth

- `calendar` — 📅 Agenda
- `tasks` — ✅ Tarefas
- `classroom.courses.readonly` — 🎓 Cursos
- `classroom.student-submissions.me.readonly` — 📚 Atividades
- `spreadsheets` — 📊 Planilhas (financeiro)
- `drive.file` — ☁️ Upload de arquivos

### 🚀 Deploy

```bash
# Primeiro deploy
docker compose up -d --build

# Hot-deploy (atualização de código)
scp -i chave.key arquivo.py usuario@vm:/home/usuario/jarvis/services/
ssh -i chave.key usuario@vm "cd jarvis && docker compose restart jarvis_v3"

# Ver logs em tempo real
docker logs jarvis_v3 --tail=50 -f
```

---

## 👨‍💻 Autor

**Idarlan Magalhães**

> Desenvolvido com foco em produtividade pessoal real — cada funcionalidade nasceu de uma necessidade do dia a dia. 🚀

---

_🕐 Última atualização: Março 2026_
