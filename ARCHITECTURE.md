# Arquitetura J.A.R.V.I.S. v2.0

## Diagrama de Componentes

```mermaid
graph TD
    User((Usuário))

    subgraph "Interface Layer"
        Telegram[Telegram Handler]
        Voice[Voice Handler]
    end

    subgraph "Core Layer"
        Orchestrator[Jarvis Orchestrator]
        Config[Config Manager]
        Logger[Structured Logger]
    end

    subgraph "Security Layer"
        Privacy[Privacy Layer]
        Classifier[Data Classifier]
        Anonymizer[Anonymizer]
    end

    subgraph "Service Layer"
        AI[AI Service (Gemini)]
        Calendar[Calendar Service]
        Finance[Finance Service]
        Tasks[Task Service]
        Reminders[Reminder Service]
        TTS[Voice Service (Edge)]
    end

    subgraph "Data Layer"
        Memory[Memory Store]
        Files[Local Files (.json)]
        GoogleAPI[Google Cloud APIs]
    end

    User --> Telegram
    Telegram --> Orchestrator
    Orchestrator --> SecurityLayer

    Orchestrator --> Calendar
    Orchestrator --> Finance
    Orchestrator --> Tasks
    Orchestrator --> Reminders

    Orchestrator --> AI
    AI --> Privacy
    Privacy --> Classifier
    Privacy --> Anonymizer

    AI --> Memory
    Config --> Orchestrator

    Calendar --> GoogleAPI
    Finance --> GoogleAPI
    Tasks --> GoogleAPI
```

## Fluxo de Mensagem

1. **Entrada**: Usuário envia mensagem no Telegram.
2. **Handler**: `TelegramHandler` recebe e encapsula em `UserContext`.
3. **Orquestrador**:
   - Sanitiza logs.
   - Verifica se é comando (`/agenda`) -> Executa Service direto.
   - Se texto natural -> Chama `AIService`.
4. **IA Service**:
   - `PrivacyLayer` anonimiza dados do contexto (agenda, perfil).
   - Monta Prompt enriquecido (Memória + Contexto + System Instructions).
   - Chama Google Gemini.
   - Retorna resposta texto.
5. **Orquestrador**:
   - Se for resposta de voz, chama `VoiceService` para gerar áudio.
   - Devolve `MessageResponse`.
6. **Saída**: `TelegramHandler` envia texto/áudio para usuário.

## Estrutura de Diretórios

- `core/`: Componentes centrais (Orchestrator, Config, Contracts).
- `services/`: Integrações externas (Google, AI, TTS).
- `security/`: Proteção de dados (Privacy Layer).
- `handlers/`: Interfaces de entrada (Telegram).
- `data/`: Persistência local (Memory, Cache).
