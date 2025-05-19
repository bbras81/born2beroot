---
Data: 12-05-2025
tags:
---

# 🌐 Guia Rápido do Lighttpd

O **Lighttpd** (pronuncia-se _"lighty"_) é um servidor web leve, rápido e seguro, ideal para sistemas com poucos recursos ou projetos simples.

---

## 🔎 O que é o Lighttpd?

- Um **servidor HTTP** alternativo ao Apache e Nginx
    
- Projetado para **alto desempenho e baixa utilização de memória**
    
- Muito usado em:
    
    - Servidores embarcados (ex: Raspberry Pi)
        
    - Páginas web estáticas
        
    - Pequenas APIs ou aplicações locais
        

---

## 🚀 Características principais

|Recurso|Descrição|
|---|---|
|🔥 Leve e rápido|Usa poucos recursos do sistema|
|⚙️ Suporte a FastCGI|Permite correr PHP, Python, Ruby|
|🔒 Seguro|Suporte a SSL/TLS, limitação de conexões|
|📁 Virtual Hosts|Permite vários sites no mesmo servidor|
|🧾 Configuração simples|Tudo gerido em `/etc/lighttpd/lighttpd.conf`|

---

## 📦 Instalação

### Em Debian/Ubuntu:

```bash
sudo apt update
sudo apt install lighttpd
```

---

## 🧪 Comandos básicos

### Iniciar, parar ou reiniciar o serviço:

```bash
sudo systemctl start lighttpd
sudo systemctl stop lighttpd
sudo systemctl restart lighttpd
sudo systemctl status lighttpd
```

---

## 📁 Estrutura de ficheiros

|Caminho|Função|
|---|---|
|`/var/www/html`|Diretório das páginas web|
|`/etc/lighttpd/lighttpd.conf`|Ficheiro de configuração principal|
|`/var/log/lighttpd/`|Logs de acesso e erro|

---

## 🔧 Exemplo de configuração básica

Abre o ficheiro:

```bash
sudo nano /etc/lighttpd/lighttpd.conf
```

E configura:

```conf
server.port = 80
server.document-root = "/var/www/html"
```

Para aplicar alterações:

```bash
sudo systemctl restart lighttpd
```

---


