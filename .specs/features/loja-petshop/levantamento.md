# Registro da modelagem — loja do pet shop

**Estado:** histórico de decisões e dúvidas para discutirmos juntos; não há etapa de entrevista. **Data:** 2026-11-06.

Este documento conserva observações do início do projeto. A [base atual dos requisitos fundamentais](base-requisitos.md) concentra o que o produto precisa fazer.

## 1. O que sabemos

- O produto será um site para o pet shop do tio da namorada do Vinícius.
- O projeto deve ser funcional, cobrir front-end e back-end e servir como referência de portfólio.
- O back-end deve permitir aplicar o aprendizado em Java e Spring Boot.
- Requisitos, arquitetura, banco, implantação e organização do projeto serão discutidos antes de decisões definitivas.
- O Vinícius deseja entender as razões das escolhas, participar da implementação e fazer revisão manual.
- A primeira versão deve ser usada pelo pet shop, e o cliente enviará o pedido pelo WhatsApp da loja.
- O cliente navegará por categorias e produtos com preço, adicionará produtos e quantidades ao carrinho e verá preços e total antes de enviar o pedido.
- A mensagem ao WhatsApp conterá produtos, quantidades, preço unitário de cada um e o total dos produtos.
- O cliente informará nome e telefone; o pedido será registrado no sistema para a equipe consultar e aceitar.
- O cliente escolherá retirada sem taxa ou entrega com frete informado manualmente no WhatsApp.
- Um benefício por quantidade de compras foi citado como possibilidade futura, sem regra definida.
- A equipe do pet shop atualizará produtos, preços e fotos.
- O [Instagram da Casa Pet](https://www.instagram.com/casapet_saocarlos/) é a referência principal de produtos e valores neste momento.

Depois que o Vinícius liberou o acesso, foram verificadas publicações do perfil em 2026-11-06. Elas mostram rações para cães e gatos, areia para gatos, petiscos, brinquedos, roupas, caixas de transporte, comedouros, bebedouros e itens de utilidade como cestos e bacias. A [amostra de produtos e preços](catalogo-referencia.md) mantém links para as publicações. Não foi possível concluir, a partir da amostra, se o pet shop oferece serviços.

As publicações orientam o catálogo inicial, mas não precisam definir todas as regras do produto. Nós decidiremos as regras e as registraremos antes de implementar.

## 2. Papéis modelados

| Papel | Responsabilidade no produto |
| --- | --- |
| Cliente | Consultar catálogo, montar carrinho, informar dados, escolher recebimento e registrar pedido. |
| Equipe do pet shop | Manter catálogo, consultar pedidos e clientes, combinar frete quando necessário e aceitar pedidos. |
| Vinícius e assistente | Definir e revisar os requisitos, modelar o sistema, implementar e verificar cada parte. |

O cliente e a equipe são atores do sistema. Vinícius e assistente conduzem o projeto, mas não são atores do produto por esse motivo.

## 3. Decisões tomadas e pendências

| Nº | Decisão | Por que importa |
| --- | --- | --- |
| D1 | Selecionar categorias e produtos iniciais a partir do Instagram. | Define o catálogo que será construído. |
| D2 | Resolvida: conta com nome, e-mail e telefone; login por código enviado ao e-mail no checkout. | Define autenticação e perfil do cliente. |
| D3 | Resolvida para o fluxo principal: Enviado, Aceito e Pronto; recusa e cancelamento continuam em aberto. | Define a evolução do pedido. |
| D4 | Resolvida: somente o proprietário acessa a área administrativa; forma de login ainda a definir. | Protege clientes e operações da loja. |
| D5 | Pendente para a etapa final: conta de WhatsApp da loja, conteúdo das mensagens ao cliente e implementação da integração automática. | Completa a comunicação de cada estado do pedido ao cliente; o proprietário acompanha pedidos no sistema. |

## 4. Base atual do produto

Os requisitos funcionais, regras de negócio, qualidades essenciais e o cenário de aceitação estão na [base de requisitos](base-requisitos.md). Este arquivo permanece como histórico das decisões, para não manter duas listas de requisitos com IDs diferentes.

## 5. Outros temas para decidir ao preparar o lançamento

- **Dados pessoais:** identificar quais dados serão coletados, por quanto tempo e quem poderá vê-los.
- **Segurança:** decidir como a equipe acessará a manutenção do catálogo.
- **Operação:** definir quem manterá conteúdo, domínio, hospedagem, cópias de segurança e custos recorrentes.
- **Desempenho:** medir quando houver um catálogo e um fluxo definidos, em vez de inventar metas agora.

## 6. Critério para encerrar esta etapa

Vinícius e assistente revisam o fluxo principal, os atores, as regras e o que caracteriza a primeira entrega útil. A [base de requisitos](base-requisitos.md) é ajustada conforme as decisões; as dúvidas restantes ficam explícitas.

## 7. UML proposta

O [rascunho de casos de uso](casos-de-uso-rascunho.puml) mostra os objetivos do cliente e do proprietário. O [rascunho de atividades](atividade-pedido-rascunho.puml) mostra a ordem das ações no pedido. O [diagrama de classes conceituais](classes-dominio-rascunho.puml) ajuda a discutir os elementos do negócio sem decidir código ou banco. Todos aguardam revisão.
