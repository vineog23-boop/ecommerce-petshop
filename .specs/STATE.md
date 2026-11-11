# Estado do projeto — loja do pet shop

## Objetivo

Construir, com participação e revisão manual do Vinícius, uma aplicação de ponta a ponta para o pet shop do tio de sua namorada. O projeto também deve demonstrar decisões de engenharia em seu portfólio.

## Etapa atual

Modelagem colaborativa dos requisitos, com fluxo principal consolidado para revisão. A primeira versão será usada pelo negócio. O cliente explorará uma vitrine e categorias, abrirá detalhes, montará o carrinho e só precisará entrar na conta ao finalizar. A composição visual da home ainda está aberta. Após escolher retirada ou entrega, o pedido ficará registrado e vinculado ao cliente. O proprietário será o único usuário da área administrativa; verá os pedidos no sistema, consultará histórico, aceitará e marcar pedidos como prontos. Os estados do fluxo principal são Enviado, Aceito e Pronto. A conta de WhatsApp da loja deverá enviar automaticamente ao cliente uma confirmação após o registro e uma atualização após cada mudança de estado. O proprietário não depende de mensagens no próprio WhatsApp para receber pedidos. O frete da entrega será combinado manualmente; o Instagram da Casa Pet é a referência inicial de produtos e valores. A integração automática com WhatsApp será implementada depois do fluxo principal de back-end e front-end. O [mapa de capacidades](MAPA-CAPACIDADES.md) e a [spec do catálogo público](features/catalogo/SPEC.md) foram aprovados para planejamento; o plano de implementação aguarda revisão.

Os documentos em `.specs/features/loja-petshop/` são **rascunhos de descoberta**, ainda não uma especificação formal aprovada. Nenhum código foi iniciado.

## Como vamos aprender e construir

O guia de agents é uma referência, não uma sequência obrigatória para esta conversa. O fluxo principal é a construção guiada: discutir uma decisão real, expor alternativas e consequências, pedir uma previsão ou escolha relevante ao Vinícius, aplicar em uma parte pequena do sistema, verificar o comportamento e revisar juntos. O assistente pode implementar; a revisão manual do Vinícius e explicações curtas dos conceitos fazem parte de cada etapa.

Manter requisitos e decisões em `.specs/`; usar UML apenas quando ajudar a entender atores, fluxo ou domínio. Usar as skills especializadas quando sua tarefa surgir, sem encadear todos os roteiros por padrão. Preparar `AGENTS.md` e `CLAUDE.md` locais quando houver convenções concretas para registrar; não inventar comandos antes da aplicação existir.

**Localização a decidir antes de criar código:** a pasta foi movida para `~/Projetos/Programacao/Ecommerce Petshop/`; o guia global sugere `~/Projetos/Programacao/java/` para projetos Java. Decidir onde o código ficará antes de criar a aplicação.

## Etapas de aprendizagem propostas

1. Entender o negócio e transformar observações em requisitos verificáveis.
2. Modelar o fluxo principal e comparar opções de arquitetura, dados e interface com justificativas.
3. Construir partes pequenas e executáveis de front-end e back-end, com participação ativa do Vinícius.
4. Testar, inspecionar no navegador e revisar o comportamento e o código após cada parte.
5. Preparar operação e implantação para uso real quando a solução estiver validada.

O código e as decisões devem continuar coerentes com os requisitos em `.specs/`. Uma hipótese só vira requisito confirmado após validação. O guia formal continua disponível para uma spec, revisão ou publicação quando isso trouxer clareza ou segurança.

## Próxima decisão

Revisar com Vinícius o scaffold da primeira tarefa, que compila e entrega uma página HTML com Tailwind. Em seguida, executar T2 da [lista de tarefas](../tasks/todo.md): PostgreSQL local, categorias persistidas e consulta HTTP; produção também terá PostgreSQL na nuvem. O projeto foi movido para `~/Projetos/Programacao/java/ecommerce-petshop/`; o caminho antigo é uma ligação que mantém o acesso do Codex. Hospedagem gratuita do Spring Boot, mecanismo de autenticação do proprietário e provedor de armazenamento de fotos continuam em aberto. O envio das fotos pelo proprietário no painel está decidido. Deixar a escolha do provedor e a implementação da automação do WhatsApp para depois de o fluxo principal estar funcional. Vinícius e assistente tomarão as decisões juntos, sem etapa de entrevista.

## Registro de decisões

