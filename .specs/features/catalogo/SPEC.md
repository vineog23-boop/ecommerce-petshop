# Spec — catálogo público da Casa Pet

**Estado:** aprovada pelo Vinícius para planejamento em 2026-11-06, após registrar o porte de até cerca de 100 produtos. Decisões abertas continuam indicadas ao final. **Capacidade:** `catalogo`, conforme o [mapa aprovado](../../MAPA-CAPACIDADES.md).

## Objetivo e limite

Permitir que uma pessoa encontre produtos da Casa Pet pela vitrine e por categorias, consulte foto, descrição e preço e decida o que deseja comprar. Esta spec cobre a **consulta pública** ao catálogo. Carrinho e finalização pertencem a `pedidos`; cadastro e login pertencem a `acesso`; edição e envio de fotos pelo proprietário pertencem a `gestao-catalogo`.

A primeira entrega demonstrável será navegar da página inicial até uma categoria e abrir o detalhe de um produto, em celular, com informações vindas do back-end. Não chamar produtos de “mais vendidos” sem dados de vendas que sustentem essa afirmação.

**Porte esperado da primeira versão:** loja pequena do interior de São Paulo, poucas categorias e até cerca de 100 produtos no total. Não há justificativa para busca avançada, paginação complexa ou infraestrutura de grande escala nesta etapa. Essa estimativa orienta as escolhas, mas não substitui a medição de uso quando o site estiver publicado.

## Fonte e categorias iniciais

