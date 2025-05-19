---
Data: 07-05-2025
tags:
---


## Subject
# 🔥 UFW – Guia Rápido de Firewall no Linux

UFW (Uncomplicated Firewall) é uma interface simplificada para o iptables, facilitando a gestão de regras de firewall em sistemas Linux.

---

## 📦 Instalação

```bash
sudo apt update
sudo apt install ufw
```

---

## 🚀 Comandos Básicos

### 🔒 Ativar o UFW

```bash
sudo ufw enable
```

### 🔓 Desativar o UFW

```bash
sudo ufw disable
```

### 🔍 Ver o status da firewall

```bash
sudo ufw status
```

### 🔍 Ver status com detalhes

```bash
sudo ufw status verbose
```

### 🧹 Reset total (remove todas as regras)

```bash
sudo ufw reset
```

---

## ✅ Permitir conexões

### Permitir porta específica (ex: SSH)

```bash
sudo ufw allow 22
```

### Permitir serviço pelo nome

```bash
sudo ufw allow ssh
```

### Permitir TCP/UDP

```bash
sudo ufw allow 80/tcp
sudo ufw allow 53/udp
```

### Permitir acesso de IP específico

```bash
sudo ufw allow from 192.168.1.100
```

### Permitir de IP para porta

```bash
sudo ufw allow from 192.168.1.100 to any port 22
```

---

## ⛔ Bloquear conexões

### Bloquear porta

```bash
sudo ufw deny 23
```

### Bloquear IP

```bash
sudo ufw deny from 10.0.0.100
```

---

## ⚙️ Regras Avançadas

### Permitir conexão a uma interface específica

```bash
sudo ufw allow in on eth0 to any port 22
```

### Permitir faixa de IPs (CIDR)

```bash
sudo ufw allow from 192.168.1.0/24 to any port 22
```

### Permitir porta com intervalo

```bash
sudo ufw allow 1000:2000/tcp
```

---

## 🔐 Políticas Padrão

### Bloquear tudo por padrão (recomendado)

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

---

## 📁 Logs

### Ativar logging

```bash
sudo ufw logging on
```

### Ver logs

```bash
sudo less /var/log/ufw.log
```

---

## 🧠 Dica Extra

Para garantir que o SSH continue acessível após ativar o UFW:

```bash
sudo ufw allow ssh
sudo ufw enable
```

---

UFW é uma ferramenta simples mas poderosa para garantir a segurança da tua máquina! 🛡️


## Thinking...





