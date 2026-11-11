# Base de requisitos — loja da Casa Pet

**Estado:** proposta para discussão e decisão conjunta com Vinícius. **Data:** 2026-11-06.

## 1. Objetivo do produto

Permitir que o cliente encontre produtos da Casa Pet em uma vitrine, navegue por categorias, consulte detalhes e preços, monte o carrinho e finalize o pedido após criar uma conta ou entrar nela por código enviado ao e-mail. O site registra o pedido vinculado à conta e solicita o envio automático de uma confirmação ao WhatsApp do cliente **a partir da conta da loja**. O proprietário vê o pedido no sistema, sem depender do próprio WhatsApp, consulta o histórico do cliente, aceita pedidos e marca pedidos como prontos. Cada mudança de estado gera uma nova mensagem automática ao cliente. O Instagram da loja é a referência inicial de produtos e preços; a [amostra consultada](catalogo-referencia.md) ajuda a preparar o catálogo.

O primeiro resultado útil é o caminho completo **explorar a vitrine → escolher produtos → montar o carrinho → entrar na conta no checkout → escolher retirada ou entrega → registrar o pedido → proprietário aceitar → marcar como pronto** funcionando em celular. Os três estados são **Enviado → Aceito → Pronto**. “Enviado” significa que o pedido foi registrado no sistema, não que já foi aceito ou está sendo preparado. O cliente recebe mensagens automáticas da conta da loja após o registro e após cada mudança de estado. A integração de mensagens será implementada depois do fluxo principal de front-end e back-end.

## 2. Como classificar os requisitos

| Tipo | Pergunta que responde | Exemplo neste projeto |
| --- | --- | --- |
| Objetivo de negócio | Para que o produto existe? | Receber e organizar pedidos originados no site. |
| Requisito funcional (RF) | O que o sistema faz? | Adicionar um produto com quantidade ao carrinho. |
| Regra de negócio (RN) | Que condição do negócio governa o comportamento? | Total dos produtos = soma de quantidade × preço unitário. |
| Requisito não funcional (RNF) | Que qualidade o sistema precisa ter? | O fluxo de compra deve funcionar em celular e proteger os dados do cliente. |
| Restrição | Que limite ou escolha já foi imposto? | O back-end será desenvolvido em Java/Spring Boot para atender ao objetivo de aprendizagem. |

Essa separação evita confundir uma necessidade do cliente com uma tecnologia ou uma solução de interface. Os itens abaixo são decisões que o Vinícius e o assistente estão construindo e revisando juntos; não há uma etapa de entrevista com o responsável da loja.

## 3. Pessoas e objetivos

| Papel | Objetivo |
| --- | --- |
| Cliente | Explorar a vitrine e as categorias, consultar detalhes, montar o carrinho, entrar na conta no checkout, escolher retirada ou entrega e enviar o pedido. |
| Proprietário | Acessar a área restrita, manter o catálogo, consultar pedidos e histórico de clientes, aceitar pedidos e marcá-los como prontos. |

O cadastro cria uma conta persistida com nome, e-mail e telefone. O cliente pode navegar e montar o carrinho sem login; a autenticação por código recebido no e-mail é exigida ao iniciar a finalização. A área administrativa terá acesso apenas do proprietário. A forma técnica de autenticação dele será definida na arquitetura.

## 4. Requisitos funcionais fundamentais

