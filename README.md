# 🤖 Assistente Pessoal - Telegram Bot (J.A.R.V.I.S. V3)

Um assistente pessoal completo integrado ao Telegram, com IA (Google Gemini Function Calling), Google Workspace, automações inteligentes e deploy 24/7 na nuvem Oracle Cloud.

---

## 📋 Sumário

- [Visão Geral](#-visão-geral)
- [Tecnologias](#-tecnologias)
- [Funcionalidades](#-funcionalidades)
- [Comandos Disponíveis](#-comandos-disponíveis)
- [Automações](#-automações)
- [Configuração](#-configuração)
- [Arquitetura](#-arquitetura)

---

## 🎯 Visão Geral

Este bot transforma seu Telegram em uma central de produtividade pessoal, combinando:

- 🧠 **Inteligência Artificial** com Google Gemini Function Calling para conversação natural e roteamento de intenções
- 📅 **Google Workspace** (Calendar, Tasks, Classroom, Sheets, Drive)
- 💰 **Controle Financeiro** com categorização automática
- 🎓 **Monitor Acadêmico** com alertas de notas
- ⏱️ **Produtividade** com Pomodoro, hábitos e lembretes
- ☁️ **Deploy 24/7** na Oracle Cloud (Always Free Tier) — sem precisar manter o PC ligado

---

## 🛠️ Tecnologias

| Tecnologia              | Uso                                         |
| ----------------------- | ------------------------------------------- |
| Python 3.11             | Linguagem principal                         |
| aiogram 3.x             | Interface assíncrona com Telegram           |
| Google Gemini API       | IA multimodal + Function Calling (NLP)      |
| Google Calendar API     | Agenda e eventos                            |
| Google Tasks API        | Tarefas                                     |
| Google Classroom API    | Atividades e notas                          |
| Google Sheets API       | Controle financeiro                         |
| Google Drive API        | Backup de arquivos                          |
| Open-Meteo API          | Previsão do tempo                           |
| APScheduler             | Agendamento de tarefas assíncrono           |
| Docker / Docker Compose | Containerização e deploy                    |
| Oracle Cloud (ARM VM)   | Hospedagem gratuita 24/7 (Always Free Tier) |

---

## ⚡ Funcionalidades

### 🗣️ Entrada de Dados

| Tipo      | Suporte                             |
| --------- | ----------------------------------- |
| Texto     | ✅ Comandos e conversa natural      |
| Voz       | ✅ Transcrição automática via IA    |
| Foto      | ✅ Leitura de recibos (OCR com IA)  |
| Documento | ✅ Backup no Drive + resumo de PDFs |

### 📅 Google Agenda

- Visualizar compromissos do dia
- Criar novos eventos por texto ou voz
- Alertas automáticos (30, 15 e 10 minutos antes)

### 📝 Google Tasks

- Listar tarefas pendentes
- Criar novas tarefas por texto ou voz

### 🎓 Google Classroom

- Visualizar atividades pendentes
- **Monitor de Notas**: Alerta quando professor lança nota
- **Monitor de Entregas**: Parabéns automático ao entregar atividade
- **Monitor de Devoluções**: Aviso quando atividade é devolvida

### 💰 Controle Financeiro

| Recurso                  | Descrição                           |
| ------------------------ | ----------------------------------- |
| Registro de Gastos       | Texto, voz ou foto de recibo        |
| Categorização Automática | IA classifica automaticamente       |
| Meta Mensal              | Defina limite e acompanhe progresso |
| Fechamento Diário        | Resumo às 23:59                     |
| Relatório Semanal        | Todo domingo às 20h                 |
| Barra de Progresso       | Visual do quanto gastou da meta     |

### 🧠 Memória de Longo Prazo

- Guarde informações importantes
- A IA lembra quando você perguntar
- Histórico com data e hora

### 📈 Hábitos com Streaks

- Crie hábitos para acompanhar
- Marque como feito diariamente
- Visualize streaks com 🔥

### ⏱️ Pomodoro

- Timer customizável
- Alerta ao finalizar
- Sugestão de pausa

### 💧 Bem-estar

- Lembrete de beber água a cada 2 horas (8h às 22h)

### 📂 Google Drive

- Backup automático de documentos enviados
- Organização em pasta dedicada

### 📖 Resumo de PDFs

- Envie um PDF e peça resumo
- IA lê e organiza em tópicos principais

---

## 🎮 Comandos Disponíveis

### Menu e Navegação

| Comando  | Descrição                  |
| -------- | -------------------------- |
| `/start` | Inicia o bot e mostra menu |
| `/menu`  | Mostra menu com botões     |
| `/ajuda` | Lista de comandos          |

### Agenda e Tarefas

| Comando                   | Descrição       |
| ------------------------- | --------------- |
| `Nova tarefa [nome]`      | Cria uma tarefa |
| `Adicionar evento [nome]` | Cria um evento  |

### Financeiro

| Comando                      | Descrição             |
| ---------------------------- | --------------------- |
| `Gastei [valor] [descrição]` | Registra gasto        |
| `/gastei 50 Pizza`           | Formato alternativo   |
| `/meta 1500`                 | Define meta mensal    |
| `/meta`                      | Ver progresso da meta |

### Memória

| Comando            | Descrição             |
| ------------------ | --------------------- |
| `/lembrar [texto]` | Salva na memória      |
| `/memoria`         | Lista memórias salvas |

### Hábitos

| Comando          | Descrição              |
| ---------------- | ---------------------- |
| `/habito [nome]` | Cria um hábito         |
| `/fiz [nome]`    | Marca como feito hoje  |
| `/habitos`       | Lista todos os hábitos |

### Produtividade

| Comando                    | Descrição          |
| -------------------------- | ------------------ |
| `/pomodoro [min] [tarefa]` | Inicia timer       |
| `/pausa`                   | Pausa de 5 minutos |

### Arquivos

| Comando                 | Descrição                   |
| ----------------------- | --------------------------- |
| `/resumir`              | Resume o último PDF enviado |
| _Enviar documento_      | Salva no Google Drive       |
| _Enviar foto de recibo_ | Lê e registra gasto         |

### Conversa Natural

Qualquer mensagem que não seja comando é processada pela IA com contexto completo (agenda, tarefas, memórias).

---

## 🔄 Automações

### Agendamentos Fixos

| Horário                               | Ação                                  |
| ------------------------------------- | ------------------------------------- |
| 08:00                                 | ☀️ Bom Dia + Agenda + Clima + Tarefas |
| 8h, 10h, 12h, 14h, 16h, 18h, 20h, 22h | 💧 Lembrete de água                   |
| 23:59                                 | 💰 Fechamento financeiro do dia       |
| Domingo 20:00                         | 📊 Relatório semanal de gastos        |

### Monitoramentos Contínuos

| Intervalo  | Ação                                            |
| ---------- | ----------------------------------------------- |
| 1 minuto   | ⏰ Verifica alertas de eventos (30/15/10 min)   |
| 10 minutos | 🎓 Verifica novas notas e entregas no Classroom |

---

## ⚙️ Configuração

### Variáveis de Ambiente (.env)

```env
TELEGRAM_API_TOKEN=seu_token_aqui
GEMINI_API_KEY=sua_chave_gemini
```

### Arquivos Necessários

| Arquivo            | Descrição                                      |
| ------------------ | ---------------------------------------------- |
| `credentials.json` | Credenciais OAuth Google                       |
| `token.json`       | Token de autenticação (gerado automaticamente) |
| `.env`             | Variáveis de ambiente                          |

### Escopos Google (OAuth)

- `calendar` - Agenda
- `tasks` - Tarefas
- `classroom.courses.readonly` - Cursos
- `classroom.student-submissions.me.readonly` - Atividades
- `spreadsheets` - Planilhas
- `drive.file` - Upload de arquivos

---

## 🏗️ Arquitetura V3

```
whatsapp-calendar-bot/
├── run_jarvis_v3.py         # Entrypoint assíncrono (aiogram)
├── handlers/
│   └── telegram_handler_v3.py # Handler principal (aiogram 3.x)
├── core/
│   ├── orchestrator_v3.py   # Orquestrador com Gemini Function Calling
│   └── tools_definitions.py # Definições de ferramentas para a IA
├── services/
│   ├── ai_service.py        # Google Gemini API
│   ├── finance_service.py   # Controle financeiro (Google Sheets)
│   ├── calendar_service.py  # Google Calendar
│   ├── study_coach.py       # Coach de estudos
│   └── ...                  # Demais serviços especializados
├── data/
│   └── memory_store.py      # Persistência SQLite
├── security/                # Camada de privacidade (dados mascarados)
├── Dockerfile               # Imagem Python 3.11-slim
├── docker-compose.yml       # Orquestração dos contêineres
└── .env                     # Variáveis de ambiente (não versionado)
```

---

## 🚀 Executando

### Produção (Docker - Oracle Cloud)

```bash
# Na VM Oracle (Ubuntu ARM - Always Free Tier)
docker compose up -d --build

# Ver logs ao vivo
docker logs jarvis_v3 -f

# Reiniciar
docker compose restart
```

### Desenvolvimento Local

```bash
cd whatsapp-calendar-bot
python run_jarvis_v3.py
```

---

## 📊 Modelo de IA

| Aspecto    | Detalhe                                |
| ---------- | -------------------------------------- |
| Modelo     | Google Gemini (Function Calling)       |
| Tipo       | Multimodal (texto, áudio, imagem, PDF) |
| Velocidade | < 1 segundo por resposta               |
| Custo      | Cota gratuita generosa                 |

---

## 📱 Uso Típico

1. **Manhã**: Receba o resumo do dia às 8h
2. **Durante o dia**: Registre gastos por voz, gerencie tarefas
3. **Ao receber notas**: Notificação automática
4. **A cada 2h**: Lembrete de hidratação
5. **À noite**: Fechamento financeiro automático
6. **Domingo**: Relatório semanal de gastos

---

## 🎯 Roadmap Futuro

- [ ] Ativação por voz (wake word)
- [ ] Integração com Spotify
- [ ] Relatórios gráficos (imagens de pizza/barras)
- [ ] Backup automático de conversas
- [ ] Modo offline com sincronização

---

## 👨‍💻 Autor

**Idarlan Magalhaes - Especialista em IA - Certificado pela UFC**

Desenvolvido com ❤️ e muito ☕

---

_Última atualização: Fevereiro 2026 — V3 com aiogram, Gemini Function Calling, Docker e Oracle Cloud_
