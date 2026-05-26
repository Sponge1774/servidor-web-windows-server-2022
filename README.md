# 🖥️ Servidor WEB para Hospedagem de Site
### Projeto Acadêmico — Server and Data Center Administration
**UNIFECAF — Tecnologia em Análise e Desenvolvimento de Sistemas**

---

## 🏆 Resultado

| Item | Nota | Status |
|---|---|---|
| **Trabalho Prático** | **8 / 8** | ✅ Nota máxima |
| Questionário Unidade 1 | 0,5 / 0,5 | ✅ |
| Questionário Unidade 2 | 0,5 / 0,5 | ✅ |
| Questionário Unidade 3 | 0,5 / 0,5 | ✅ |
| **Nota Final Calculada** | **9,94 / 10** | 🥇 |

> *"Eduardo, sua entrega apresentou um nível técnico extremamente elevado e foi uma das atividades mais completas e profissionais em relação aos requisitos propostos no roteiro da disciplina."*
> — Feedback do Professor

---

## 📋 Descrição do Projeto

Implementação de um servidor web completo para hospedagem de sites, utilizando virtualização com **Microsoft Hyper-V**, **Windows Server 2022**, **IIS**, **PHP via FastCGI** e **MySQL 8.0**, simulando um ambiente real de produção corporativa.

O projeto inclui uma aplicação PHP funcional de **Cadastro de Estoque de Supermercado** com operações CRUD completas integradas ao banco de dados MySQL.

---

## 🏗️ Arquitetura do Ambiente

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

## 🛠️ Tecnologias Utilizadas

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

## 📁 Estrutura do Repositório

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

## 🚀 Como Reproduzir o Ambiente

### Pré-requisitos

- Windows 10 ou 11 **Pro/Enterprise/Education** (o Home não possui Hyper-V)
- Processador com Intel VT-x ou AMD-V habilitado na BIOS
- Mínimo 8 GB RAM (recomendado 12 GB)
- ISO do [Windows Server 2022 Evaluation](https://www.microsoft.com/evalcenter/evaluate-windows-server-2022) (gratuita, 180 dias)

### Passo 1 — Habilitar o Hyper-V

```
Painel de Controle → Programas → Ativar ou desativar recursos do Windows
→ Marcar: Hyper-V (Plataforma + Ferramentas de Gerenciamento)
→ OK → Reiniciar
```

### Passo 2 — Criar Switch Virtual Externo

```
Gerenciador do Hyper-V → Gerenciador de Switch Virtual
→ Novo → Externo → Associar ao adaptador de rede ativo → OK
```

### Passo 3 — Criar a Máquina Virtual

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

### Passo 4 — Instalar o Windows Server 2022

- Edição: **Windows Server 2022 Standard (Desktop Experience)**
- Tipo: **Instalação Personalizada** → Drive 0
- Definir senha forte para o Administrator
- Primeiro login: `Ctrl + Alt + End`

### Passo 5 — Instalar o IIS

```
Server Manager → Gerenciar → Adicionar Funções e Recursos
→ Servidor Web (IIS) → incluir CGI → Instalar
```

### Passo 6 — Instalar e Configurar o PHP

```bash
# 1. Baixar PHP Thread Safe x64 em windows.php.net/download
# 2. Extrair para C:\php
# 3. No IIS Manager → Handler Mappings → Adicionar Mapeamento de Módulo:
#    Caminho: *.php | Módulo: FastCgiModule | Executável: C:\php\php-cgi.exe
# 4. Instalar Microsoft Visual C++ 2015-2022 Redistributable (x64)
# 5. Atribuir permissões "Leitura e Execução" ao grupo IIS_IUSRS em C:\php
```

### Passo 7 — Configurar o php.ini

```ini
; Descomentar as seguintes linhas em C:\php\php.ini:
extension_dir = "ext"
extension=mysqli
```

```bash
# Reiniciar o IIS após salvar:
iisreset
```

### Passo 8 — Instalar o MySQL

```
# Baixar MySQL Installer em dev.mysql.com/downloads
# Tipo: Server only
# Porta: 3306
# Executar iisreset após a instalação
```

### Passo 9 — Publicar a Aplicação

```bash
# Copiar index.php para C:\inetpub\wwwroot\
# Acessar http://localhost no navegador da VM
```

### Passo 10 — Configurar o Firewall

```
Firewall do Windows com Segurança Avançada
→ Regras de Entrada → Nova Regra → Porta → TCP → 80
→ Permitir a conexão → Todos os perfis → Nome: "IIS HTTP Porta 80"
```

---

## 💻 Aplicação — Cadastro de Estoque

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

## 🗄️ Banco de Dados

### Banco atual — `estoque_supermercado`

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

### Evolução futura — `ciclo_vendas_supermercado`

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

## 🔒 Segurança Implementada

- ✅ Firewall configurado — apenas porta 80 (HTTP) aberta
- ✅ Isolamento total da VM pelo Hyper-V
- ✅ Senha forte para o usuário Administrator
- ✅ Permissões mínimas para IIS_IUSRS em `C:\php` e `wwwroot`
- ✅ MySQL acessível apenas localmente (127.0.0.1)
- ✅ Windows Server e Windows 11 atualizados via Windows Update
- 🔜 Evolução futura: HTTPS com certificado SSL/TLS

---

## 📸 Evidências do Ambiente

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

## 📚 Referências Bibliográficas

- SANTANA, W. J. G. S.; AGUIAR, D. A. **Virtualização de data centers e o seu potencial produtivo.** Núcleo do Conhecimento, v. 03, pp. 05-15, jan. 2023.
- PARKUTS, E.; DUFECH, S. M.; ORLOVSKI, R. **Virtualização — Conceitos e Aplicações.** Faculdade Guairacá, 2013.
- CARDOSO, L. P. **Migração de Máquinas Virtuais para Economia de Energia.** UFRJ, 2014.
- POPEK, G.; GOLDBERG, R. Formal requirements for virtualizable third generation architectures. **Communications of the ACM**, v. 17, n. 7, 1974.
- MICROSOFT. **Windows Server 2022 Evaluation Center.** microsoft.com/evalcenter
- MICROSOFT. **IIS — Configuração do FastCGI para PHP.** docs.microsoft.com/iis
- PHP GROUP. **PHP Manual — Instalação no Windows.** php.net

---

## 👨‍💻 Autor

**Eduardo Souza Mattos**
Curso de Tecnologia em Análise e Desenvolvimento de Sistemas
UNIFECAF — São Paulo, SP

---

## 📄 Licença

Este projeto foi desenvolvido para fins acadêmicos.
O código da aplicação está disponível para uso educacional.

---

*Projeto desenvolvido em maio de 2026 — Disciplina Server and Data Center Administration — UNIFECAF*
