# 📄 Product Requirements Document (PRD)

**Projeto:** Caronas UTFPR
**Versão:** 1.0 (MVP)
**Autor:** Gabriel Campos Manzoli
**Última atualização:** 23/09/2026

> 🤖 **Este documento é a fonte da verdade sobre o QUE o produto faz.** Regra de
> negócio que não estiver aqui não existe — nem para a equipe, nem para a IA.
> Tecnologia **não** se discute aqui: isso é assunto do `architecture.md`.
>
> ✍️ **Este PRD foi consolidado com o tema, histórias, regras e escopo aprovados
> para o MVP da disciplina.**

---

## 🎯 1. Visão Geral e Objetivo

**O problema:** Dificuldade de mobilidade diária vivida por estudantes, professores e visitantes da UTFPR Campus Guarapuava devido a horários escassos de transporte público e custos elevados de transporte individual.

**A solução:** Plataforma web de intermediação e organização de caronas universitárias cotidianas, conectando motoristas com vagas a passageiros com itinerários compatíveis.

**Como saberemos que deu certo:** Facilitar o encontro de trajetos comuns, reduzir o tempo de espera no deslocamento diário e garantir transparência no status das solicitações e na identificação de perfil dos participantes.

---

## 📖 2. Glossário Ubíquo

> Os termos do negócio, como o cliente fala. É daqui que o `architecture.md`
> deriva os nomes das entidades.

| Termo | Significa | Não confundir com |
| :---- | :-------- | :---------------- |
| Motorista | Usuário autenticado que cadastra e oferece um trajeto em seu próprio veículo com vagas disponíveis. | Passageiro ou Motorista profissional/uber. |
| Passageiro | Usuário autenticado que pesquisa caronas disponíveis e envia solicitação para ocupar uma vaga. | Motorista ou pessoa sem reserva. |
| Carona (Viagem) | Oferta cadastrada contendo origem, destino, data, horário de saída e quantidade de vagas ofertadas. | Carona recorrente ou linha de ônibus fixa. |
| Solicitação | Pedido formal enviado por um passageiro para reservar uma vaga em uma carona ativa. | Reserva automática ou confirmação imediata. |
| Vaga | Assento individual disponível em um veículo ofertado para um trajeto. | Reserva confirmada. |
| Visitante | Usuário cadastrado no sistema sem vínculo ativo direto com a universidade, identificado por badge obrigatória. | Usuário anônimo ou aluno/professor. |
| Ponto de Encontro | Local específico combinado para embarque ou desembarque do passageiro ao longo do trajeto. | Rota inteira com paradas complexas. |
| Status da Solicitação | Estado atual da vaga pedida pelo passageiro: Pendente, Aceita ou Recusada. | Status da carona. |

---

## 👤 3. Atores e Permissões

> ⚠️ A coluna **"Não pode"** vira Guard na rota e regra de acesso no BaaS
> (ex.: RLS no Supabase).

| Ator | Quem é | Pode | Não pode |
| :--- | :----- | :--- | :------- |
| Aluno | Usuário autenticado pertencente ao corpo discente da UTFPR. | Cadastrar ofertas de carona, buscar caronas por trajeto, solicitar vaga, gerenciar solicitações em suas ofertas, cancelar solicitações próprias e conversar no chat da viagem. | Exigir pagamento, alterar dados de caronas de terceiros, reservar mais de uma vaga para si na mesma carona, aceitar solicitações na carona de outro motorista. |
| Professor | Usuário autenticado pertencente ao corpo docente/servidores da UTFPR. | Cadastrar ofertas de carona, buscar caronas por trajeto, solicitar vaga, gerenciar solicitações em suas ofertas, cancelar solicitações próprias e conversar no chat da viagem. | Exigir pagamento, alterar dados de caronas de terceiros, omitir seu perfil acadêmico, reservar mais de uma vaga para si na mesma carona. |
| Visitante | Usuário cadastrado sem vínculo ativo direto (aluno/servidor) com a universidade. | Cadastrar ofertas de carona, solicitar vagas e participar de chats de carona, sempre identificado com a badge obrigatória de Visitante. | Ocultar ou remover a tag/badge visual de "Visitante" em suas ofertas, solicitações ou perfil; alterar dados de outros usuários. |
| Sistema | Infraestrutura automatizada da aplicação. | Atualizar o saldo de vagas disponíveis em tempo real, alternar status de solicitações/caronas, exibir badges de perfil e garantir as regras de acesso ao chat. | Tomar decisões arbitrárias de aceite/recusa de vagas sem a ação do motorista, permitir solicitações em caronas sem vagas livres ou com horários passados. |