O [Instagram da Casa Pet](https://www.instagram.com/casapet_saocarlos/) é a fonte inicial para identificar produtos e preços. A [amostra documentada](../loja-petshop/catalogo-referencia.md) reúne publicações e valores observados, inclusive rações, areias para gatos e um cesto. As categorias abaixo são uma **organização proposta por nós dos itens publicados**, não nomes de seções declaradas pelo perfil:

| Categoria proposta | Itens observados no perfil |
| --- | --- |
| Alimentação | Rações para cães e gatos, sachês, petiscos e complementos. |
| Higiene e cuidados | Areias para gatos, escovas e produtos de limpeza. |
| Brinquedos | Brinquedos para pets. |
| Acessórios | Roupas, caixas de transporte, comedouros e bebedouros. |
| Utilidades | Cestos e bacias anunciados no perfil. |

Antes de disponibilizar um item para compra real, confirmar com o proprietário seu nome, descrição, variante ou embalagem, preço atual, disponibilidade e imagem autorizada. Uma publicação antiga serve como referência inicial, não como atualização automática do catálogo. A lista inicial completa será fechada com essa conferência; não há sincronização com o Instagram.

## Comportamento esperado

| ID | Critério de aceite | Origem |
| --- | --- | --- |
| CAT-01 | A página inicial apresenta a Casa Pet e caminhos visíveis para explorar categorias e produtos. | RF-15 |
| CAT-02 | A pessoa consegue ver as categorias disponíveis e abrir uma delas. | RF-01, RF-16 |
| CAT-03 | A página de categoria lista os produtos correspondentes com nome, imagem e preço; quando não houver itens, mostra uma mensagem compreensível. | RF-01, RNF-02 |
| CAT-04 | A pessoa consegue abrir o detalhe de um produto e ver nome, descrição, foto e preço em reais. | RF-02, RF-17 |
| CAT-05 | Produtos e preços exibidos vêm dos dados registrados no back-end; alterar o HTML ou JavaScript do navegador não altera o catálogo persistido. | Objetivo da arquitetura e integridade dos dados |
| CAT-06 | O percurso página inicial → categoria → produto funciona em largura de celular e com navegação por teclado. | RNF-01, RNF-02 |
| CAT-07 | O catálogo não exibe como vendável um produto sem preço válido ou que tenha sido desativado pelo proprietário. | Regra proposta para evitar pedidos de itens indisponíveis |

O layout usa como referência a clareza de navegação observada em [Petlove, Cobasi e Petz](../loja-petshop/referencias-vitrine.md). Cabeçalho, categorias, cartões de produto e acesso ao carrinho devem ser fáceis de encontrar. Banner, busca, filtros e posição exata dos elementos ainda serão decididos no desenho das telas. O acesso ao carrinho poderá ser preparado visualmente, mas só será funcional quando a capacidade `pedidos` for implementada.

## Stack e estrutura previstas

- **Back-end:** Java 21 com Spring Boot, uma aplicação modular. A funcionalidade `catalogo` terá `web` para receber pedidos HTTP, `application` para coordenar consultas, `domain` para conceitos e regras e `persistence` para acesso aos dados. Usar uma versão 4.1.x com suporte aberto no scaffold; registrar a versão exata quando instalada.
- **Banco:** PostgreSQL tanto no desenvolvimento local quanto em produção na nuvem. Neon é candidato para o ambiente publicado; o provedor será definido antes do deploy.
- **Interface:** HTML, CSS, Tailwind e JavaScript. As páginas públicas serão servidas pelo Spring Boot e consultarão o catálogo por requisições HTTP; os detalhes dessa comunicação serão mostrados durante a implementação.
- **Arquivos:** os registros do produto guardam a referência da foto; o envio pelo proprietário e o armazenamento persistente do arquivo serão especificados em `gestao-catalogo`. Fotos enviadas durante o uso não devem depender do disco temporário da aplicação hospedada.
- **Imagens:** o volume inicial esperado é pequeno; a implementação do envio deverá limitar tamanho e formato e preparar imagens adequadas à web, sem exigir infraestrutura de mídia em grande escala.
- **Documentação:** specs em `.specs/features/<id>/`; decisões gerais em `.specs/STATE.md`.

## Comandos e convenções

A primeira etapa criou Java 21, Spring Boot 4.1.2, Maven Wrapper e Tailwind 4.3.5. Comandos executados:

```bash
npm install
npm run build:css
./mvnw package
java -jar target/casapet-0.0.1-SNAPSHOT.jar
```

`./mvnw test` é o comando de testes Maven, mas ainda não há testes automatizados na etapa inicial. `./mvnw spring-boot:run` está documentado para desenvolvimento; o JAR foi o modo usado para a verificação manual. O código Java começa em `br.com.casapet`; os pacotes do catálogo serão adicionados nas etapas seguintes. O estilo inicial segue nomes descritivos e uma classe de entrada pequena, como [CasaPetApplication.java](../../../src/main/java/br/com/casapet/CasaPetApplication.java).

## Verificação

- Testar as regras e consultas do catálogo com dados controlados: categoria com itens, categoria vazia, produto existente e inexistente, preço válido e produto desativado.
- Testar que a resposta HTTP entrega os dados necessários sem expor detalhes internos de persistência.
- Percorrer CAT-01 a CAT-06 no navegador, em celular e computador, verificando imagens, preços, teclado e textos alternativos.
- Antes de usar o catálogo com clientes reais, comparar nomes, preços, disponibilidade e imagens com o proprietário; a amostra do Instagram não substitui essa conferência.

## Limites desta spec

- **Sempre:** usar o back-end como fonte dos dados exibidos; manter as informações do produto verificáveis; preservar a navegação em celular.
- **Decidir em conjunto antes de acrescentar:** busca, filtros, promoções, cálculo de popularidade ou sincronização com Instagram.
- **Não fazer:** publicar preços antigos como atuais sem conferência; exibir “mais vendidos” sem dados; usar arquivos locais temporários como armazenamento definitivo de fotos.

## Pontos a resolver antes da implementação

1. Quais itens da amostra entram na primeira carga após conferência de preço e disponibilidade?
2. Qual desenho de página inicial e de cartão de produto será usado? Os padrões pesquisados são referência, não uma cópia.
3. Como representar variantes ou embalagens diferentes de um mesmo produto no catálogo?
4. Qual será o armazenamento persistente das fotos quando o painel do proprietário for desenvolvido?
