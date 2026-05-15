# Multi-Bot Identity Architecture

## Overview
This document describes the architecture for supporting multiple independent bot identities in WeChat Enterprise Group, enabling distinct avatars and behaviors for Shuyu & Momo.

## Architecture

### Bot Identity Registry
Each bot maintains its own:
- **Avatar**: Unique visual identity
- **Personality**: Distinct response patterns
- **Context**: Independent conversation memory
- **Capabilities**: Specific skill set

### Identity Isolation
```
┌─────────────────────────────────┐
│       WeChat Enterprise Group    │
│  ┌───────────┐  ┌───────────┐  │
│  │   Shuyu   │  │   Momo    │  │
│  │  (Bot A)  │  │  (Bot B)  │  │
│  └─────┬─────┘  └─────┬─────┘  │
│        │              │         │
│  ┌─────┴──────────────┴─────┐  │
│  │    Identity Router       │  │
│  │  (message dispatch)      │  │
│  └──────────────────────────┘  │
└─────────────────────────────────┘
```

### Implementation Steps
1. Define bot identity schema (name, avatar_url, personality_config)
2. Implement identity router for message dispatch
3. Add per-bot context management
4. Create avatar upload/management API
5. Implement message signing per bot identity

### API Design
```json
POST /api/bot/identity
{
  "name": "Shuyu",
  "avatar_url": "...",
  "personality": "professional, helpful",
  "webhook_endpoint": "..."
}
```

### WeChat Integration
- Use separate webhook endpoints per bot
- Each bot has its own access token
- Message formatting includes bot identity headers
