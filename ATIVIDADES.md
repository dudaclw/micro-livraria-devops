# Atividades Práticas — Resultados

Resumo do que foi feito nas duas tarefas do roteiro de microsserviços.

## Tarefa 1: Buscar produto por ID

Criei uma rota nova para buscar um livro pelo ID.

**Arquivos alterados:**

-   `proto/inventory.proto`
-   `services/inventory/index.js`
-   `services/controller/index.js`

**Teste:**

```bash
curl http://localhost:3000/product/1
```

**Resultado:**

```json
{
    "id": 1,
    "name": "Refactoring",
    "quantity": 10,
    "price": 79.92,
    "photo": "/img/refactoring.png",
    "author": "Martin Fowler"
}
```

Funcionou. ✅

## Tarefa 2: Container Docker do Shipping

Criei um Dockerfile para rodar o serviço de frete dentro de um container.

**Arquivo criado:** `shipping.Dockerfile`

**Arquivo alterado:** `package.json` (tirei o shipping do comando `npm run start`, já que ele passa a rodar via Docker)

**Teste:**

```bash
docker build -t micro-livraria/shipping -f shipping.Dockerfile ./
docker run -d --name shipping -p 3001:3001 micro-livraria/shipping
```

**Resultado:**

```
Shipping Service running at http://127.0.0.1:3001
```

O Controller conseguiu calcular o frete normalmente, chamando o serviço dentro do container:

```bash
curl http://localhost:3000/shipping/30130000
```

```json
{ "cep": "30130000", "value": 10.51 }
```

Funcionou. ✅

## Resumo

| Tarefa                       | Status |
| ----------------------------- | ------ |
| Buscar produto por ID         | ✅     |
| Container Docker do Shipping  | ✅     |

Tudo testado localmente e funcionando.
