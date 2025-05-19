---
Data: 12-05-2025
tags:
---
# 🐬 Guia Básico de MariaDB – Instalação e Configuração Inicial

Este guia mostra os passos básicos para instalar, proteger e configurar uma base de dados MariaDB no Debian, com base nas ações executadas na imagem fornecida.

---

## 📦 Passo 1 – Instalar o MariaDB

```bash
sudo apt install mariadb-server
```

---

## 🔒 Passo 2 – Proteger a instalação

Executa o script de segurança:

```bash
sudo mysql_secure_installation
```

Durante este processo:

- Proibiste o login remoto como `root`: **(y)**
    
- Removeste a base de dados de teste: **(y)**
    
- Recarregaste as tabelas de privilégios: **(y)**
    

Resultado final: instalação segura concluída ✅

---

## 🧑‍💻 Passo 3 – Aceder ao MariaDB

```bash
sudo mariadb
```

Este comando abre o cliente MariaDB no terminal.

---

## 🛠️ Passo 4 – Criar base de dados e utilizador

### Criar base de dados

```sql
CREATE DATABASE brunnigu;
```

### Criar utilizador com permissões completas

```sql
GRANT ALL ON brunnigu.* TO 'brunnigu'@'localhost' IDENTIFIED BY '5ee0Vwf84B' WITH GRANT OPTION;
```

> ⚠️ Substituir a senha por uma segura em ambientes reais!

### Aplicar alterações

```sql
FLUSH PRIVILEGES;
```

### Entrar na base de dados
```shell
mariadb -u $USER -p
```

### Sair do cliente MariaDB

```sql
EXIT;
```

---

## ✅ Resultado

Criaste uma base de dados chamada `brunnigu` e um utilizador `brunnigu` com permissões totais sobre ela.

---

### Criar base de dados
```sql
CREATE DATABASE;
```

## Ver bases de dados 
```sql
SHOW DATABASES;
```