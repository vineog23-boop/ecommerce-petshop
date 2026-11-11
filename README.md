# Casa Pet

Loja virtual da Casa Pet, construída como projeto de aprendizagem guiada e para uso real após a validação do catálogo e do fluxo de pedidos.

O back-end e as páginas do site fazem parte da mesma aplicação Spring Boot. O desenvolvimento local e a produção usarão PostgreSQL; a conexão com o banco será acrescentada na etapa de categorias. Os requisitos e as decisões estão em [`.specs/`](.specs/STATE.md), e o trabalho atual está em [`tasks/`](tasks/todo.md).

## Requisitos de desenvolvimento

- Java 21.
- Node.js e npm para gerar o CSS com Tailwind.
- PostgreSQL quando a etapa de dados começar.

## Executar a versão inicial

```bash
npm install
npm run build:css
./mvnw spring-boot:run
```

Abra `http://localhost:8080/` no navegador.

Em outro terminal, `npm run dev:css` recompila o CSS durante alterações nas páginas. Para verificar a aplicação e gerar o pacote:

```bash
./mvnw test
./mvnw package
```

Esta primeira página apenas confirma que Spring Boot entrega HTML e CSS. Categorias, produtos, carrinho, contas e pedidos serão acrescentados em etapas verificáveis.
