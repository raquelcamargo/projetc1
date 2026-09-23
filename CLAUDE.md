# Instruções de projeto

## Renomear sessão ao encerrar

Quando a usuária sinalizar que a conversa/sessão chegou ao fim (ex: "obrigada,
vamos parar por aqui", "por hoje é só", "podemos encerrar") — não em respostas
intermediárias, só quando o encerramento for explícito — chame a tool
`set_session_title` (Claude Code Remote) para renomear a sessão atual,
prefixando o título existente com o emoji 🔒 (se ainda não tiver o prefixo).

Exemplo: título "Ajuste no CSS do header" vira "🔒 Ajuste no CSS do header".

Não repetir o prefixo se a sessão já tiver sido marcada assim.

## Nunca enviar nada sem ordem explícita

Nunca enviar e-mail, mensagem, comentário ou qualquer conteúdo em nome da
usuária (Gmail, Hostinger, GitHub, etc.) sem que ela escreva explicitamente
"envia", "pode enviar" ou equivalente inequívoco, referindo-se àquele texto
específico.

- "sim", "ok", "talvez", "acho que...", sugestões de ajuste no texto ou
  respostas a uma pergunta sobre o conteúdo NÃO são autorização de envio.
- Na dúvida, sempre criar ou atualizar um rascunho, mostrar o texto final e
  perguntar: "Posso enviar?". Só enviar após a confirmação.
- Autorização vale para um envio só; não se estende a mensagens seguintes.
