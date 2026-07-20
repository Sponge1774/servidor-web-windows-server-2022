# 🖥️ Servidor WEB para Hospedagem de Site | Web Server for Website Hosting
### Projeto Acadêmico — Server and Data Center Administration | Academic Project — Server and Data Center Administration
**UNIFECAF — Tecnologia em Análise e Desenvolvimento de Sistemas | Technology in Systems Analysis and Development**

---

🌐 **Idioma / Language:** [Português](#-português) | [English](#-english)

---

## 🇧🇷 Português

### 🏆 Resultado

| Item | Nota | Status |
|---|---|---|
| **Trabalho Prático** | **8 / 8** | ✅ Nota máxima |
| Questionário Unidade 1 | 0,5 / 0,5 | ✅ |
| Questionário Unidade 2 | 0,5 / 0,5 | ✅ |
| Questionário Unidade 3 | 0,5 / 0,5 | ✅ |
| Questionário Unidade 4 | 0,44 / 0,5 | ✅ |
| **Nota Final Calculada** | **9,94 / 10** | 🥇 |

> *"Eduardo, sua entrega apresentou um nível técnico extremamente elevado e foi uma das atividades mais completas e profissionais em relação aos requisitos propostos no roteiro da disciplina."*
> — Feedback do Professor

---

### 📋 Descrição do Projeto

Implementação de um servidor web completo para hospedagem de sites, utilizando virtualização com **Microsoft Hyper-V**, **Windows Server 2022**, **IIS**, **PHP via FastCGI** e **MySQL 8.0**, simulando um ambiente real de produção corporativa.

O projeto inclui uma aplicação PHP funcional de **Cadastro de Estoque de Supermercado** com operações CRUD completas integradas ao banco de dados MySQL.

---

### 🏗️ Arquitetura do Ambiente

```
Notebook Samsung Expert (2018)
├── Intel Core i7-8550U @ 1.80GHz
├── 12 GB RAM DDR4
├── 224 GB SSD SATA
└── Windows 11 Pro (versão 25H2 — build 26200.8328)
    │
    └── Microsoft Hyper-V (hipervisor nativo bare-metal)
        │
        └── VM: Windows_Server_2022_Estudo
            ├── Geração 2 | 4 GB RAM (dinâmica) | VHDX 60 GB
            ├── Criada em: 01/05/2026
            │
            ├── IIS — Internet Information Services
            │   └── PHP 8.x via FastCGI (php-cgi.exe)
            │       └── Driver MySQLi (extension=mysqli)
            │
            └── MySQL Server 8.0.46
                └── Banco: estoque_supermercado
                    └── Tabela: produtos (id, nome, quantidade, preco)
```

---

### 🛠️ Tecnologias Utilizadas

| Tecnologia | Versão | Função |
|---|---|---|
| Windows 11 Pro | 25H2 (26200.8328) | Sistema operacional host |
| Microsoft Hyper-V | Versão config. 12.0 | Hipervisor (bare-metal) |
| Windows Server 2022 | Standard Evaluation | Sistema operacional da VM |
| IIS | Incluído no WS2022 | Servidor web |
| PHP | 8.x Thread Safe x64 | Interpretador backend |
| FastCGI | Nativo no IIS | Protocolo de integração PHP-IIS |
| MySQL Server | 8.0.46 | Banco de dados relacional |
| Microsoft Visual C++ | 2015-2022 Redistributable x64 | Dependência do PHP |

---

### 📁 Estrutura do Repositório

```
📦 servidor-web-unifecaf/
├── 📄 README.md
├── 📂 app/
│   └── 📄 index.php              # Aplicação de Cadastro de Estoque
├── 📂 database/
│   ├── 📄 estoque_supermercado.sql    # Banco simples (usado no projeto)
│   └── 📄 ciclo_vendas_supermercado.sql  # Script avançado (evolução futura)
├── 📂 docs/
│   ├── 📄 Relatorio_Teorico.pdf       # Parte teórica (25% da nota)
│   ├── 📄 Relatorio_Pratico.pdf       # Parte prática (50% da nota)
│   └── 📄 Script_Video_Pitch.pdf      # Script do vídeo (25% da nota)
└── 📂 screenshots/
    ├── 🖼️ windows11-sobre.png
    ├── 🖼️ hyperv-vm-executando.png
    ├── 🖼️ server-manager-dashboard.png
    ├── 🖼️ iis-handler-mappings.png
    ├── 🖼️ php-ini-mysqli.png
    ├── 🖼️ permissoes-pasta-php.png
    ├── 🖼️ visualc-mysql-instalados.png
    └── 🖼️ localhost-aplicacao.png
```

---

### 🚀 Como Reproduzir o Ambiente

#### Pré-requisitos

- Windows 10 ou 11 **Pro/Enterprise/Education** (o Home não possui Hyper-V)
- Processador com Intel VT-x ou AMD-V habilitado na BIOS
- Mínimo 8 GB RAM (recomendado 12 GB)
- ISO do [Windows Server 2022 Evaluation](https://www.microsoft.com/evalcenter/evaluate-windows-server-2022) (gratuita, 180 dias)

#### Passo 1 — Habilitar o Hyper-V

```
Painel de Controle → Programas → Ativar ou desativar recursos do Windows
→ Marcar: Hyper-V (Plataforma + Ferramentas de Gerenciamento)
→ OK → Reiniciar
```

#### Passo 2 — Criar Switch Virtual Externo

```
Gerenciador do Hyper-V → Gerenciador de Switch Virtual
→ Novo → Externo → Associar ao adaptador de rede ativo → OK
```

#### Passo 3 — Criar a Máquina Virtual

| Campo | Valor |
|---|---|
| Nome | Windows_Server_2022_Estudo |
| Geração | **Geração 2** |
| RAM | 4096 MB (dinâmica) |
| Rede | Switch Externo |
| Disco VHDX | 60 GB |
| ISO | Windows Server 2022 Evaluation |

> ⚠️ **Importante:** desabilitar o Secure Boot antes de iniciar a VM:
> Configurações da VM → Segurança → Firmware → desmarcar "Habilitar Inicialização Segura"

#### Passo 4 — Instalar o Windows Server 2022

- Edição: **Windows Server 2022 Standard (Desktop Experience)**
- Tipo: **Instalação Personalizada** → Drive 0
- Definir senha forte para o Administrator
- Primeiro login: `Ctrl + Alt + End`

#### Passo 5 — Instalar o IIS

```
Server Manager → Gerenciar → Adicionar Funções e Recursos
→ Servidor Web (IIS) → incluir CGI → Instalar
```

#### Passo 6 — Instalar e Configurar o PHP

```bash
# 1. Baixar PHP Thread Safe x64 em windows.php.net/download
# 2. Extrair para C:\php
# 3. No IIS Manager → Handler Mappings → Adicionar Mapeamento de Módulo:
#    Caminho: *.php | Módulo: FastCgiModule | Executável: C:\php\php-cgi.exe
# 4. Instalar Microsoft Visual C++ 2015-2022 Redistributable (x64)
# 5. Atribuir permissões "Leitura e Execução" ao grupo IIS_IUSRS em C:\php
```

#### Passo 7 — Configurar o php.ini

```ini
; Descomentar as seguintes linhas em C:\php\php.ini:
extension_dir = "ext"
extension=mysqli
```

```bash
# Reiniciar o IIS após salvar:
iisreset
```

#### Passo 8 — Instalar o MySQL

```
# Baixar MySQL Installer em dev.mysql.com/downloads
# Tipo: Server only
# Porta: 3306
# Executar iisreset após a instalação
```

#### Passo 9 — Publicar a Aplicação

```bash
# Copiar index.php para C:\inetpub\wwwroot\
# Acessar http://localhost no navegador da VM
```

#### Passo 10 — Configurar o Firewall

```
Firewall do Windows com Segurança Avançada
→ Regras de Entrada → Nova Regra → Porta → TCP → 80
→ Permitir a conexão → Todos os perfis → Nome: "IIS HTTP Porta 80"
```

---

### 💻 Aplicação — Cadastro de Estoque

A aplicação `index.php` implementa um sistema completo de gestão de estoque:

- ✅ Conexão MySQL com tratamento correto de caracteres especiais na senha
- ✅ Criação automática do banco e tabela se não existirem
- ✅ Formulário HTML para cadastro de produtos
- ✅ Listagem em tempo real dos produtos cadastrados
- ✅ Operações CRUD via `mysqli` com prepared statements

> ⚠️ **Atenção PHP:** senhas com o caractere `$` devem usar **aspas simples** na string de conexão para evitar interpretação como variável PHP:
> ```php
> // ❌ Errado — $ interpretado como variável
> $pass = "Senha$Forte";
>
> // ✅ Correto — lido como texto literal
> $pass = 'Senha$Forte';
> ```

---

### 🗄️ Banco de Dados

#### Banco atual — `estoque_supermercado`

```sql
CREATE DATABASE estoque_supermercado;
USE estoque_supermercado;

CREATE TABLE produtos (
  id         INT AUTO_INCREMENT PRIMARY KEY,
  nome       VARCHAR(100) NOT NULL,
  quantidade INT NOT NULL,
  preco      DECIMAL(10,2) NOT NULL
);
```

#### Evolução futura — `ciclo_vendas_supermercado`

Script SQL avançado com **16 tabelas** modelando o ciclo completo de vendas:

| Grupo | Tabelas |
|---|---|
| Principais | clientes, lojas, fornecedores, produtos, colaboradores, vendas, programa_fidelidade |
| Contato | clientes_telefone, clientes_email |
| Endereço | clientes_endereco, lojas_endereco, fornecedores_endereco |
| Ligação N:N | cadastro_fidelidade, fornecedores_produtos, item_venda |
| Pagamento | forma_pagamento |

Destaques técnicos do script avançado:
- **PK Composta** em tabelas N:N (sem coluna `id` extra)
- **DECIMAL(10,2)** para valores monetários
- **CHAR(11/14)** para CPF e CNPJ de tamanho fixo
- **DATE/DATETIME** para campos de data
- **ENGINE=InnoDB** com suporte a transações
- **UNIQUE KEY** em CPF, CNPJ e e-mail
- **FOREIGN KEY** com integridade referencial completa

---

### 🔒 Segurança Implementada

- ✅ Firewall configurado — apenas porta 80 (HTTP) aberta
- ✅ Isolamento total da VM pelo Hyper-V
- ✅ Senha forte para o usuário Administrator
- ✅ Permissões mínimas para IIS_IUSRS em `C:\php` e `wwwroot`
- ✅ MySQL acessível apenas localmente (127.0.0.1)
- ✅ Windows Server e Windows 11 atualizados via Windows Update
- 🔜 Evolução futura: HTTPS com certificado SSL/TLS

---

### 📸 Evidências do Ambiente

| Screenshot | Descrição |
|---|---|
| `windows11-sobre.png` | Hardware real: i7-8550U, 12GB RAM, Win11 Pro 25H2 |
| `hyperv-vm-executando.png` | VM executando: 3432MB RAM, Geração 2 |
| `server-manager-dashboard.png` | IIS instalado, Roles: 2, status verde |
| `iis-handler-mappings.png` | PHP_via_FastCGI habilitado para *.php |
| `php-ini-mysqli.png` | extension=mysqli ativa no php.ini |
| `permissoes-pasta-php.png` | IIS_IUSRS configurado em C:\php |
| `visualc-mysql-instalados.png` | VC++ 14.44.35211.0 e MySQL 8.0.46 |
| `localhost-aplicacao.png` | Sistema funcionando com dados no MySQL |

---

### 📚 Referências Bibliográficas

- SANTANA, W. J. G. S.; AGUIAR, D. A. **Virtualização de data centers e o seu potencial produtivo.** Núcleo do Conhecimento, v. 03, pp. 05-15, jan. 2023.
- PARKUTS, E.; DUFECH, S. M.; ORLOVSKI, R. **Virtualização — Conceitos e Aplicações.** Faculdade Guairacá, 2013.
- CARDOSO, L. P. **Migração de Máquinas Virtuais para Economia de Energia.** UFRJ, 2014.
- POPEK, G.; GOLDBERG, R. Formal requirements for virtualizable third generation architectures. **Communications of the ACM**, v. 17, n. 7, 1974.
- MICROSOFT. **Windows Server 2022 Evaluation Center.** microsoft.com/evalcenter
- MICROSOFT. **IIS — Configuração do FastCGI para PHP.** docs.microsoft.com/iis
- PHP GROUP. **PHP Manual — Instalação no Windows.** php.net

---

### 👨‍💻 Autor

**Eduardo Souza Mattos**
Curso de Tecnologia em Análise e Desenvolvimento de Sistemas
UNIFECAF — São Paulo, SP

---

### 📄 Licença

Este projeto foi desenvolvido para fins acadêmicos.
O código da aplicação está disponível para uso educacional.

---

*Projeto desenvolvido em maio de 2026 — Disciplina Server and Data Center Administration — UNIFECAF*

<br>

[⬆ Voltar ao topo](#-servidor-web-para-hospedagem-de-site--web-server-for-website-hosting)

---
---

## 🇬🇧 English

### 🏆 Result

| Item | Grade | Status |
|---|---|---|
| **Practical Assignment** | **8 / 8** | ✅ Maximum grade |
| Unit 1 Quiz | 0.5 / 0.5 | ✅ |
| Unit 2 Quiz | 0.5 / 0.5 | ✅ |
| Unit 3 Quiz | 0.5 / 0.5 | ✅ |
| Unit 4 Quiz | 0.44 / 0.5 | ✅ |
| **Calculated Final Grade** | **9.94 / 10** | 🥇 |

> *"Eduardo, your submission showed an extremely high technical level and was one of the most complete and professional assignments in relation to the requirements proposed in the course guide."*
> — Instructor Feedback

---

### 📋 Project Description

Implementation of a complete web server for website hosting, using virtualization with **Microsoft Hyper-V**, **Windows Server 2022**, **IIS**, **PHP via FastCGI**, and **MySQL 8.0**, simulating a real corporate production environment.

The project includes a functional PHP application for **Supermarket Inventory Management** with full CRUD operations integrated with the MySQL database.

---

### 🏗️ Environment Architecture

```
Samsung Expert Notebook (2018)
├── Intel Core i7-8550U @ 1.80GHz
├── 12 GB DDR4 RAM
├── 224 GB SATA SSD
└── Windows 11 Pro (version 25H2 — build 26200.8328)
    │
    └── Microsoft Hyper-V (native bare-metal hypervisor)
        │
        └── VM: Windows_Server_2022_Estudo
            ├── Generation 2 | 4 GB RAM (dynamic) | 60 GB VHDX
            ├── Created on: 05/01/2026
            │
            ├── IIS — Internet Information Services
            │   └── PHP 8.x via FastCGI (php-cgi.exe)
            │       └── MySQLi driver (extension=mysqli)
            │
            └── MySQL Server 8.0.46
                └── Database: estoque_supermercado
                    └── Table: produtos (id, nome, quantidade, preco)
```

---

### 🛠️ Technologies Used

| Technology | Version | Function |
|---|---|---|
| Windows 11 Pro | 25H2 (26200.8328) | Host operating system |
| Microsoft Hyper-V | Config version 12.0 | Hypervisor (bare-metal) |
| Windows Server 2022 | Standard Evaluation | VM operating system |
| IIS | Included in WS2022 | Web server |
| PHP | 8.x Thread Safe x64 | Backend interpreter |
| FastCGI | Native in IIS | PHP-IIS integration protocol |
| MySQL Server | 8.0.46 | Relational database |
| Microsoft Visual C++ | 2015-2022 Redistributable x64 | PHP dependency |

---

### 📁 Repository Structure

```
📦 servidor-web-unifecaf/
├── 📄 README.md
├── 📂 app/
│   └── 📄 index.php              # Inventory management application
├── 📂 database/
│   ├── 📄 estoque_supermercado.sql    # Simple database (used in the project)
│   └── 📄 ciclo_vendas_supermercado.sql  # Advanced script (future evolution)
├── 📂 docs/
│   ├── 📄 Relatorio_Teorico.pdf       # Theoretical part (25% of the grade)
│   ├── 📄 Relatorio_Pratico.pdf       # Practical part (50% of the grade)
│   └── 📄 Script_Video_Pitch.pdf      # Video pitch script (25% of the grade)
└── 📂 screenshots/
    ├── 🖼️ windows11-sobre.png
    ├── 🖼️ hyperv-vm-executando.png
    ├── 🖼️ server-manager-dashboard.png
    ├── 🖼️ iis-handler-mappings.png
    ├── 🖼️ php-ini-mysqli.png
    ├── 🖼️ permissoes-pasta-php.png
    ├── 🖼️ visualc-mysql-instalados.png
    └── 🖼️ localhost-aplicacao.png
```

---

### 🚀 How to Reproduce the Environment

#### Prerequisites

- Windows 10 or 11 **Pro/Enterprise/Education** (Home edition does not include Hyper-V)
- Processor with Intel VT-x or AMD-V enabled in the BIOS
- Minimum 8 GB RAM (12 GB recommended)
- [Windows Server 2022 Evaluation](https://www.microsoft.com/evalcenter/evaluate-windows-server-2022) ISO (free, 180 days)

#### Step 1 — Enable Hyper-V

```
Control Panel → Programs → Turn Windows features on or off
→ Check: Hyper-V (Platform + Management Tools)
→ OK → Restart
```

#### Step 2 — Create an External Virtual Switch

```
Hyper-V Manager → Virtual Switch Manager
→ New → External → Associate with the active network adapter → OK
```

#### Step 3 — Create the Virtual Machine

| Field | Value |
|---|---|
| Name | Windows_Server_2022_Estudo |
| Generation | **Generation 2** |
| RAM | 4096 MB (dynamic) |
| Network | External Switch |
| VHDX Disk | 60 GB |
| ISO | Windows Server 2022 Evaluation |

> ⚠️ **Important:** disable Secure Boot before starting the VM:
> VM Settings → Security → Firmware → uncheck "Enable Secure Boot"

#### Step 4 — Install Windows Server 2022

- Edition: **Windows Server 2022 Standard (Desktop Experience)**
- Type: **Custom Installation** → Drive 0
- Set a strong password for the Administrator account
- First login: `Ctrl + Alt + End`

#### Step 5 — Install IIS

```
Server Manager → Manage → Add Roles and Features
→ Web Server (IIS) → include CGI → Install
```

#### Step 6 — Install and Configure PHP

```bash
# 1. Download PHP Thread Safe x64 from windows.php.net/download
# 2. Extract to C:\php
# 3. In IIS Manager → Handler Mappings → Add Module Mapping:
#    Path: *.php | Module: FastCgiModule | Executable: C:\php\php-cgi.exe
# 4. Install Microsoft Visual C++ 2015-2022 Redistributable (x64)
# 5. Grant "Read & Execute" permissions to the IIS_IUSRS group on C:\php
```

#### Step 7 — Configure php.ini

```ini
; Uncomment the following lines in C:\php\php.ini:
extension_dir = "ext"
extension=mysqli
```

```bash
# Restart IIS after saving:
iisreset
```

#### Step 8 — Install MySQL

```
# Download MySQL Installer from dev.mysql.com/downloads
# Type: Server only
# Port: 3306
# Run iisreset after installation
```

#### Step 9 — Publish the Application

```bash
# Copy index.php to C:\inetpub\wwwroot\
# Access http://localhost in the VM's browser
```

#### Step 10 — Configure the Firewall

```
Windows Firewall with Advanced Security
→ Inbound Rules → New Rule → Port → TCP → 80
→ Allow the connection → All profiles → Name: "IIS HTTP Port 80"
```

---

### 💻 Application — Inventory Management

The `index.php` application implements a complete inventory management system:

- ✅ MySQL connection with correct handling of special characters in the password
- ✅ Automatic creation of the database and table if they don't exist
- ✅ HTML form for product registration
- ✅ Real-time listing of registered products
- ✅ CRUD operations via `mysqli` with prepared statements

> ⚠️ **PHP note:** passwords containing the `$` character must use **single quotes** in the connection string to avoid being interpreted as a PHP variable:
> ```php
> // ❌ Wrong — $ interpreted as a variable
> $pass = "Senha$Forte";
>
> // ✅ Correct — read as literal text
> $pass = 'Senha$Forte';
> ```

---

### 🗄️ Database

#### Current database — `estoque_supermercado`

```sql
CREATE DATABASE estoque_supermercado;
USE estoque_supermercado;

CREATE TABLE produtos (
  id         INT AUTO_INCREMENT PRIMARY KEY,
  nome       VARCHAR(100) NOT NULL,
  quantidade INT NOT NULL,
  preco      DECIMAL(10,2) NOT NULL
);
```

#### Future evolution — `ciclo_vendas_supermercado`

Advanced SQL script with **16 tables** modeling the complete sales cycle:

| Group | Tables |
|---|---|
| Core | clientes, lojas, fornecedores, produtos, colaboradores, vendas, programa_fidelidade |
| Contact | clientes_telefone, clientes_email |
| Address | clientes_endereco, lojas_endereco, fornecedores_endereco |
| N:N Relationships | cadastro_fidelidade, fornecedores_produtos, item_venda |
| Payment | forma_pagamento |

Technical highlights of the advanced script:
- **Composite PK** in N:N tables (no extra `id` column)
- **DECIMAL(10,2)** for monetary values
- **CHAR(11/14)** for fixed-length CPF and CNPJ (Brazilian tax IDs)
- **DATE/DATETIME** for date fields
- **ENGINE=InnoDB** with transaction support
- **UNIQUE KEY** on CPF, CNPJ, and email
- **FOREIGN KEY** with full referential integrity

---

### 🔒 Security Implemented

- ✅ Firewall configured — only port 80 (HTTP) open
- ✅ Full VM isolation via Hyper-V
- ✅ Strong password for the Administrator account
- ✅ Minimal permissions for IIS_IUSRS on `C:\php` and `wwwroot`
- ✅ MySQL accessible only locally (127.0.0.1)
- ✅ Windows Server and Windows 11 updated via Windows Update
- 🔜 Future evolution: HTTPS with SSL/TLS certificate

---

### 📸 Environment Evidence

| Screenshot | Description |
|---|---|
| `windows11-sobre.png` | Real hardware: i7-8550U, 12GB RAM, Win11 Pro 25H2 |
| `hyperv-vm-executando.png` | VM running: 3432MB RAM, Generation 2 |
| `server-manager-dashboard.png` | IIS installed, Roles: 2, green status |
| `iis-handler-mappings.png` | PHP via FastCGI enabled for *.php |
| `php-ini-mysqli.png` | extension=mysqli active in php.ini |
| `permissoes-pasta-php.png` | IIS_IUSRS configured on C:\php |
| `visualc-mysql-instalados.png` | VC++ 14.44.35211.0 and MySQL 8.0.46 |
| `localhost-aplicacao.png` | System working with data in MySQL |

---

### 📚 References

- SANTANA, W. J. G. S.; AGUIAR, D. A. **Data center virtualization and its productive potential.** Núcleo do Conhecimento, v. 03, pp. 05-15, Jan. 2023.
- PARKUTS, E.; DUFECH, S. M.; ORLOVSKI, R. **Virtualization — Concepts and Applications.** Faculdade Guairacá, 2013.
- CARDOSO, L. P. **Migration of Virtual Machines for Energy Savings.** UFRJ, 2014.
- POPEK, G.; GOLDBERG, R. Formal requirements for virtualizable third generation architectures. **Communications of the ACM**, v. 17, n. 7, 1974.
- MICROSOFT. **Windows Server 2022 Evaluation Center.** microsoft.com/evalcenter
- MICROSOFT. **IIS — FastCGI Configuration for PHP.** docs.microsoft.com/iis
- PHP GROUP. **PHP Manual — Installation on Windows.** php.net

---

### 👨‍💻 Author

**Eduardo Souza Mattos**
Technology in Systems Analysis and Development
UNIFECAF — São Paulo, SP, Brazil

---

### 📄 License

This project was developed for academic purposes.
The application code is available for educational use.

---

*Project developed in May 2026 — Server and Data Center Administration course — UNIFECAF*

<br>

[⬆ Back to top](#-servidor-web-para-hospedagem-de-site--web-server-for-website-hosting)
