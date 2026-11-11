# Mapa de capacidades — loja da Casa Pet

**Estado:** divisão e ordem aprovadas pelo Vinícius em 2026-11-06. Este mapa organiza as próximas especificações; não fecha decisões técnicas pendentes.

## Premissas usadas neste rascunho

1. A primeira versão será usada pela loja e terá uma área pública para clientes e uma área restrita para o proprietário.
2. Haverá uma aplicação Spring Boot, organizada por funcionalidades, servindo as duas áreas do site e acessando um banco PostgreSQL.
3. A interface usará HTML, CSS, Tailwind e JavaScript para as interações e chamadas HTTP. Ela será entregue junto da aplicação Spring Boot na primeira versão.
4. O cliente monta o carrinho antes de entrar na conta; autenticação é obrigatória para registrar o pedido.
5. O envio automático pelo WhatsApp é parte do produto, mas será integrado depois que o fluxo de pedidos funcionar.

As premissas 1, 4 e 5 vêm das decisões de produto. As premissas 2 e 3 registram a arquitetura discutida e ainda podem ser ajustadas antes da implementação.

## Capacidades

| ID estável | O que entrega | Depende de | Evidência de funcionamento |
| --- | --- | --- | --- |
| `catalogo` | Vitrine, categorias, detalhes e preços dos produtos. | — | Um cliente encontra um produto por categoria e vê seus detalhes e preço. |
| `acesso` | Cadastro de cliente, entrada por código enviado ao e-mail e acesso restrito do proprietário. | — | O cliente entra na conta; um visitante não acessa a área do proprietário. |
| `gestao-catalogo` | Cadastro e correção de produtos, categorias e preços, com envio de fotos pelo proprietário no painel. | `catalogo`, `acesso` | Uma alteração autorizada aparece na vitrine; um cliente não consegue fazê-la. |
| `pedidos` | Carrinho, fechamento, histórico, consulta e mudança de estado pelo proprietário. | `catalogo`, `acesso` | Um cliente autenticado registra pedido com itens e total; o proprietário o vê e altera Enviado → Aceito → Pronto. |
| `notificacoes` | Mensagens automáticas da conta de WhatsApp da loja ao cliente quando o pedido é registrado ou muda de estado. | `pedidos` | As mensagens correspondem ao pedido e estado persistidos; falha no envio não apaga o pedido. |

**Ordem sugerida:** `catalogo` → `acesso` → `gestao-catalogo` e `pedidos` → `notificacoes`. `Gestao-catalogo` e `pedidos` podem ser detalhados separadamente depois de suas dependências. O catálogo público pode ser a primeira parte executável do projeto.

As capacidades descrevem comportamentos verificáveis, não cinco aplicações ou cinco serviços. Permanecem **um back-end e duas áreas de interface no mesmo site**. Cada capacidade terá sua especificação detalhada em `.specs/features/<id>/`. A [base de requisitos já levantada](features/loja-petshop/base-requisitos.md) é a fonte dos comportamentos de produto; os [diagramas atuais](features/loja-petshop/casos-de-uso-rascunho.puml) continuam como apoio à discussão.

As categorias iniciais serão agrupadas a partir dos produtos observados no [Instagram da Casa Pet](features/loja-petshop/catalogo-referencia.md). A disposição da vitrine usará os padrões estudados em [outras lojas](features/loja-petshop/referencias-vitrine.md), sem copiar sua identidade visual. A loja deverá funcionar sem mensalidade de hospedagem na primeira versão; essa restrição ainda precisa de uma solução operacional verificada.

**Porte esperado:** loja pequena no interior de São Paulo, poucas categorias, no máximo cerca de 100 produtos e um conjunto pequeno de imagens. Escolher serviços proporcionais a esse porte, mantendo o fluxo de pedidos confiável para uso real.

## Decisões ainda abertas

- Hospedagem gratuita da aplicação Spring Boot e domínio para uso real.
- Forma técnica de identificar e autenticar o proprietário; clientes não poderão escolher esse papel no cadastro.
- Provedor de armazenamento persistente das fotos enviadas pelo proprietário; o fluxo de envio e manutenção no painel está decidido.
- Provedor de e-mail para os códigos de acesso.
- Provedor e detalhes operacionais da integração com WhatsApp.
- Relação completa de produtos disponíveis, preços atuais e composição visual final da página principal. O Instagram é a fonte inicial, não uma garantia de estoque ou preço vigente.

PostgreSQL é a escolha proposta; **Neon é candidato para a produção, ainda não contratado ou configurado**. Essas escolhas não precisam ser inventadas neste mapa. Também não há comandos de build, teste ou execução para documentar enquanto a aplicação não existir.
