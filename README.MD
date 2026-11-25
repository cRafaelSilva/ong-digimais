# Ong-DigiMais

Sistema web e API REST para gestão de doações, doadores e catálogo de itens da ONG **Ong-DigiMais**.  
Projeto Integrador Extensionista II · Análise e Desenvolvimento de Sistemas (ADS).

## Tecnologias

- **Frontend:** Vite+ (Vanilla JS)
- **Backend:** Node.js + Express
- **Banco de Dados:** MySQL 8 (`mysql2`)

## Requisitos

- Git
- [Vite+](https://viteplus.dev) (comando `vp`)
- MySQL 8 (via Docker, XAMPP ou instalação local)

## Como rodar

1. Clone o repositório e entre na pasta:

```bash
git clone https://github.com/cRafaelSilva/ong-digimais
cd ong-digimais
```

2. Instale as dependências:

```bash
vp install
```

3. Configure as variáveis de ambiente:
   - Copie `.env.example` para `.env` e preencha `DB_USER`, `DB_PASSWORD` e `DB_NAME=ongdigimais`.

4. Crie e popule o banco de dados:
   - Com o MySQL rodando (porta `3306`), execute `database/schema.sql` e depois `database/seed.sql`.
   - Exemplo usando Docker:

```bash
docker run --name mysql-ongdigimais -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mysql:8
docker exec -i mysql-ongdigimais mysql -u root -proot < database/schema.sql
docker exec -i mysql-ongdigimais mysql -u root -proot < database/seed.sql
```

5. Inicie os servidores em dois terminais:
   - **Terminal 1 (API):** `vp run api`
   - **Terminal 2 (Frontend):** `vp dev`

6. Acesse no navegador:
   - **Frontend:** `http://localhost:5173`
   - **Health check (API + Banco):** `http://localhost:3000/api/health`

## Rotas principais da API

| Método | Rota | Descrição |
| --- | --- | --- |
| `GET` | `/api/health` | Verifica status da API e conexão com o banco |
| `GET` | `/api/doadores` | Lista todos os doadores |
| `GET` | `/api/doadores/:id` | Busca um doador por ID |
| `POST` | `/api/doadores` | Cadastra um novo doador |
| `PUT` | `/api/doadores/:id` | Atualiza dados de um doador |
| `DELETE` | `/api/doadores/:id` | Remove um doador (sem doações vinculadas) |
| `GET` | `/api/itens` | Lista o catálogo de itens com categoria |
| `GET` | `/api/doacoes` | Lista doações com doador e itens agrupados |
| `POST` | `/api/doacoes` | Registra uma doação com itens (em transação) |