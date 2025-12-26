# API E-commerce - JSON Server

API REST mockada para projeto de curso Databricks com estrutura Medallion (Bronze, Silver, Gold).

## 📋 Sobre o Projeto

Este é um JSON Server contendo dados de e-commerce estruturados para ser consumido no Databricks Free Edition, processado através da arquitetura Medallion e visualizado no Power BI.

## 🗂️ Estrutura de Dados

A API contém os seguintes endpoints:

### Tabelas Principais
- **categorias** - Categorias de produtos (5 registros)
- **fornecedores** - Fornecedores dos produtos (5 registros)
- **produtos** - Catálogo de produtos (10 registros)
- **clientes** - Base de clientes (8 registros)
- **pedidos** - Pedidos realizados (15 registros)
- **itens_pedido** - Itens de cada pedido (25 registros)
- **cupons** - Cupons de desconto (4 registros)
- **avaliacoes** - Avaliações de produtos (5 registros)

### Campos Enriquecidos

**Produtos:**
- SKU, marca, modelo, cor, tamanho
- Preço de venda e custo
- Controle de estoque (atual e mínimo)
- Dimensões e peso
- Avaliações médias e quantidade
- Datas de criação/atualização

**Pedidos:**
- Status (processando, em_transito, entregue, cancelado)
- Status de pagamento (pendente, pago, estornado)
- Métodos de pagamento (cartao_credito, cartao_debito, pix, boleto)
- Informações de entrega
- Aplicação de cupons de desconto
- Datas previstas e reais de entrega

**Clientes:**
- Informações demográficas completas
- Endereços completos
- Estatísticas de compras

**Itens de Pedido:**
- Quantidades
- Preços unitários
- Descontos por item
- Subtotal calculado

## 🚀 Como Usar

### Instalação Local

```bash
# Instalar dependências
npm install

# Executar em modo desenvolvimento
npm run dev

# Ou usar o servidor padrão
npm start
```

A API estará disponível em: `http://localhost:3000`

### Deploy

#### Vercel

1. Instalar Vercel CLI: `npm i -g vercel`
2. Executar: `vercel`
3. Ou fazer deploy via GitHub/GitLab conectando o repositório

#### Render

1. Conectar repositório no Render
2. O arquivo `render.yaml` já está configurado
3. Deploy automático ao fazer push

## 📡 Endpoints Disponíveis

Todos os endpoints seguem o padrão REST do JSON Server:

```
GET    /categorias          - Lista todas as categorias
GET    /categorias/:id      - Busca categoria por ID
GET    /fornecedores        - Lista todos os fornecedores
GET    /fornecedores/:id    - Busca fornecedor por ID
GET    /produtos            - Lista todos os produtos
GET    /produtos/:id        - Busca produto por ID
GET    /clientes            - Lista todos os clientes
GET    /clientes/:id        - Busca cliente por ID
GET    /pedidos             - Lista todos os pedidos
GET    /pedidos/:id         - Busca pedido por ID
GET    /itens_pedido        - Lista todos os itens
GET    /itens_pedido/:id    - Busca item por ID
GET    /cupons              - Lista todos os cupons
GET    /cupons/:id          - Busca cupom por ID
GET    /avaliacoes          - Lista todas as avaliações
GET    /avaliacoes/:id      - Busca avaliação por ID
```

### Filtros e Buscas

```bash
# Filtrar por campo
GET /produtos?categoria_id=1
GET /pedidos?status=entregue
GET /clientes?status=ativo

# Buscar por texto
GET /produtos?q=smartphone
GET /clientes?nome_like=Ana

# Ordenar
GET /produtos?_sort=preco&_order=desc
GET /pedidos?_sort=data_pedido&_order=desc

# Paginar
GET /produtos?_page=1&_limit=10

# Relacionamentos
GET /pedidos/1?_embed=itens_pedido
GET /produtos/1?_embed=avaliacoes
```

## 🎯 Uso no Databricks

### Estrutura Medallion Proposta

**Bronze Layer (Raw):**
- Ingestão direta da API
- Dados brutos sem transformação
- Preservação completa dos dados originais

**Silver Layer (Cleansed):**
- Limpeza e padronização
- Validações de dados
- Tratamento de nulos e erros
- Normalização de formatos (datas, valores monetários)

**Gold Layer (Business):**
- Modelo dimensional (Dimensões e Fatos)
- Agregações e métricas de negócio
- Preparado para Power BI

### Dimensões Sugeridas
- Dim_Cliente
- Dim_Produto
- Dim_Categoria
- Dim_Fornecedor
- Dim_Data
- Dim_Cupom

### Fatos Sugeridas
- Fato_Vendas (baseada em pedidos e itens_pedido)
- Fato_Estoque (baseada em produtos)

## 📊 Visualização Power BI

Conectar ao Databricks Gold Layer e criar dashboards com:
- Vendas por período, produto, categoria, cliente
- Análise de estoque
- Performance de cupons
- Avaliações de produtos
- Métricas de entrega

## 🔧 Tecnologias

- Node.js
- JSON Server
- Deploy: Vercel / Render

## 📝 Notas

- Este é um projeto de aprendizado
- Dados são mockados e fictícios
- Ideal para demonstrar pipeline de dados end-to-end