> Aluno e Professor compartilham as mesmas permissões funcionais na plataforma. Visitante possui a obrigatoriedade da badge visual em todas as suas interações relevantes ao sistema.

---

## 📝 4. Escopo Funcional (User Stories)

> Uma story por vez, no formato do modelo abaixo. Cada uma carrega dois eixos:
> **Prioridade (MoSCoW)** — `Must Have` é o escopo comprometido do projeto
> (o escopo mínimo da ficha é `Must Have` por definição); `Should`/`Could`
> entram se sobrar tempo, mas ficam documentadas — nada se perde; o
> `Won't Have` vira item da seção *Fora de Escopo* — e **Tamanho (esforço)** —
> `S` cabe numa sessão, `M` vira algumas tarefas no plano, `L` pede divisão.
> O status percorre `Draft` → `Ready` → `Live`: toda story nasce `Draft` —
> **só você promove a `Ready`** — e vira `Live` quando o PR dela é mesclado
> (o auditor final cobra essa atualização; o commit é seu).

### US01 — Publicar oferta de carona · `Must Have` · `M` · Status: `Draft`

**Como** motorista autenticado (Aluno, Professor ou Visitante), **eu quero** publicar uma oferta de carona com origem, destino, data, horário e quantidade de vagas, **para que** eu possa compartilhar meu trajeto com outros usuários da comunidade.

**Critérios de aceite:**

- [ ] **Dado** que preenchi todos os campos obrigatórios (origem, destino, data/horário futuro e pelo menos 1 vaga), **quando** confirmo a publicação, **então** a carona é criada com status "Ativa" e exibida na listagem de buscas.
- [ ] **Dado** que tentei cadastrar uma carona com data/horário no passado ou com 0 vagas, **quando** tento submeter o formulário, **então** o sistema impede o envio e exibe a mensagem de erro "Preencha uma data futura e pelo menos 1 vaga disponível".
- [ ] **Dado** que sou um usuário cadastrado como Visitante, **quando** publico uma oferta de carona, **então** a oferta é criada exibindo obrigatoriamente o badge visual "Visitante" no card da carona.

**Regras relacionadas:** RN01, RN05, RN06

### US02 — Pesquisar caronas por trajeto · `Must Have` · `S` · Status: `Draft`

**Como** passageiro (Aluno, Professor ou Visitante), **eu quero** pesquisar caronas informando origem e destino, **para que** eu possa encontrar viagens compatíveis com o meu itinerário.

**Critérios de aceite:**

- [ ] **Dado** que existem caronas ativas e futuras para os termos de busca informados, **quando** executo a pesquisa, **então** vejo a lista de caronas encontradas ordenadas por horário de saída mais próximo.
- [ ] **Dado** que não existem caronas cadastradas que correspondam ao trajeto pesquisado, **quando** executo a pesquisa, **então** vejo a tela de resultado vazio com a mensagem "Nenhuma carona encontrada para este trajeto".
- [ ] **Dado** que realizo uma busca e há caronas de usuários Visitantes nos resultados, **quando** visualizo os cards das caronas, **então** os cards desses usuários exibem de forma visível o badge "Visitante".

**Regras relacionadas:** RN02, RN05, RN06

### US03 — Solicitar vaga em uma carona · `Must Have` · `M` · Status: `Draft`

**Como** passageiro autenticado (Aluno, Professor ou Visitante), **eu quero** solicitar uma vaga em uma carona com lugares disponíveis, **para que** o motorista possa avaliar meu pedido e me incluir na viagem.

**Critérios de aceite:**

- [ ] **Dado** que a carona possui vagas livres e eu ainda não possuo solicitação para ela, **quando** confirmo a solicitação de vaga, **então** o pedido é criado com status "Pendente" e o motorista é notificado.
- [ ] **Dado** que as vagas da carona se esgotaram enquanto eu analisava os detalhes, **quando** tento confirmar a solicitação, **então** o sistema impede a ação, exibe a mensagem "Esta carona não possui mais vagas disponíveis" e nada é registrado.
- [ ] **Dado** que já possuo uma solicitação ativa (Pendente ou Aceita) para a mesma carona, **quando** visualizo os detalhes da viagem, **então** o botão de solicitação aparece desabilitado informando "Você já solicitou vaga nesta viagem".

**Regras relacionadas:** RN01, RN03, RN04

### US04 — Avaliar solicitação de vaga · `Must Have` · `M` · Status: `Draft`

**Como** motorista autenticado (Aluno, Professor ou Visitante), **eu quero** aceitar ou recusar as solicitações recebidas para minha carona, **para que** eu possa controlar quem participa da viagem e manter a vaga disponível para os usuários corretos.

