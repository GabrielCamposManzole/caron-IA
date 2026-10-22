---
issue: 1
status: aprovado   # rascunho | aprovada
---

# US01 — Publicar oferta de carona

## O problema

Motoristas da comunidade UTFPR (alunos, professores e visitantes) não têm
uma forma centralizada de anunciar que têm vagas disponíveis em seu trajeto
diário. Sem isso, caronas potenciais são perdidas por falta de visibilidade,
e quem poderia compartilhar o trajeto fica sem saber que há interesse.

## A história

**Como** motorista autenticado (Aluno, Professor ou Visitante), **eu quero**
publicar uma oferta de carona com origem, destino, data, horário e quantidade
de vagas, **para que** eu possa compartilhar meu trajeto com outros usuários
da comunidade.

## Critérios de aceite

- [ ] **CA1 — Dado** que preenchi todos os campos obrigatórios (origem e
  destino via seleção no mapa, data/horário futuro, pelo menos 1 vaga e ponto
  de encontro), **quando** confirmo a publicação, **então** a carona é criada
  com status "Ativa" e aparece imediatamente na listagem de buscas.

- [ ] **CA2 — Dado** que tentei cadastrar uma carona com data/horário no
  passado ou com 0 vagas, **quando** tento submeter o formulário, **então** o
  sistema impede o envio e exibe a mensagem de erro
  "Preencha uma data futura e pelo menos 1 vaga disponível".

- [ ] **CA3 — Dado** que sou um usuário cadastrado como Visitante, **quando**
  publico uma oferta de carona, **então** a oferta é criada exibindo
  obrigatoriamente o badge visual "Visitante" no card da carona — aplicado
  automaticamente pelo sistema com base no tipo de perfil, sem intervenção do
  usuário.

- [ ] **CA4 — Dado** que deixei o formulário preenchido pela metade e fechei
  a aba (ou naveguei para outra página), **quando** retorno ao formulário de
  criação, **então** nenhum rascunho é restaurado — o formulário começa limpo.

- [ ] **CA5 — Dado** que minha sessão expirou enquanto eu preenchia o
  formulário e cliquei em "Publicar", **quando** o sistema tenta salvar a
  oferta, **então** a ação é bloqueada e uma mensagem de erro é exibida
  ("Sessão expirada. Faça login novamente.") — sem criar registros parciais
  no banco.

## Fora de escopo

- Edição ou exclusão de uma oferta já publicada (outra Issue).
- Caronas recorrentes ou agendamento semanal (PRD §6).
- Navegação GPS, rastreamento em tempo real ou geolocalização ao vivo
  (PRD §6) — o mapa desta história é **apenas um seletor estático de ponto**
  (ex.: clique no mapa para marcar o local), não um mapa interativo de rota.
- Avaliação de motoristas/passageiros (PRD §6).
- Divisão de custos ou pagamentos (PRD §6).
- Notificação ao passageiro após publicação da oferta.

## Abandono no meio

O motorista pode iniciar o preenchimento e desistir em qualquer momento. Casos
mapeados:

- **Fechar a aba / navegar para outra página:** formulário descartado, nenhum
  registro criado (CA4).
- **Sessão expirar antes de salvar:** o clique em "Publicar" dispara a chamada
  ao BaaS; se o token de sessão estiver vencido, o BaaS rejeita a operação e o
  front exibe mensagem de erro (CA5). Nenhum dado parcial é persistido.
- **Conexão cair durante o envio:** o front aguarda o retorno da chamada;
  timeout ou falha de rede devem resultar em mensagem de erro genérica
  ("Não foi possível publicar a carona. Tente novamente."). **Esta mensagem
  de timeout cobre CA5 no cenário de rede — o critério CA5 vale tanto para
  sessão expirada quanto para falha de rede.**

## Assume que

| Premissa | Issue que fecha |
| --- | --- |
| O usuário está autenticado antes de acessar o formulário. A tela de login e o fluxo de autenticação (Supabase Auth) já existem e são responsabilidade do setup inicial — esta história não implementa login. | Setup (pre-existing) |
| O perfil do usuário já possui o campo `role` (`aluno`, `professor`, `visitante`) populado no Supabase. O badge de Visitante é lido desse campo. | Setup (pre-existing) |
| O componente de mapa para seleção de ponto (origem, destino e ponto de encontro) está disponível na camada de front-end. Se ainda não existir, é pré-condição técnica desta história. | — |

## Depende de

Nenhuma Issue de feature. Depende apenas do setup inicial (autenticação e
perfil de usuário configurados no Supabase).

## Dúvidas em aberto

| # | Dúvida | Quem responde |
| --- | --- | --- |
