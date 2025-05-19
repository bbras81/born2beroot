---
Data: 18-04-2025
tags:
---
# 📚 Gestão de Utilizadores, Grupos e Sudo no Linux

Este guia reúne os comandos essenciais para gerir utilizadores, grupos e entender a configuração do `sudo` — útil para administradores de sistemas e estudantes de projetos como o **Born2beRoot**.

---

## 🔐 `sudo -V` – Verificar versão e capacidades

### 🔍 Exemplo de saída do comando:

```bash
Sudo version 1.9.5p2
Configure options: --with-password-timeout=0 ...
Sudoers policy plugin version 1.9.5p2
Sudoers file grammar version 46
Sudoers I/O plugin version 1.9.5p2
```

### 📋 O que esta informação inclui:

- **Versão do `sudo` instalada**
    
- **Opções de compilação** (como suporte a plugins de I/O, log, autenticação PAM)
    
- **Versão do ficheiro sudoers e dos plugins**
    
- Diretórios utilizados pelo `sudo`: `sudoers_path`, `plugin_dir`, etc.
    

### 💡 Para que serve?

- Verificar se `sudo` tem suporte a:
    
    - `log_input`, `log_output`
        
    - `requiretty`
        
    - Integração com PAM
        
- Útil para **debug**, **auditorias de segurança** e **avaliações técnicas**.
    

---

## 👥 Utilizadores – Comandos Essenciais

### ➕ Criar novo utilizador

```bash
sudo adduser nome_utilizador
```

Cria utilizador com diretório home, shell e senha.

### 🔐 Alterar senha

```bash
sudo passwd nome_utilizador
```

### ✏️ Modificar utilizador

```bash
sudo usermod -l novo_nome nome_antigo         # Alterar login
sudo usermod -d /novo/home -m nome_utilizador # Alterar diretório home
sudo usermod -s /bin/bash nome_utilizador     # Alterar shell
```

### ❌ Remover utilizador

```bash
sudo deluser nome_utilizador
sudo deluser --remove-home nome_utilizador
```

---

## 👪 Grupos – Comandos Essenciais

### ➕ Criar grupo

```bash
sudo groupadd nome_grupo
```

### ➕ Adicionar utilizador a grupo

```bash
sudo usermod -aG nome_grupo nome_utilizador
```

### 🔍 Ver grupos de um utilizador

```bash
groups nome_utilizador
```

### ❌ Remover utilizador de grupo

```bash
sudo gpasswd -d nome_utilizador nome_grupo
```

### ❌ Apagar grupo

```bash
sudo groupdel nome_grupo
```

---

## 📄 Listagens do Sistema

### Ver todos os utilizadores do sistema

```bash
cat /etc/passwd
```

### Ver todos os grupos existentes

```bash
cat /etc/group
```

---

## 🧰 Identificação de Sessão

### Ver utilizador atual e identificadores

```bash
whoami     # Nome do utilizador logado
id         # UID, GID, e grupos
```

---

Este conjunto de comandos é essencial para administração segura e eficaz de sistemas Linux. 🧠🔐