---
Data: 12-05-2025
tags:
---
# ⚙️ Instalação e Configuração do PHP com Lighttpd

Este guia mostra como instalar e configurar o PHP com o servidor web **Lighttpd**, utilizando PHP-FPM e módulos essenciais para aplicações web.

---

## 📦 Instalar PHP e extensões necessárias

```bash
sudo apt install php-cgi php-mysql -y
```

### 🔍 O que cada pacote faz:

|Pacote|Função|
|---|---|
|`php-fpm`|PHP FastCGI Process Manager – permite que o Lighttpd execute PHP|
|`php-mysql`|Comunicação com bases de dados MySQL/MariaDB|
|`php-curl`|Comunicação HTTP via cURL (muito usado por APIs)|
|`php-gd`|Manipulação de imagens em PHP|
|`php-zip`|Leitura/criação de ficheiros `.zip` em PHP|

---

## 🔧 Ativar suporte a FastCGI no Lighttpd

### Habilitar o módulo FastCGI e FastCGI-PHP:

```bash
sudo lighty-enable-mod fastcgi
sudo lighty-enable-mod fastcgi-php
```

### Reiniciar o Lighttpd:

```bash
sudo systemctl restart lighttpd
```

---

## 🧪 Testar PHP

### Criar ficheiro de teste:

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

### Aceder no navegador:

```
http://localhost/info.php
```

Deverás ver a página do `phpinfo()` com informações do PHP.

---

## 📋 Verificar estado do PHP-FPM

```bash
sudo systemctl status php*-fpm
```

Procura por `active (running)`.

---

## 🧼 Remover ficheiro de teste após uso:

```bash
sudo rm /var/www/html/info.php
```

---

Agora o teu Lighttpd já suporta PHP, e está pronto para executar aplicações web com acesso a bases de dados e funcionalidades modernas! 🚀