| ID | Comportamento esperado | Origem |
| --- | --- | --- |
| RF-01 | Exibir categorias e os produtos de cada categoria. | Pedido do Vinícius. |
| RF-02 | Exibir nome, foto, descrição e preço na página de detalhes de cada produto. | Pedido do Vinícius. |
| RF-03 | Adicionar produtos e quantidades ao carrinho, continuar navegando e permitir corrigir a seleção antes de enviar. | Pedido do Vinícius. |
| RF-04 | Mostrar no carrinho itens, quantidades, preços unitários e total dos produtos. | Pedido do Vinícius. |
| RF-05 | Permitir criar uma conta com nome, e-mail e telefone e armazenar esses dados no banco de dados. | Decisão do Vinícius. |
| RF-06 | Permitir escolher retirada na loja ou entrega. | Pedido do Vinícius. |
| RF-07 | Registrar no back-end um pedido ligado à conta autenticada do cliente, com itens, quantidades, preços e modalidade escolhida. | Pedido do Vinícius. |
| RF-08 | Após registrar o pedido, disponibilizá-lo na área do proprietário para consulta e atendimento, sem exigir que ele consulte o WhatsApp. | Correção explícita do Vinícius. |
| RF-09 | Permitir que o proprietário consulte pedidos e veja cliente, itens, preços, modalidade e estado. | Decisão do Vinícius. |
| RF-10 | Permitir que o proprietário aceite um pedido Enviado, alterando-o para Aceito. | Decisão do Vinícius. |
| RF-11 | Permitir que o proprietário cadastre e corrija produtos, categorias e preços, envie fotos pelo painel e veja essas alterações refletidas na vitrine. | Responsável e forma de manutenção definidos pelo Vinícius; armazenamento das fotos a escolher. |
| RF-12 | Permitir que o proprietário consulte o histórico de pedidos ligado à conta de cada cliente. | Decisão do Vinícius. |
| RF-13 | Permitir que o cliente solicite um código enviado ao e-mail cadastrado e entre na própria conta ao informar um código válido. | Escolha do Vinícius pelo login por e-mail. |
| RF-14 | Ao solicitar a finalização, exigir login ou cadastro sem perder os itens do carrinho; depois permitir confirmar e registrar o pedido. | Decisão do Vinícius. |
| RF-15 | Exibir uma página inicial que funcione como vitrine e permita ao cliente chegar aos produtos e categorias. | Objetivo confirmado pelo Vinícius; composição visual em aberto. |
| RF-16 | Permitir navegar pelos produtos a partir das categorias. | Decisão do Vinícius. |
| RF-17 | Permitir abrir a página de detalhes de um produto a partir do catálogo. | Decisão do Vinícius. |
| RF-18 | Restringir a área administrativa e suas ações ao proprietário autenticado. | Decisão do Vinícius. |
| RF-19 | Permitir que o proprietário marque como Pronto um pedido Aceito. | Decisão do Vinícius. |
| RF-20 | Enviar automaticamente, pela conta de WhatsApp da loja, uma confirmação ao cliente com o resumo e o estado Enviado após o registro do pedido. | Correção explícita do Vinícius; integração será implementada por último. |
| RF-21 | Enviar automaticamente, pela conta de WhatsApp da loja, uma atualização ao cliente sempre que o proprietário mudar o pedido para Aceito ou Pronto. | Correção explícita do Vinícius; integração será implementada por último. |

O formato do histórico será decidido com a área do proprietário. Descontos e promoções ligados ao histórico são uma **possibilidade futura**: faltam as condições, os valores e a definição de quais pedidos contam. Busca, pagamento online, cálculo automático de frete e estoque em tempo real também ficam fora do primeiro fluxo. O serviço de envio de e-mail será escolhido durante a implementação. A integração com WhatsApp é um requisito do produto, mas sua solução técnica fica para uma etapa final. Banner, posição das categorias e produtos em destaque são ideias de interface, registradas como [referências para a vitrine](referencias-vitrine.md), não requisitos fechados. O Instagram é a fonte inicial de produtos e categorias propostas; preços e disponibilidade precisam ser conferidos antes do uso real.

## 5. Regras de negócio fundamentais

| ID | Regra | Estado |
| --- | --- | --- |
| RN-01 | Um item do carrinho tem produto e quantidade positiva. | Proposta para validação. |
| RN-02 | O valor de cada item é quantidade × preço unitário; o total dos produtos é a soma dos itens. | Deriva do fluxo descrito pelo Vinícius. |
| RN-03 | A confirmação ao cliente deve refletir o pedido registrado a partir do carrinho revisado; as mensagens seguintes devem refletir o estado efetivo do pedido. | Deriva do fluxo descrito pelo Vinícius. |
| RN-04 | Um carrinho vazio não gera pedido. | Proposta para validação. |
| RN-05 | Retirada na loja não acrescenta taxa de entrega. | Definido pelo Vinícius. |
| RN-06 | Para entrega, o site mostra o total dos produtos; o valor do frete é informado manualmente na conversa pelo WhatsApp. | Definido pelo Vinícius. |
| RN-07 | O pedido começa como Enviado; somente o proprietário pode mudá-lo para Aceito e, depois, para Pronto, nessa ordem. | Definido pelo Vinícius. |
| RN-08 | O pedido registrado conserva os itens, quantidades e preços apresentados no fechamento, para que o proprietário veja o que o cliente enviou. | Proposta necessária ao histórico do pedido. |
| RN-09 | Somente um cliente autenticado pode finalizar o carrinho e registrar um pedido em sua conta. | Definido pelo Vinícius. |
| RN-10 | Enviado significa pedido registrado no sistema; não significa Aceito nem “em preparo”. A entrega de uma mensagem pelo WhatsApp não define nem altera o estado. | Distinção necessária para não confundir pedido e mensagem. |
| RN-11 | Uma falha no envio de mensagem não deve apagar o pedido já registrado; o proprietário precisa poder consultá-lo no sistema. | Proposta para confiabilidade operacional. |

