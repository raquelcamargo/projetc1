# Instruções de projeto

## Renomear sessão ao encerrar

Quando a usuária sinalizar que a conversa/sessão chegou ao fim (ex: "obrigada,
vamos parar por aqui", "por hoje é só", "podemos encerrar") — não em respostas
intermediárias, só quando o encerramento for explícito — chame a tool
`set_session_title` (Claude Code Remote) para renomear a sessão atual,
prefixando o título existente com o emoji 🔒 (se ainda não tiver o prefixo).

Exemplo: título "Ajuste no CSS do header" vira "🔒 Ajuste no CSS do header".

Não repetir o prefixo se a sessão já tiver sido marcada assim.
