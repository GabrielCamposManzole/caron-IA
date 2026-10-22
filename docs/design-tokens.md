
# Tokens de Design — Caronas UTFPR

**Versão:** 0.1.0 — consolidação da Entrega 1, valores visuais pendentes  
**Última atualização:** 2026-10-22  
**Framework CSS:** pendente de confirmação pela equipe e registro na arquitetura.

Este documento separa decisões comprovadas pelos requisitos das escolhas que ainda precisam ser lidas ou confirmadas no protótipo. Nenhuma cor, fonte ou medida abaixo é atribuída ao protótipo sem acesso visual a ele.

## Identidade e fontes

- **Produto:** Caronas UTFPR, plataforma web para a comunidade da UTFPR Campus Guarapuava.
- **Identidade de marca:** o nome do projeto está confirmado no PRD e no README; logotipo, símbolo e demais elementos de marca ainda não estão documentados.
- **Protótipo Figma:** [abrir protótipo](https://www.figma.com/design/lKeGyx9s4LH1bQ7KTdt6dN/Untitled?node-id=1-1128&t=nXCuX4tWgNwH5yPn-0).
- **Protótipo Stitch:** [abrir projeto](https://stitch.google.com/projects/8491646570534218067?pli=1).
- **Acesso nesta revisão:** o Figma não exibiu o arquivo porque o navegador informou que WebGL não está disponível; o Stitch abriu a aplicação, mas não carregou o projeto devido a um erro RPC. Não foi possível conferir telas nem extrair valores visuais. O diretório `site/` contém o site do método UTF-SDD, não um protótipo do produto, e seus estilos não são fonte para estes tokens.
- **Fonte de verdade visual a confirmar:** definir qual dos dois links representa a versão vigente e aprovada e se o outro deve permanecer como referência.

## Paleta

Os nomes são semânticos e únicos. Os valores marcados como pendentes precisam ser confirmados no protótipo ou pela equipe; usar nomes de papel não significa que a cor esteja definida.

| Token | Valor | Uso / evidência |
| --- | --- | --- |
| `primaria` | Pendente: confirmar valor HEX e papel no protótipo | Ação principal; valor e uso visual final não foram observados. |
| `superficie` | Pendente: confirmar valor HEX | Cards e painéis; uso visual final a confirmar. |
| `fundo` | Pendente: confirmar valor HEX | Fundo geral da aplicação; confirmar se distinto de `superficie`. |
| `texto` | Pendente: confirmar valor HEX | Texto principal. |
| `texto-suave` | Pendente: confirmar valor HEX | Texto auxiliar; confirmar contraste com cada superfície. |
| `borda` | Pendente: confirmar valor HEX | Divisórias e contornos, se usados no protótipo. |
| `perigo` | Pendente: confirmar valor HEX | Erros e ações destrutivas; não atribuir automaticamente uma cor ao protótipo. |
| `sucesso` | Pendente: confirmar valor HEX | Confirmações e estado Aceita. |
| `pendente` | Pendente: confirmar valor HEX | Estado Pendente, visualmente distinto de Aceita e Recusada (PRD, RNF03). |
| `desabilitado` | Pendente: confirmar valor HEX | Controles inativos; o estado não deve depender apenas da cor. |
| `perfil-aluno` | Pendente: confirmar par de cores HEX para fundo e texto | Badge identificável de Aluno (PRD, RNF03). |
| `perfil-professor` | Pendente: confirmar par de cores HEX para fundo e texto | Badge identificável de Professor (PRD, RNF03). |
| `perfil-visitante` | Pendente: confirmar par de cores HEX para fundo e texto | Badge obrigatório de Visitante em perfil, cards de oferta e solicitações (PRD, RN06). |

**Associação semântica a validar:** considerar `pendente` para o estado Pendente, `sucesso` para Aceita e `perigo` para Recusada; confirmar o mapeamento com a equipe e no protótipo. Rótulos textuais devem acompanhar as cores. Os pares de cores das badges de perfil também precisam de rótulos legíveis e contraste suficiente.

## Espaçamento

Manter uma única escala crescente e reutilizar seus passos. Os valores abaixo não foram extraídos do protótipo e precisam ser confirmados antes de serem tratados como medidas aprovadas.

| Token | Valor |
| --- | --- |
| `xs` | Pendente: confirmar medida |
| `sm` | Pendente: confirmar medida |
| `md` | Pendente: confirmar medida |
| `lg` | Pendente: confirmar medida |
| `xl` | Pendente: confirmar medida |

## Tipografia

O PRD não define fontes ou escala tipográfica. Confirmar família, tamanhos e pesos nas telas do protótipo; não reutilizar as fontes do site UTF-SDD como se fossem fontes do produto.

| Token | Família | Tamanho | Peso | Papel |
| --- | --- | --- | --- | --- |
| `corpo` | Pendente | Pendente | Pendente | Texto corrido e controles. |
| `titulo` | Pendente | Pendente | Pendente | Títulos e hierarquia de tela. |
| `rotulo` | Pendente | Pendente | Pendente | Labels, badges e estados. |

Confirmar também fallback tipográfico e se a família de títulos difere da família de corpo.

## Botões

O PRD prevê ações de publicar, pesquisar, solicitar vaga, aceitar e recusar. A aparência de cada variante deve seguir o protótipo; não há estilo visual confirmado nesta revisão.

| Estado | Regra visual a confirmar |
| --- | --- |
| Normal | Confirmar preenchimento, texto, contorno, dimensões e raio no protótipo. |
| Hover | Confirmar feedback visual; manter o texto legível. |
| Foco por teclado | Definir indicador visível e contrastante, sem depender de hover. |
| Desabilitado | Aplicar `desabilitado` e manter o motivo perceptível; formulários inválidos não permitem submit (checklist, ID24). |
| Carregando | Confirmar indicador e texto; o protótipo e o PRD não definem duração nem comportamento de repetição. |

## Layout, responsividade e componentes

- **Mobile-first:** projetar primeiro para celular e expandir para tablet e desktop (PRD, RNF01; checklist, ID2). Os valores exatos das larguras de viewport não aparecem nos documentos nem puderam ser lidos no protótipo.
- **Breakpoints:** confirmar no protótipo os limites em pixels e os nomes usados pelo projeto. Não assumir os breakpoints padrão do Tailwind como decisão da equipe.
- **Regras de layout:** o conteúdo deve adaptar-se às larguras de celular, tablet e desktop. Confirmar no protótipo colunas, largura máxima, gutters, margens, espaçamento entre seções e pontos de mudança do layout.
- **Componentes visuais compartilhados a validar:** botão; campo e mensagem de validação; badge de perfil; badge de status da solicitação; estado vazio e mensagem de feedback. A forma, dimensões e composição visual de cada um estão pendentes de conferência no protótipo.
- **Componentes de domínio:** card de carona, gestão de solicitações e chat pertencem às jornadas descritas no PRD. Sua composição deve seguir as telas do protótipo; este documento não cria novas telas nem define seus fluxos.
- **Contraste e rótulos:** os estados Pendente, Aceita e Recusada e as badges Aluno, Professor e Visitante precisam de cores diferenciadas e rótulos claros de alto contraste (PRD, RNF03). O badge Visitante é obrigatório nas superfícies descritas na RN06.

## Identidade PWA

O checklist exige manifest, ícones, cores, splash, modo standalone e previsão visual offline (ID3). O PRD não define conteúdo offline.

| Campo | Decisão registrada |
| --- | --- |
| Nome do produto | Caronas UTFPR (PRD e README). |
| Nome curto (`short_name`) | Pendente: confirmar nome curto e limite de exibição no ícone. |
| Cor de tema (`theme_color`) | Pendente: escolher valor HEX a partir da paleta aprovada. |
| Cor de fundo (`background_color`) | Pendente: escolher valor HEX a partir da paleta aprovada. |
| Ícones | Pendente: definir símbolo, arquivo e tamanhos; não há ícone local do produto confirmado. |
| Splash screen | Exigida pelo checklist (ID3); arte e cores pendentes. |
| Modo de exibição (`display`) | `standalone`, conforme checklist e documento de arquitetura. |
| Aparência offline | Pendente: definir a mensagem ou estado visual e quais telas exibem esse estado. |
| Operações offline | Não especificadas no PRD. Não presumir leitura em cache, gravação local, fila de ações ou sincronização posterior. |

## Valores a confirmar com a equipe

1. Qual protótipo é a referência vigente e aprovada; verificar se as telas de celular, tablet e desktop estão presentes para as jornadas do PRD.
2. Valores HEX/RGB e papéis da paleta; pares fundo/texto das badges; contraste das combinações para texto e estados.
3. Medidas da escala `xs` a `xl` e tipografia: famílias, tamanhos, pesos e fallbacks.
4. Aparência dos botões em normal, hover, foco, desabilitado e carregando, incluindo dimensões e variantes visuais realmente usadas.
5. Larguras dos breakpoints e regras de colunas, gutters, largura máxima e demais mudanças de layout.
6. Nome curto, cores do manifest, arquivos e tamanhos dos ícones e arte da splash.
7. Estado offline: mensagem exibida e comportamento visual das jornadas de busca, oferta, solicitação e chat quando não há rede. O PRD não define operações offline nem sincronização.

## Histórico

| Data | Alteração |
| --- | --- |
| 2026-10-19 | Consolidação da documentação da Entrega 1, mantendo pendentes os valores visuais não confirmados. |
| 2026-10-22 | Revisão documental dos tokens e registro explícito das decisões visuais pendentes. |