**Critérios de aceite:**

- [ ] **Dado** que recebi uma solicitação de vaga em minha carona e ainda existem vagas disponíveis, **quando** eu aprovo a solicitação, **então** o status da solicitação muda para "Aceita" e a vaga correspondente é reservada para esse passageiro.
- [ ] **Dado** que recebi uma solicitação em minha carona e decido rejeitá-la, **quando** confirmo a recusa, **então** o status da solicitação muda para "Recusada" e a vaga continua disponível para outros passageiros.
- [ ] **Dado** que a carona já chegou ao limite de vagas, **quando** tento aceitar uma nova solicitação, **então** o sistema bloqueia a ação e exibe a mensagem "Não há vagas disponíveis para esta carona".

**Regras relacionadas:** RN01, RN03, RN04

### US05 — Trocar mensagens no chat da carona · `Should Have` · `M` · Status: `Draft`

**Como** participante de uma carona (motorista ou passageiro com solicitação aceita), **eu quero** trocar mensagens em tempo real no chat da viagem, **para que** possamos alinhar os pontos de encontro e detalhes do embarque.

**Critérios de aceite:**

- [ ] **Dado** que minha solicitação para a carona foi Aceita pelo motorista (ou sou o motorista da viagem), **quando** envio uma mensagem no chat, **então** a mensagem é publicada em tempo real e fica visível para todos os membros aceitos na carona.
- [ ] **Dado** que minha solicitação está Pendente ou foi Recusada, **quando** tento acessar a carona, **então** o chat permanece bloqueado/inacessível com a indicação "O chat só fica disponível após a confirmação da vaga".
- [ ] **Dado** que envio uma mensagem vazia ou composta apenas por espaços, **quando** tento clicar em enviar, **então** o sistema desabilita o envio e nada é registrado no histórico.

**Regras relacionadas:** RN03, RNF02

---

## 🛡️ 5. Regras de Negócio (Constraints)

| ID | Regra |
| :-- | :---- |
| RN01 | Uma oferta de carona só pode ser publicada com data/horário no futuro e com quantidade de vagas maior ou igual a 1. |
| RN02 | A busca por trajetos deve exibir apenas caronas com status "Ativa", data/horário futuro e com vagas ainda disponíveis. |
| RN03 | A confirmação do passageiro na viagem depende exclusivamente da aprovação manual do motorista. O aceite incrementa os passageiros confirmados e reduz as vagas livres em 1. |
| RN04 | Um mesmo usuário não pode possuir mais de uma solicitação ativa (Pendente ou Aceita) para a mesma carona. |
| RN05 | O chat em tempo real da carona é restrito ao motorista e aos passageiros que tiveram suas solicitações explicitamente aceitas. |
| RN06 | Usuários cadastrados como Visitantes devem exibir obrigatoriamente a badge visual "Visitante" em seu perfil, nos cards de carona ofertada e nas solicitações de vaga. |

---

## 🚫 6. Fora de Escopo (Non-goals)

> O que o produto deliberadamente **não** faz neste semestre — o `Won't Have`
> do MoSCoW, com o motivo de cada corte.

- Não haverá cobrança, divisão financeira automática de custos de combustível ou processamento de pagamentos dentro do sistema.
- Não haverá navegação GPS, rastreamento em mapa interativo ou geolocalização em tempo real.
- Não haverá sistema de avaliação, notas ou comentários (reviews) de motoristas e passageiros.
- Não haverá suporte a caronas recorrentes automáticas (ex.: agendamento semanal) ou viagens com paradas intermediárias complexas.
- Não haverá integração automática para publicação ou compartilhamento em redes sociais externas.

---

## ⚙️ 7. Requisitos Não Funcionais (Qualidade)

> Só os que você consegue justificar na defesa.

- RNF01 (Mobile First & Usabilidade): A interface da aplicação deve ser projetada prioritariamente para dispositivos móveis, garantindo layout responsivo e navegação simplificada.
- RNF02 (Mensageria em Tempo Real): O chat entre os participantes aceitos da carona deve atualizar e entregar mensagens de forma instantânea sem necessidade de recarregar a página.
- RNF03 (Contraste e Clareza Visual): Os status das solicitações (Pendente, Aceita, Recusada) e as badges de identificação (Aluno, Professor, Visitante) devem utilizar cores diferenciadas e rótulos claros de alto contraste.

---

## 🛠️ 8. Histórico

| Data | Versão | O que mudou |
| :--- | :----- | :---------- |
| 2026-09-23 | 1.0.0 | Versão inicial do PRD preenchida com tema, glossário, atores, stories, regras de negócio, fora de escopo e RNFs. |
