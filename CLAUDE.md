# Project instructions

## Language for GitHub content

Everything that goes to GitHub must be written in English: commit messages,
PR titles and descriptions, issue and PR comments, code comments, and files
in this repository (including this one). Conversation with the user stays
in Portuguese.

## Rename the session on wrap-up

When the user signals that the conversation/session is over (e.g. "obrigada,
vamos parar por aqui", "por hoje é só", "podemos encerrar"), and only when the
wrap-up is explicit, not in intermediate replies, call the
`set_session_title` tool (Claude Code Remote) to rename the current session,
prefixing the existing title with the 🔒 emoji (if it does not already have
the prefix).

Example: the title "Ajuste no CSS do header" becomes "🔒 Ajuste no CSS do header".

Do not repeat the prefix if the session has already been marked this way.

## Never send anything without an explicit order

Never send an email, message, comment or any content on the user's behalf
(Gmail, Hostinger, GitHub, etc.) unless she explicitly writes "envia",
"pode enviar" or an equally unambiguous equivalent, referring to that
specific text.

- "sim", "ok", "talvez", "acho que...", suggested edits to the text, or
  answers to a question about the content are NOT permission to send.
- When in doubt, always create or update a draft, show the final text and
  ask: "Posso enviar?". Send only after confirmation.
- Permission covers a single send; it does not extend to later messages.
