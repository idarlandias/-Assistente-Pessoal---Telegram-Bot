# J.A.R.V.I.S. — Assistente Pessoal via Telegram

Um assistente pessoal completo integrado ao Telegram, com IA (Google Gemini), Google Workspace, automacoes inteligentes e arquitetura modular em producao na nuvem.

---

## Sumario

- [Visao Geral](#visao-geral)
- [Tecnologias](#tecnologias)
- [Arquitetura v3](#arquitetura-v3)
- [Funcionalidades](#funcionalidades)
- [Comandos](#comandos)
- [Automacoes](#automacoes)
- [Infraestrutura](#infraestrutura)
- [Configuracao](#configuracao)
- [Autor](#autor)

---

## Visao Geral

O J.A.R.V.I.S. transforma o Telegram em uma central de produtividade pessoal completa, combinando:

- **Inteligencia Artificial** para conversacao natural, transcricao de voz, leitura de imagens e PDFs
- **Google Workspace** integrado (Calendar, Tasks, Classroom, Sheets, Drive)
- **Controle Financeiro** com categorizacao automatica por IA
- **Modulos de Estudo** com coach, repeticao espacada, cronometro e diario de erros
- **Saude e Bem-estar** com personal trainer, coach de corrida e habitos com streaks
- **Privacidade** com camada de anonimizacao antes de enviar dados para a IA
- **Infraestrutura profissional** com Docker, GCP e backup automatico diario

---

## Tecnologias

| Tecnologia | Uso |
|---|---|
| Python 3.11 | Linguagem principal |
| aiogram 3.x | Interface assincrona com Telegram |
| Google Gemini 2.5 Flash | IA multimodal (texto, audio, imagem, PDF) |
| Google Calendar API | Agenda e eventos |
| Google Tasks API | Tarefas |
| Google Classroom API | Atividades e notas academicas |
| Google Sheets API | Controle financeiro |
| Google Drive API | Backup de arquivos |
| SQLite | Banco de dados local persistente |
| APScheduler | Agendamento assincrono de tarefas |
| edge-tts | Sintese de voz (Text-to-Speech) |
| Open-Meteo API | Previsao do tempo |
| Docker + Docker Compose | Containerizacao e deploy |
| Google Cloud Platform | Hospedagem em nuvem (Always Free) |

---

## Arquitetura v3

O projeto evoluiu de um arquivo monolitico (1200+ linhas) para uma arquitetura modular em camadas:

```
jarvis/
├── run_jarvis_v3.py               # Entry point
├── scheduler_v3.py                # Scheduler assincrono (APScheduler)
├── scheduler_tasks.py             # Tarefas agendadas
│
├── core/                          # Camada central
│   ├── orchestrator.py            # Orquestrador principal
│   ├── config.py                  # Configuracoes centralizadas e tipadas
│   ├── contracts.py               # Protocolos e interfaces
│   └── container.py               # Injecao de dependencias
│
├── handlers/                      # Camada de entrada
│   └── telegram_handler_v3.py
│
├── services/                      # Integracoes externas
│   ├── ai_service.py              # Google Gemini
│   ├── calendar_service.py        # Google Calendar
│   ├── finance_service.py         # Google Sheets (financeiro)
│   ├── task_service.py            # Google Tasks
│   ├── classroom_service.py       # Google Classroom
│   ├── voice_service.py           # TTS assincrono
│   ├── habit_service.py           # Habitos e streaks
│   ├── study_coach_service.py     # Coach de estudos com IA
│   ├── spaced_repetition_service.py  # Repeticao espacada
│   ├── personal_trainer_service.py   # Personal trainer
│   ├── running_coach_service.py      # Coach de corrida
│   ├── notebook_service.py           # Caderno digital
│   ├── exam_service.py               # Modulo de provas
│   ├── error_diary_service.py        # Diario de erros
│   ├── pomodoro_service.py           # Timer Pomodoro
│   ├── study_timer_service.py        # Cronometro de estudo
│   ├── routine_service.py            # Rotinas personalizadas
│   ├── dashboard_service.py          # Dashboard geral
│   └── local_agenda_service.py       # Agenda local offline
│
├── security/                      # Camada de privacidade
│   ├── privacy_layer.py           # Anonimizacao antes da IA
│   ├── data_classifier.py         # Classificacao de dados sensiveis
│   └── anonymizer.py              # Motor de anonimizacao
│
├── data/
│   └── db.py                      # Camada de acesso ao SQLite
│
├── local_data/                    # Dados persistentes (volume Docker)
│   ├── jarvis.db                  # Banco SQLite principal
│   ├── ai_memory.json             # Memoria de longo prazo da IA
│   └── dados_dashboard.json       # Cache do dashboard
│
├── Dockerfile
└── docker-compose.yml
```

### Fluxo de uma mensagem

```
Usuario (Telegram)
    |
    v
TelegramHandler (aiogram)
    |
    v
Orchestrator
    |-- Comando direto (/agenda) --> Service especifico
    |
    +-- Texto natural -----------> AIService
                                      |
                                      v
                                 PrivacyLayer
                                 (anonimiza dados sensiveis)
                                      |
                                      v
                                 Google Gemini
                                      |
                                      v
                                 Resposta (texto ou audio TTS)
```

---

## Funcionalidades

### Entrada de Dados

| Tipo | Suporte |
|---|---|
| Texto | Comandos e conversacao natural |
| Voz | Transcricao automatica via Gemini |
| Foto | Leitura de recibos com OCR por IA |
| Documento/PDF | Backup no Drive + resumo por IA |

### Google Agenda

- Visualizar compromissos do dia
- Criar eventos por texto ou voz
- Alertas automaticos 30, 15 e 10 minutos antes do evento

### Google Tasks

- Listar e criar tarefas por texto ou voz

### Google Classroom

- Visualizar atividades pendentes
- Alerta automatico ao lancar nota
- Notificacao ao entregar atividade
- Aviso ao devolver atividade corrigida

### Controle Financeiro

| Recurso | Descricao |
|---|---|
| Registro de gastos | Texto, voz ou foto de recibo |
| Categorizacao automatica | IA classifica o tipo de gasto |
| Meta mensal | Defina limite e acompanhe em tempo real |
| Barra de progresso | Visual percentual do mes |
| Fechamento diario | Resumo automatico as 23:59 |
| Relatorio semanal | Todo domingo as 20h |

### Modulo de Estudos

| Recurso | Descricao |
|---|---|
| Study Coach | Planejamento e orientacao de estudos com IA |
| Repeticao Espacada | Algoritmo para revisao otimizada de conteudo |
| Cronometro de Estudo | Registro de tempo por disciplina |
| Diario de Erros | Registro e analise de erros em provas |
| Modulo de Provas | Simulados e acompanhamento de desempenho |
| Quiz | Perguntas e respostas interativas |
| Caderno Digital | Anotacoes organizadas por topico |
| Pomodoro | Timer com alertas de pausa |

### Saude e Bem-estar

| Recurso | Descricao |
|---|---|
| Personal Trainer | Treinos personalizados com IA |
| Running Coach | Planejamento e acompanhamento de corridas |
| Habitos com Streaks | Criacao, acompanhamento e sequencias diarias |
| Hidratacao | Lembrete de agua a cada 2h (8h as 22h) |

### Privacidade e Seguranca

- **Privacy Layer**: dados sensiveis (consultas medicas, psicologos, CPF) sao anonimizados antes de qualquer envio para a IA
- **Classificador de dados**: identifica automaticamente informacoes que nao devem sair do dispositivo
- **Logs sanitizados**: informacoes pessoais mascaradas nos registros do sistema

### Memoria de Longo Prazo

- Salve informacoes importantes via comando
- A IA recupera o contexto automaticamente nas conversas
- Historico com data e hora

### Google Drive

- Backup automatico de documentos enviados
- Organizacao em pasta dedicada

---

## Comandos

### Menu e Navegacao

| Comando | Descricao |
|---|---|
| `/start` | Inicia o bot |
| `/menu` | Menu interativo com botoes |
| `/ajuda` | Lista de comandos |

### Agenda e Tarefas

| Comando | Descricao |
|---|---|
| `Adicionar evento [nome]` | Cria evento no Calendar |
| `Nova tarefa [nome]` | Cria tarefa no Tasks |

### Financeiro

| Comando | Descricao |
|---|---|
| `Gastei [valor] [descricao]` | Registra gasto |
| `/meta [valor]` | Define meta mensal |
| `/meta` | Ver progresso da meta |

### Estudos

| Comando | Descricao |
|---|---|
| `/estudo` | Abre modulo de estudos |
| `/pomodoro [min] [tarefa]` | Inicia timer Pomodoro |
| `/quiz` | Inicia sessao de quiz |
| `/erros` | Abre diario de erros |
| `/caderno` | Abre caderno digital |

### Habitos e Saude

| Comando | Descricao |
|---|---|
| `/habito [nome]` | Cria um habito |
| `/fiz [nome]` | Marca habito como feito hoje |
| `/habitos` | Lista todos com streaks |
| `/treino` | Abre modulo de personal trainer |
| `/corrida` | Abre modulo de running coach |

### Memoria

| Comando | Descricao |
|---|---|
| `/lembrar [texto]` | Salva na memoria da IA |
| `/memoria` | Lista memorias salvas |

### Arquivos

| Comando | Descricao |
|---|---|
| `/resumir` | Resume o ultimo PDF enviado |
| Enviar documento | Salva automaticamente no Google Drive |
| Enviar foto de recibo | IA le e registra o gasto |

---

## Automacoes

### Agendamentos Fixos

| Horario | Acao |
|---|---|
| 08:00 | Bom dia + Agenda do dia + Clima + Tarefas pendentes |
| 8h, 10h, 12h, 14h, 16h, 18h, 20h, 22h | Lembrete de hidratacao |
| 23:59 | Fechamento financeiro do dia |
| Domingo 20:00 | Relatorio semanal de gastos |

### Monitoramentos Continuos

| Intervalo | Acao |
|---|---|
| 1 minuto | Verifica alertas de eventos (30/15/10 min antes) |
| 10 minutos | Verifica novas notas e entregas no Classroom |

---

## Infraestrutura

### Producao — Google Cloud Platform

| Item | Detalhe |
|---|---|
| Provedor | Google Cloud Platform |
| VM | e2-micro (Always Free tier) |
| Regiao | us-east1 — Carolina do Sul |
| SO | Debian 12 (Bookworm) |
| Custo | $0/mes (dentro da cota gratuita) |
| Uptime | 24/7 com restart automatico via Docker |

### Containerizacao

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

O mapeamento de volumes permite **hot-deploy**: atualizar um arquivo e reiniciar o container sem rebuildar a imagem completa.

### Backup Automatico

- Script agendado diariamente via Windows Task Scheduler
- Copia `jarvis.db`, `ai_memory.json` e dados do dashboard para o PC local
- Executa checkpoint SQLite antes de copiar para garantir consistencia do banco
- Retencao de 30 dias de historico local

---

## Configuracao

### Variaveis de Ambiente (.env)

```env
TELEGRAM_API_TOKEN=seu_token_aqui
GEMINI_API_KEY=sua_chave_gemini
TELEGRAM_CHAT_ID=seu_chat_id
```

### Arquivos Necessarios

| Arquivo | Descricao |
|---|---|
| `security/keys/credentials.json` | Credenciais OAuth Google |
| `security/keys/token.json` | Token de autenticacao (gerado automaticamente) |
| `.env` | Variaveis de ambiente |

### Escopos Google OAuth

- `calendar` — Agenda
- `tasks` — Tarefas
- `classroom.courses.readonly` — Cursos
- `classroom.student-submissions.me.readonly` — Atividades
- `spreadsheets` — Planilhas (financeiro)
- `drive.file` — Upload de arquivos

### Deploy

```bash
# Primeiro deploy
docker compose up -d --build

# Hot-deploy (atualizacao de codigo)
scp -i chave.key arquivo.py usuario@vm:/home/usuario/jarvis/services/
ssh -i chave.key usuario@vm "cd jarvis && docker compose restart jarvis_v3"

# Ver logs em tempo real
docker logs jarvis_v3 --tail=50 -f
```

---

## Autor

**Idarlan Magalhaes**

Desenvolvido com foco em produtividade pessoal real — cada funcionalidade nasceu de uma necessidade do dia a dia.

---

_Ultima atualizacao: Marco 2026_
