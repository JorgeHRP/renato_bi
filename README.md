# Profecia® Dashboard System

Sistema web para gestão e visualização de dados financeiros por empresa.

---

## Como Rodar

### 1. Instalar dependências
```bash
pip install flask pandas openpyxl werkzeug
```

### 2. Iniciar o servidor
```bash
cd dashboard_app
python app.py
```

### 3. Acessar
Abra no navegador: **http://localhost:5000**

---

## Login Padrão (Admin)

| Campo | Valor |
|-------|-------|
| Usuário | `admin` |
| Senha | `admin123` |

> ⚠️ Troque a senha do admin após o primeiro login (edite o arquivo `data/users.json`).

---

## Estrutura do Sistema

```
dashboard_app/
├── app.py                  # Servidor Flask principal
├── data/
│   ├── users.json          # Usuários (admin + clientes)
│   └── companies.json      # Empresas cadastradas
├── static/
│   └── uploads/            # Arquivos Excel enviados
└── templates/
    ├── base.html           # Layout principal
    ├── login.html          # Tela de login
    ├── admin_dashboard.html
    ├── admin_companies.html
    ├── admin_company_detail.html
    ├── admin_new_company.html
    ├── admin_users.html
    └── client_dashboard.html
```

---

## Fluxo de Uso

### Como Admin:
1. Login com credenciais de admin
2. **Dashboard** → visão geral de empresas
3. **Empresas → Nova Empresa** → preencher nome, CNPJ, criar usuário do cliente
4. **Empresas → [Empresa]** → upload do Excel do cliente
5. O sistema processa automaticamente o arquivo e extrai dados financeiros

### Como Cliente:
1. Login com as credenciais criadas pelo admin
2. Visualiza automaticamente o **Dashboard** da própria empresa com:
   - KPIs financeiros (entradas, saídas, saldo)
   - Gráfico de fluxo mensal (barras)
   - Distribuição de gastos por categoria (rosca)
   - Tabela de transações com filtro e busca

---

## Formatos Excel Suportados

O sistema detecta automaticamente e processa:

- **Financeiro** (formato `Financeiro_2025-2026.xlsx`):
  - Aba `Base` com colunas: Data, Descricao, Categoria, Valor, Tipo, Status
  - Gera: KPIs, gráfico mensal, gráfico por categoria, tabela de transações

- **Profecia** (formato `PROFECIA_*.xlsx`):
  - Aba `DASH` com saldo inicial, geração de caixa, saldo final

---

## Dados em JSON

Os dados ficam em `data/`:
- `users.json` — usuários do sistema
- `companies.json` — empresas cadastradas  
- `company_{id}_data.json` — dados financeiros de cada empresa (extraídos do Excel)

Nenhum banco de dados externo é necessário.
