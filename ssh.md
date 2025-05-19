---
Data: 18-04-2025
tags:
  - ssh
---
# SSH – Guia Completo

Este guia cobre os principais conceitos e comandos relacionados ao SSH (Secure Shell), uma ferramenta fundamental para administradores de sistemas, desenvolvedores e utilizadores de servidores remotos.

---

## 🔐 O que é o SSH?

SSH (Secure Shell) é um protocolo de rede criptografado que permite comunicação segura entre dois computadores, normalmente para acesso remoto a sistemas Unix/Linux.

- **Porta padrão:** 22 (pode ser alterada por segurança)
    
- **Autenticação:** por senha ou chave pública/privada
    
- **Segurança:** Criptografa os dados transmitidos (diferente de Telnet)
    

---

## 🚀 Comandos SSH Mais Comuns

### 📡 Conectar a um servidor remoto

```bash
ssh usuario@ip_ou_host
```

**Exemplo:**

```bash
ssh nome42@192.168.1.42
```

Estabelece uma conexão segura com o servidor.

---

### 🔐 Especificar chave SSH

```bash
ssh -i caminho/para/chave.pem usuario@host
```

**Exemplo:**

```bash
ssh -i ~/.ssh/id_rsa nome42@192.168.1.42
```

Autentica com uma chave privada.

---

### 📁 Copiar ficheiros com SCP (via SSH)

```bash
scp origem destino
```

**Exemplos:**

- Enviar ficheiro:
    

```bash
scp ficheiro.txt nome42@192.168.1.42:/home/nome42/
```

- Buscar ficheiro:
    

```bash
scp nome42@192.168.1.42:/home/nome42/ficheiro.txt ./
```

---

### 📂 Copiar pastas inteiras (com -r)

```bash
scp -r pasta usuario@host:/destino
```

**Exemplo:**

```bash
scp -r projeto/ nome42@192.168.1.42:/home/nome42/
```

---

### 🔁 Túnel SSH (Encaminhamento de Portas)

```bash
ssh -L porta_local:destino:porta_remota usuario@ip
```

**Exemplo:**

```bash
ssh -L 8080:localhost:80 nome42@192.168.1.42
```

Encaminha uma porta local para um serviço remoto.

---

### 📜 Executar comando remoto via SSH

```bash
ssh usuario@host 'comando'
```

**Exemplo:**

```bash
ssh nome42@192.168.1.42 'ls -la /var/log'
```

Executa comandos sem abrir sessão interativa.

---

### 📂 Montar diretório remoto com SSHFS

```bash
sshfs usuario@host:/caminho/remoto /ponto/montagem/local
```

**Exemplo:**

```bash
sshfs nome42@192.168.1.42:/home/nome42 ~/servidor
```

Permite aceder a ficheiros remotos como se fossem locais.

---

### ⏱️ Tempo limite de conexão (timeout)

```bash
ssh -o ConnectTimeout=10 usuario@host
```

Define um timeout de 10 segundos.

---

### 🚪 Usar porta customizada (ex: 4242)

```bash
ssh -p 4242 usuario@host
```

Especifica uma porta alternativa ao padrão.

---

### 🧹 Manter conexão ativa (keepalive)

Adicione ao ficheiro `~/.ssh/config`:

```bash
Host *
  ServerAliveInterval 60
  ServerAliveCountMax 3
```

Evita que a conexão seja encerrada por inatividade.

---

## 🔧 Gestão do Serviço SSH

### 🔍 Verificar estado do serviço

```bash
sudo systemctl status ssh
```

### ✅ Reiniciar o serviço SSH

```bash
sudo systemctl restart ssh
```

### 📜 Ver logs do serviço SSH

```bash
journalctl -u ssh
```

---

## 📚 Curiosidades e Dicas

### apt vs aptitude

- **apt** é o gestor de pacotes mais comum.
    
- **aptitude** é uma interface com mais funcionalidades e visual amigável (modo texto).
    

### SELinux vs AppArmor

- **AppArmor** (usado no Debian/Ubuntu) e **SELinux** (Red Hat/CentOS) são ferramentas de segurança que aplicam políticas de acesso aos programas.
    
- Ambos são sistemas de Mandatory Access Control (MAC).
    

---

Bom estudo e boas conexões! 🔐🖥️e