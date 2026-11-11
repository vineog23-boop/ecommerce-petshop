# Tarefas — catálogo público

**Estado:** propostas; executar somente após revisão do [plano](plan.md). A [spec](../.specs/features/catalogo/SPEC.md) define os critérios do produto. Os arquivos citados abaixo são **locais previstos**, não arquivos já existentes. Comandos exatos serão preenchidos quando o scaffold existir.

## T1 — Preparar aplicação executável

- [x] Confirmar o diretório do código e criar um projeto Spring Boot com Maven Wrapper e Java 21. As conexões PostgreSQL local/produção serão configuradas em T2, quando o banco passar a ser usado.
- [x] Fazer o Spring Boot entregar uma página HTML mínima e preparar a compilação do Tailwind para CSS local.
- [x] Registrar comandos reais de iniciar, testar e gerar o pacote; executar build e inicialização.

**Depende de:** aprovação deste plano e decisão do diretório. **Verificação feita:** `npm run build:css` e `./mvnw package` passaram; o JAR iniciou em `localhost:8080` e a página com CSS apareceu no navegador. Ainda não há testes automatizados. **Arquivos criados:** entrada Spring, `pom.xml`, Maven Wrapper, página inicial, CSS/Tailwind, `package.json`, lockfile e README. **Tamanho:** médio.

## T2 — Consultar categorias no back-end

- [ ] Persistir categorias no PostgreSQL com identificador e nome, incluindo as categorias propostas pela spec para desenvolvimento.
- [ ] Expor consulta pública de categorias pelo Spring Boot, retornando dados apropriados à interface.
- [ ] Verificar a resposta com teste focado e uma requisição manual; lista vazia deve ter resposta previsível.

**Depende de:** T1. **Verificação:** teste do endpoint, build e resposta HTTP observada. **Arquivos previstos:** migração de banco, modelo/repositório, serviço/controller e teste focado, distribuídos em mudanças pequenas se excederem cerca de cinco arquivos. **Tamanho:** médio.

## T3 — Mostrar categorias na vitrine

- [ ] Buscar categorias com JavaScript e mostrá-las como caminhos de navegação na página inicial.
- [ ] Tratar lista vazia e falha de carregamento com mensagens compreensíveis.
- [ ] Conferir no DevTools a requisição e revisar a página em celular e por teclado com o Vinícius.

**Depende de:** T2. **Verificação:** caminho completo banco → API → navegador, inclusive estados vazios/erro. **Arquivos previstos:** HTML, módulo JavaScript e CSS gerado a partir do Tailwind. **Tamanho:** pequeno. **Marco 1:** CAT-01 e CAT-02 demonstráveis.

## Marco 1 — Categorias funcionando

- [ ] Testes e build passam com os comandos reais do projeto.
- [ ] O Vinícius vê uma categoria carregada do PostgreSQL na página e encontra a requisição no DevTools.

## T4 — Consultar produtos de uma categoria no back-end

- [ ] Persistir produto com categoria, nome, descrição, preço e referência de imagem; usar somente dados de desenvolvimento até conferência para uso real.
- [ ] Expor consulta dos produtos de uma categoria; não retornar produto desativado ou sem preço válido como vendável.
- [ ] Testar categoria com produtos, vazia e inexistente, além da regra de visibilidade.

**Depende de:** T2. **Verificação:** testes focados, build e respostas HTTP dos três cenários. **Arquivos previstos:** migração, modelo/repositório, serviço/controller e testes, fracionados se necessário. **Tamanho:** médio.

## T5 — Mostrar produtos por categoria

- [ ] Ao abrir uma categoria, buscar seus produtos e mostrar cartões com nome, imagem e preço em reais.
- [ ] Mostrar uma mensagem quando não houver produtos e oferecer retorno à vitrine.
- [ ] Revisar cartões em celular, teclado e DevTools com o Vinícius.

**Depende de:** T3 e T4. **Verificação:** caminho completo categoria → lista com produtos ou vazio no navegador. **Arquivos previstos:** página de categoria, JavaScript e estilos. **Tamanho:** pequeno. **Marco 2:** CAT-03 e CAT-05 demonstráveis.

## Marco 2 — Lista de produtos funcionando

- [ ] Testes e build passam; os cenários com produtos e sem produtos aparecem corretamente no navegador.
- [ ] O Vinícius revisa os cartões em uma largura de celular e confirma que preços vêm da resposta do back-end.

## T6 — Abrir detalhe de um produto

- [ ] Expor consulta pública de produto por identificador, com resposta previsível para produto inexistente ou desativado.
- [ ] Criar página que mostre nome, descrição, foto e preço retornados pela API.
- [ ] Conferir com teste focado e navegação manual da lista ao detalhe, inclusive em celular.

**Depende de:** T4 e T5. **Verificação:** teste HTTP, build e percurso completo no navegador. **Arquivos previstos:** serviço/controller e teste, página de detalhe e JavaScript; dividir se exceder cerca de cinco arquivos. **Tamanho:** médio. **Marco 3:** CAT-04 demonstrável.

## T7 — Revisar catálogo e preparar dados reais

- [ ] Verificar CAT-01 a CAT-07, textos alternativos, foco de teclado, estados de erro e layout em celular.
- [ ] Registrar o que falta conferir de cada produto observado no Instagram antes de publicá-lo como vendável.
- [ ] Atualizar documentação com comandos executados, limitações e decisões tomadas; revisar manualmente com o Vinícius.

**Depende de:** T1–T6. **Verificação:** testes e build reais, fluxo completo no navegador e revisão da spec. **Arquivos previstos:** ajustes localizados e documentação. **Tamanho:** médio. **Marco final:** catálogo público pronto para integrar às próximas capacidades, sem pressupor que os preços do Instagram estejam atuais.

## Marco final — Catálogo revisado

- [ ] CAT-01 a CAT-07 foram verificados com testes e navegação manual em celular, computador e teclado.
- [ ] O Vinícius revisou o resultado e as pendências de dados reais estão registradas antes de qualquer publicação.
