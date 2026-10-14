# 🎨 Tokens de Design

**Projeto:** Caronas UTFPR
**Versão:** 1.0.0
**Última atualização:** 13/10/2026

> 🤖 **Este documento existe para a IA parar de inventar um botão diferente a cada
> tela.** Não é um design system completo — é o mínimo que dá à prototipagem assistida
> algo a que obedecer.
>
> ✍️ Os valores abaixo foram acordados com o aluno e passam a ser a base visual do MVP.

---

## Paleta

Nome semântico, nunca `azul-2` — a cor muda, o papel dela não.

| Token | Valor | Onde se usa |
| --- | --- | --- |
| `primaria` | `#2563EB` | ação principal, CTA principal, links ativos |
| `secundaria` | `#0F766E` | ações complementares e destaques de apoio |
| `destaque` | `#F59E0B` | avisos, etiquetas e elementos de atenção |
| `fundo` | `#F8FAFC` | fundo geral da aplicação |
| `superficie` | `#FFFFFF` | cards, formulários, barras e painéis |
| `texto` | `#0F172A` | textos principais, títulos e labels |
| `texto-suave` | `#64748B` | suporte, legendas e textos secundários |
| `perigo` | `#DC2626` | erro, exclusão e bloqueios de ação |
| `sucesso` | `#16A34A` | confirmação de ações e estados positivos |
| `desabilitado` | `#CBD5E1` | botões inativos e campos indisponíveis |
| `azul-escuro` | `#1D4ED8` | hover e estados de interação da cor primária |

## Escala de espaçamento

Uma progressão só, usada em tudo.

| Token | Valor |
| --- | --- |
| `xs` | `4px` |
| `sm` | `8px` |
| `md` | `12px` |
| `lg` | `16px` |
| `xl` | `20px` |
| `2xl` | `24px` |
| `3xl` | `32px` |
| `4xl` | `40px` |
| `5xl` | `48px` |

## Tipografia

| Token | Família · tamanho · peso | Papel |
| --- | --- | --- |
| `display` | `Inter · 32px · 700` | títulos principais |
| `h1` | `Inter · 24px · 700` | seções e páginas |
| `h2` | `Inter · 20px · 600` | subtítulos e cards |
| `body` | `Inter · 16px · 400` | texto geral |
| `body-strong` | `Inter · 16px · 600` | textos de destaque |
| `label` | `Inter · 12px · 600` | labels, status e microcopy |
| `caption` | `Inter · 14px · 400` | legendas e apoio |

## Estados de botão

| Estado | Aparência |
| --- | --- |
| `normal` | fundo primário azul, texto branco, borda sem destaque |
| `hover` | `azul-escuro` com leve escurecimento |
| `foco` | contorno visível de foco acessível, contraste alto |
| `desabilitado` | fundo `desabilitado`, texto suave e cursor não interativo |
| `carregando` | fundo primário com spinner ou indicador de progresso |

## Breakpoints (Mobile-First)

O design nasce para a menor tela e cresce. Toda tela do protótipo tem versão mobile antes da versão desktop.

| Token | Largura mínima | Vale para |
| --- | --- | --- |
| `sm` | `0px` | mobile compacto |
| `md` | `640px` | tablets e telas médias |
| `lg` | `1024px` | desktop e notebooks |
| `xl` | `1280px` | desktop amplo |

Regra de layout: a base é mobile-first — uma coluna, navegação compacta e controle de densidade; em telas maiores, os cards e blocos de conteúdo podem expandir para duas colunas e layout mais amplo.

## Identidade PWA

Os valores abaixo alimentam o `manifest.webmanifest` no `/utf-setup`.

| Campo | Valor |
| --- | --- |
| Nome completo | `Caronas UTFPR` |
| Nome curto (`short_name`) | `Caronas` |
| Cor de tema (`theme_color`) | `#2563EB` |
| Cor de fundo (`background_color`) | `#F8FAFC` |
| Ícone | `icon-192.png` e `icon-512.png` |
| Modo de exibição (`display`) | `standalone` |
| Comportamento visual offline | mostrar splash com logo e mensagem curta de “Sem rede no momento” |

## Protótipo

**Link:** https://www.figma.com/design/lKeGyx9s4LH1bQ7KTdt6dN/Untitled?node-id=1-1128&t=nXCuX4tWgNwH5yPn-0
**Telas:** home/busca, detalhe da carona, oferta de viagem, solicitação de vaga e estado vazio de busca

> Observação: a jornada principal foi definida como busca por trajeto → visualização da carona → solicitação de vaga → confirmação/mensagem do motorista. O ponto de desistência principal fica na busca sem resultado, com suporte visual e CTA para ajustar o filtro ou publicar uma carona.
