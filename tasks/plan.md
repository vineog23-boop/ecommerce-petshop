# Plano de implementação — catálogo público

**Estado:** proposta para revisão do Vinícius, em 2026-11-06. **Base:** [spec aprovada do catálogo](../.specs/features/catalogo/SPEC.md). A lista operacional está em [todo.md](todo.md). Nenhum código foi iniciado.

## Resultado esperado

Uma pessoa abre o site da Casa Pet em celular, encontra uma categoria, vê seus produtos e abre o detalhe de um produto. As informações exibidas vêm do Spring Boot e do PostgreSQL. Esta entrega não inclui conta, carrinho, edição de produtos ou envio de fotos pelo proprietário.

## Decisões de implementação propostas

1. **Uma aplicação Spring Boot:** serve as páginas HTML/CSS/JavaScript e os dados do catálogo por HTTP. Isso deixa visível o caminho navegador → controller → serviço → repositório → PostgreSQL sem exigir dois deploys.
2. **Organização por funcionalidade:** o código do catálogo ficará em `catalogo/web`, `catalogo/application`, `catalogo/domain` e `catalogo/persistence`, como discutido a partir do Medflow.
3. **Dois ambientes PostgreSQL:** desenvolvimento local na máquina do Vinícius e produção na nuvem. Neon continua candidata para o banco de produção. O catálogo inicialmente carregado a partir do Instagram será revisável pelo proprietário antes do uso real.
4. **Front-end simples:** HTML, Tailwind/CSS compilado e JavaScript de módulos pequenos. As páginas serão servidas pelo Spring Boot; o JavaScript buscará os dados por HTTP. A versão e os comandos de instalação serão fixados ao criar o projeto.
5. **Dados de exemplo separados dos dados publicados:** produtos inspirados no Instagram podem orientar testes e demonstrações, mas só entram no catálogo real após conferência de preço, disponibilidade, descrição e direito de uso da imagem.

O projeto foi movido para `~/Projetos/Programacao/java/ecommerce-petshop/`. O caminho anterior `~/Projetos/Programacao/Ecommerce Petshop/` é uma ligação para a pasta nova e preserva o acesso do Codex. O back-end inicial usará Java 21 e uma versão Spring Boot 4.1.x com suporte aberto; a versão exata será registrada no scaffold.

## Ordem e dependências

```text
Local do código + scaffold
          ↓
Categorias: banco/API → página/JavaScript
          ↓
Produtos por categoria: banco/API → cartões/JavaScript
          ↓
Detalhe: API → página/JavaScript
          ↓
Revisão em celular, teclado e dados reais
```

Cada seta representa algo que deve estar funcional antes do passo seguinte. As tarefas estão detalhadas em [todo.md](todo.md), com critérios e verificação. O primeiro marco útil é uma categoria carregada do back-end e mostrada no navegador; os demais repetem o mesmo caminho com novos dados.

## Pontos de aprendizagem durante a implementação

- No primeiro percurso, acompanhar uma requisição `fetch` no DevTools: URL, método, resposta JSON e atualização da página.
- Relacionar `web`, `application`, `domain` e `persistence` a uma operação real, sem usar nomes de camadas como finalidade em si.
- Comparar dados de desenvolvimento com dados autorizados para a loja antes de publicar.
- Após cada percurso, o Vinícius revisará o resultado no navegador e uma parte do código; o assistente explicará brevemente o porquê da decisão técnica aplicada.

## Verificação comum

- Executar os comandos reais de testes e build que forem criados com o scaffold; registrá-los na spec e neste plano antes de usá-los como evidência.
- Conferir os critérios CAT-01 a CAT-07 da spec com testes proporcionais e o fluxo manual no navegador, inclusive em largura de celular e por teclado.
- Não marcar uma tarefa como concluída apenas por compilar: o comportamento precisa aparecer na aplicação.

## Riscos e respostas

| Risco | Resposta prevista |
| --- | --- |
| Publicação antiga do Instagram não representa preço ou disponibilidade atual. | Usar dados de demonstração no desenvolvimento; só publicar itens conferidos pelo proprietário. |
| Foto recebida por upload se perde em hospedagem com disco temporário. | O upload fica para `gestao-catalogo`, com armazenamento persistente definido antes dessa etapa. |
| Hospedagem gratuita pode suspender a aplicação ociosa ou ultrapassar limites. | Escolher e testar o provedor antes do lançamento; o catálogo local não depende dessa escolha. |
| A aparência fica boa no computador, mas não no celular. | Verificar cada percurso no navegador em largura de celular e corrigir antes de avançar. |

## Decisões antes da primeira tarefa de código

1. **Resolvido:** diretório definitivo em `~/Projetos/Programacao/java/ecommerce-petshop/`, com ligação no caminho antigo do Codex.
2. **Resolvido quanto ao modelo:** desenvolvimento local e produção na nuvem terão PostgreSQL; iniciar o banco local e escolher o serviço de produção em etapas próprias.
3. **Resolvido como direção:** esboço simples da vitrine e dos cartões a partir das referências de grandes lojas, usando os produtos observados no Instagram; o proprietário poderá ajustar o catálogo no painel depois.
4. **Ainda durante T1:** registrar os comandos reais gerados pelo scaffold.

Hospedagem, e-mail, WhatsApp e autenticação do proprietário serão tratados nas capacidades correspondentes e antes do uso real; não bloqueiam o catálogo público local.