| Data | Decisão | Situação |
| --- | --- | --- |
| 2026-11-06 | Java com Spring Boot no back-end e uma interface web no front-end fazem parte do objetivo de aprendizagem. | Diretriz do projeto |
| 2026-11-06 | Usar o guia de agents como apoio; conduzir o projeto por aprendizagem, decisões discutidas, implementação pequena, verificação e revisão manual. | Preferência explícita do Vinícius |
| 2026-11-06 | Primeira versão para uso real, com WhatsApp como canal de conversa. | Confirmado pelo Vinícius; fluxo detalhado abaixo |
| 2026-11-06 | Cliente monta uma lista de produtos e a envia pelo WhatsApp ao finalizar. | Ideia inicial substituída: o pedido fica no sistema e a loja envia atualizações automáticas ao cliente |
| 2026-11-06 | Site exibe categorias e preços; carrinho reúne produtos e quantidades e calcula o total. | Confirmado pelo Vinícius; o envio manual pelo WhatsApp foi substituído pela automação posterior |
| 2026-11-06 | Equipe do pet shop mantém produtos, preços e fotos; Instagram é a principal referência inicial. | Confirmado pelo Vinícius; forma de atualização pendente |
| 2026-11-06 | Cadastrar cliente com nome, e-mail e telefone; login por código enviado ao e-mail exigido no checkout; registrar pedido ligado à conta. | Confirmado pelo Vinícius |
| 2026-11-06 | Cliente escolhe retirada sem taxa ou entrega com frete combinado manualmente no WhatsApp. | Confirmado pelo Vinícius |
| 2026-11-06 | A página inicial será uma vitrine de produtos; navegação por categorias, detalhes e carrinho antes do login. | Vitrine confirmada; layout e destaques ainda abertos |
| 2026-11-06 | Só o proprietário acessa a área administrativa; pedidos passam por Enviado, Aceito e Pronto. | Confirmado pelo Vinícius; recusa e cancelamento fora do fluxo principal |
| 2026-11-06 | A conta de WhatsApp da loja enviará automaticamente ao cliente confirmação do pedido e atualizações após mudanças para Aceito e Pronto; o proprietário acompanha pedidos no sistema. | Correção explícita do Vinícius; implementação da integração adiada até o fluxo principal funcionar |
| 2026-11-06 | Desconto por quantidade de compras é possibilidade futura, sem regra definida. | Não incluir no primeiro fluxo |
| 2026-11-06 | Requisitos e regras serão decididos por Vinícius e assistente, sem entrevista; conceitos serão explicados resumidamente na conversa. | Preferência explícita do Vinícius |
| 2026-11-06 | Usar um Spring Boot organizado por funcionalidades, com áreas de cliente e proprietário no mesmo site e JavaScript para interação com o back-end. | Proposta discutida e aceita como direção inicial; detalhes técnicos a especificar |
| 2026-11-06 | Dividir a especificação detalhada por capacidades, começando por um mapa revisável. | Mapa criado e aprovado; ver registro seguinte |
| 2026-11-06 | Mapa de capacidades aprovado: catálogo, acesso, gestão do catálogo, pedidos e notificações; specs detalhadas por capacidade. | Confirmado pelo Vinícius; primeira spec em revisão |
| 2026-11-06 | Hospedagem precisa ser gratuita; o proprietário enviará fotos pelo painel, que aparecerão na vitrine; Instagram orientará os produtos e categorias iniciais, e lojas conhecidas orientarão o desenho. | Confirmado pelo Vinícius; provedor de hospedagem, armazenamento e catálogo final pendentes |
| 2026-11-06 | A loja é pequena, no interior de São Paulo; primeira versão com poucas categorias e cerca de 100 produtos no máximo, com baixo volume de imagens. | Premissa de dimensionamento informada pelo Vinícius; verificar uso real após publicação |
| 2026-11-06 | A spec do catálogo público foi aprovada para avançar após a revisão do porte esperado; o primeiro plano cobre apenas essa capacidade. | Plano e tarefas criados para revisão do Vinícius |
| 2026-11-06 | Projeto em `~/Projetos/Programacao/java/ecommerce-petshop/`, com ligação no caminho anterior do Codex; PostgreSQL local no desenvolvimento e PostgreSQL na nuvem em produção; vitrine inicial baseada em padrões de grandes lojas e nos produtos observados no Instagram. | Diretrizes dadas pelo Vinícius; primeira tarefa de código autorizada |
| 2026-11-06 | Scaffold Spring Boot 4.1.2/Java 21 e Tailwind 4.3.5 criado; Maven package e CSS build passaram; página inicial aberta no navegador. | T1 verificada; aguardando revisão manual do Vinícius |
