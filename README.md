# ContextIn

Memory and persistent context layer for AI coding agents via MCP (Model Context Protocol)

## Architecture
- Backend: TypeScript + Hono / Express (Cloudflare Workers / D1 or local SQLite)
- Transport: SSE (Server-Sent Events) and HTTP streaming
- Security: Application-level AES-256 encryption and ephemeral MCP session tokens

## Core MCP Tools
1. save_context: stores encrypted decision logs and context keyed by session and agent ID
2. query_memory: semantic and tag-based context retrieval before agent execution
3. list_sessions: returns active conversation threads permitted for the current session token
4. revoke_context: invalidates or purges ephemeral context upon task completion

## Database Schema (SQLite / D1)
Table context_entries:
- id (UUID, Primary Key)
- session_id (TEXT, Indexed)
- agent_id (TEXT)
- encrypted_payload (TEXT/BLOB, AES-256)
- tags (JSON)
- created_at (INTEGER)
- expires_at (INTEGER)