Exemplo verificável: duas unidades de R$ 12,00 e uma de R$ 14,00 somam **R$ 38,00 em produtos**. Na retirada, não há taxa de entrega. Na entrega, o frete será combinado no WhatsApp e o valor final será informado pela loja. Descontos e forma de pagamento ainda não foram definidos.

## 6. Qualidades essenciais para a primeira versão

| ID | Qualidade | Como verificar depois |
| --- | --- | --- |
| RNF-01 | O cliente consegue completar o fluxo em uma tela de celular. | Executar o fluxo completo no navegador em largura de celular. |
| RNF-02 | Textos, controles e erros são compreensíveis e acessíveis. | Conferir teclado, rótulos, contraste e alternativas das imagens nas telas construídas. |
| RNF-03 | Apenas o proprietário autenticado pode acessar a área administrativa, ver dados de clientes, alterar estados de pedidos e manter o catálogo. | Testar acesso e permissões na área restrita. |
| RNF-04 | Nome, e-mail, telefone, histórico e códigos de acesso do cliente não devem ser expostos a outros clientes. | Verificar as respostas da aplicação e as telas públicas. |

Metas numéricas de desempenho, hospedagem e disponibilidade serão estabelecidas quando conhecermos o catálogo e o ambiente real de operação.

## 7. Cenário principal de aceitação

1. O cliente abre a vitrine, encontra produtos, entra em uma categoria e abre os detalhes de um produto.
2. Adiciona dois produtos ao carrinho em momentos diferentes, informa as quantidades e confere o total calculado.
3. Solicita a finalização. Se ainda não estiver autenticado, cria uma conta ou entra com código por e-mail; o carrinho continua disponível. Escolhe retirada ou entrega e confirma.
4. O site registra o pedido como Enviado e vinculado à conta. O proprietário consegue consultá-lo na área restrita e ver o histórico do cliente.
5. O sistema solicita o envio automático, pela conta de WhatsApp da loja, de uma confirmação de recebimento ao cliente. O proprietário vê o pedido no sistema. Uma falha na mensagem não remove o pedido.
6. O proprietário combina manualmente o frete quando houver entrega, aceita o pedido no sistema e o cliente recebe uma mensagem automática com o estado Aceito.
7. Depois, o proprietário marca o pedido como Pronto e o cliente recebe outra atualização automática.

## 8. Decisões que vamos tomar juntos

1. Quais categorias e produtos do [Instagram](https://www.instagram.com/casapet_saocarlos/) entram no catálogo inicial? Há serviços a representar?
2. Quais dados da conta devem aparecer nas notificações do WhatsApp? Como o proprietário localizará o histórico do cliente?
3. Como a conta de WhatsApp da loja enviará automaticamente as mensagens ao cliente? Provedor, custos, modelos de mensagem e autorização do cliente serão estudados na etapa de integração, após o fluxo principal funcionar. Promoções exigem uma decisão separada.
4. Haverá recusa ou cancelamento além dos três estados do fluxo principal? O cliente verá o estado no site?
5. Qual serviço persistirá as fotos enviadas pelo proprietário no painel e como será feita a conferência do catálogo antes do lançamento?

Não haverá uma etapa de entrevista. Essas decisões serão discutidas e registradas no projeto; a operação real poderá orientar ajustes depois. Situações de mudança de preço com o carrinho aberto ficam para o detalhamento da implementação.

## 9. UML para entender o negócio

- [Casos de uso](casos-de-uso-rascunho.puml): mostram **quem** usa o sistema e **para quê**.
- [Atividades](atividade-pedido-rascunho.puml): mostram **em que ordem** o cliente e o site agem no pedido.
- [Classes conceituais](classes-dominio-rascunho.puml): mostram **quais conceitos** existem e como se relacionam; agora distinguem carrinho (seleção) de pedido (registro para a loja). Não definem ainda tabelas, endpoints ou classes Java.

Os arquivos `.puml` são fontes PlantUML. Para visualizá-los, abra esta pasta no VS Code com uma extensão PlantUML e use a prévia do diagrama. O assistente explicará os **conceitos de engenharia** na conversa conforme forem aplicados, sem traduzir cada diagrama por escrito.
