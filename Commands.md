---
Data: 08-05-2025
tags:
---
# Instalation commands

## [[Detalhes da Instalação#AppArmor|AppArmor]]
``` bash
cat /sys/module/apparmor/parameters/enabled
```

## [[sudo users and groups#👥 Utilizadores|sudo]]
- instalar sudo
``` bash 
sudo apt install sudo
```

- visudo
```bash
sudo visudo
```

- criar as pastas dos logs
```bash
sudo mkdir -p /var/log/sudo
```

- Criar o ficheiro sudo.log
```bash
touch /var/log/sudo/sudo.log
```
- Acrescentar os dados:
```sudo
Defaults passwd_tries=3
Defaults badpass_message="doup!! bad password fellow"
Defaults log_input,log_output
Defaults iolog_dir="/var/log/sudo"
Defaults requiretty
Defaults logfile="/var/log/sudo/sudo.log"
Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

- Criar um grupo
``` bash 
sudo addgroup (Nome do grupo)
```

- Comando para adicionar um USER
``` bash
sudo usermod -aG <groupname> <username>
```

- getent
```bash
$ getent group sudo
sudo:x:27:brummigu
```


#### Explicação:

1. **Estrutura da saída**:
    
    - `sudo`: Nome do grupo
        
    - `x`: Indica que a senha do grupo está armazenada no arquivo `/etc/gshadow`
        
    - `27`: ID do grupo (GID)
        
    - `brummigu`: Usuário(s) que pertencem a este grupo
        
2. **O que isso significa**:
    
    - O usuário `brummigu` tem privilégios administrativos (sudo) nesta máquina.
        
    - Este usuário pode executar comandos como root usando `sudo`.
        
3. **Verificação adicional**:  
    Para confirmar se o usuário tem realmente acesso sudo, você pode executar:

- Mostrar os privilégios específicos do usuário. 
```bash
    sudo -l -U brummigu
```
    
    

- O comando `sudo -V` (ou `sudo --version`) serve para exibir informações detalhadas sobre a versão do `sudo` instalada e as opções de compilação
``` bash
sudo -V
sudo -V>file.txt
```


## [[ssh#🔐 O que é o SSH?|SSH]]
- Instalação:
```bash
sudo apt install openssh-server
```

- Comando para verificar o estado do serviço ssh

``` bash
systemctl status ssh
```

- Comando para reeniciar o serviço ssh

``` bash
systemctl restart ssh
```

- Ficheiro para editar as definições
``` bash
vi /etc/ssh/sshd_config
```

- SSH key genarator
```bash
sudo ssh-keygen
#Insert a passphrase
```

## [[UFW#🔥 UFW – Guia Rápido de Firewall no Linux|UFW]]
### 🔒 Ativar o UFW

```bash
sudo ufw enable
```

### 🔍 Ver o status da firewall

```bash
sudo ufw status
```

## Login
```bash
sudo nano /etc/login.defs
```

Aqui vamos editar este ficheiro de forma a a cumprir os requisitos do enunciado

- **Your password has to expire every 30 days.**
```bash
PASS_MAX_DAYS   99999
#change
PASS_MAX_DAYS   30
```

---

- **The minimum number of days allowed before the modification of a password will be set to 2.**
```bash
PASS_MIN_DAYS   0
#change
PASS_MIN_DAYS   2
```

---

- **The user has to receive a warning message 7 days before their password expires.**
```bash
PASS_WARN_AGE   7
```

# 🔐 Política de Senhas com PAM no Linux

Este guia apresenta como configurar os requisitos de complexidade e segurança das senhas usando o módulo **PAM (Pluggable Authentication Module)** com `pam_pwquality`.

---

## 📦 Instalar o módulo PAM de qualidade de senhas

```bash
sudo apt install libpam-pwquality
```

---

## ✏️ Editar configurações de senha com PAM

Edita o ficheiro:

```bash
sudo nano /etc/pam.d/common-password
```

Procura a linha que começa com:

```text
password requisite pam_pwquality.so
```

### 💡 Exemplo de configuração recomendada:

```text
password requisite pam_pwquality.so retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7
```

---

## ⚙️ Parâmetros explicados

| Parâmetro         | Significado                                                |
| ----------------- | ---------------------------------------------------------- |
| `retry=3`         | Permite 3 tentativas antes de falhar                       |
| `minlen=10`       | A senha deve ter no mínimo 10 caracteres                   |
| `ucredit=-1`      | Pelo menos 1 letra maiúscula                               |
| `lcredit=-1`      | Pelo menos 1 letra minúscula                               |
| `dcredit=-1`      | Pelo menos 1 número                                        |
| `maxrepeat=3`     | No máximo 3 caracteres repetidos consecutivamente          |
| `reject_username` | Rejeita senhas que contenham o nome do utilizador          |
| `difok=7`         | Exige pelo menos 7 caracteres diferentes da senha anterior |

---
## [[Instalation credentials|change passwords]]
- para alterar a palavra passe:
```bash 
sudo passwd brunmigu
```
- definições das palavras pass

```bash
sudo chage brunmigu
sudo chage -M 30 -m 2 -W 7 brunmigu
```

---

## [[Born2beroot#monitoring.sh – Instalação, Comandos e Explicações|Script]]

---

## Enable cron
```bash
sudo systemctl enable cron.service
sudo reboot
```

- Editar o ficheiro com o comando a baixo
```bash
sudo crontab -u root -e
```

- Acrescentar a seguinte linha
```bash
@reboot /usr/local/bin/monitoring.sh
```

### Explicação do código de cron

Este é um agendamento de tarefas (cron job) em sistemas Unix/Linux que executa um script de monitoramento a cada 10 minutos.

## Detalhe de cada parte:

1. `*/10 * * * *` - Esta é a programação de tempo:
   - `*/10` - A cada 10 minutos (a barra com asterisco significa "a cada X intervalos de tempo")
   - Primeiro `*` - Toda hora
   - Segundo `*` - Todo dia do mês
   - Terceiro `*` - Todo mês
   - Quarto `*` - Todo dia da semana

2. `/usr/local/bin/monitoring.sh` - Este é o caminho completo do script que será executado:
   - Está localizado no directório `/usr/local/bin/`
   - O nome do script é `monitoring.sh` (provavelmente um script shell para tarefas de monitoramento)

## Resumo:
Esta entrada no cron irá executar o script `monitoring.sh`:
- A cada 10 minutos
- 24 horas por dia
- 7 dias por semana
- 365 dias por ano
---

## [[Lighttpd]]
- Allow port 80
- enable service
```bash
 sudo systemctl reload lighttpd
 sudo systemctl enable lighttpd
 sudo systemctl start lighttpd
 sudo systemctl status lighttpd
```

---

## [[MariaDB]]

---

## [[PHP]]
```bash
sudo nano /etc/lighttpd/conf-available/15-fastcgi-php.conf
```

- Editar a versão do php no socket(Nao usei)

```php
fastcgi.server += ( ".php" =>
        ((
                "bin-path" => "/usr/bin/php-cgi",
                "socket" => "/run/lighttpd/php8.2.socket",
                "max-procs" => 1,
                "bin-environment" => (
                        "PHP_FCGI_CHILDREN" => "4",
                        "PHP_FCGI_MAX_REQUESTS" => "10000"
                ),
                "bin-copy-environment" => (
                        "PATH", "SHELL", "USER"
                ),
                "broken-scriptfilename" => "enable"
        ))
)
```

```bash
sudo lighty-enable-mod fastcgi
sudo lighty-enable-mod fastcgi-php
sudo systemctl reload lighttpd

```