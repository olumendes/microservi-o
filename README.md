# Documentação do Microserviço de Pedidos

Este diretório contém os documentos solicitados para o microserviço de Pedidos.

- Arquivos incluídos:
  - `README.md` (este arquivo)
  - `swagger.yaml` (OpenAPI / Swagger em YAML com os endpoints implementados)

## Resumo do serviço

O microserviço de Pedidos é construído sobre `json-server` (arquivo `server.js`) e serve:

- Endpoints customizados:
  - `POST /receive-order` — receber pedidos via JSON
  - `GET /receive-order` — receber pedidos via querystring (redireciona para UI)
  - `GET /current-order` — endpoint consumido pelo front-end para obter o último pedido recebido (consumível uma vez)
- Endpoints padrões do `json-server` para `pedidos` (CRUD):
  - `GET /pedidos`, `POST /pedidos`, `GET /pedidos/{id}`, `PUT /pedidos/{id}`, `DELETE /pedidos/{id}`

O front-end está em `public/` (principalmente `public/app.js`) e faz polling em `/current-order` a cada ~1.5s para automatizar a criação de pedidos recebidos pela rede.

## Como testar localmente

1. Inicie o servidor no diretório do projeto:
```bash
node server.js
```

2. Abra a UI no navegador (na máquina da rede):
```text
http://<IP_DO_SERVIDOR>:3002/
```

3. Simular envio de pedido (exemplo via `curl` a partir de outra máquina):
```bash
curl -X POST http://<IP_DO_SERVIDOR>:3002/receive-order \
  -H "Content-Type: application/json" \
  -d '{"cliente":5,"prato":"Pizza","valor":45.9,"data":"2026-07-01","pagamentoUrl":"http://<IP_PAGTO>:3003/pagamento"}'
```

4. Verifique que o pedido foi criado em `db.json` ou na UI em `http://<IP_DO_SERVIDOR>:3002/pedidos`.

## Como subir para o GitHub (passos sugeridos para cada grupo)

1. Inicialize ou vincule o repositório local a um remoto no GitHub.
```bash
git init
git add .
git commit -m "Adicionar microserviço de pedidos e documentação"
git branch -M main
git remote add origin https://github.com/<SEU_ORG_OU_USUARIO>/<SEU_REPO>.git
git push -u origin main
```

2. Garanta que `README.md` e `swagger.yaml` estejam no diretório `# Documentação do Microserviço Implementado` antes de commitar.

## Observações

- Template de README e Swagger: a turma possui templates no Notion; adapte os campos de `info` do `swagger.yaml` conforme o template se necessário.
- Se quiser, eu posso criar um PR com esses arquivos ou adaptar o conteúdo ao template específico do Notion — me envie o template ou um link.
