---
Data: 18-04-2025
tags:
  - ssh
---
# monitoring.sh – Instalação, Comandos e Explicações

Este ficheiro resume os **passos de instalação**, os **comandos usados** no script `monitoring.sh` e suas **explicações**, para facilitar o estudo e compreensão.

---

## 🔧 Instalação do Ambiente

### 1. Instalar o sistema operativo Debian (recomendado)

**Durante a instalação:**

```bash
# Escolher modo expert ou avançado
# Selecionar partição manual
# Criar ao menos duas partições criptografadas com LVM
# NÃO instalar ambiente gráfico (sem GNOME, KDE, Xorg etc.)
```

### 2. Atualizar o sistema

```bash
sudo apt update && sudo apt upgrade -y
```

### 3. Instalar ferramentas necessárias

```bash
sudo apt install sudo ufw vim net-tools lvm2 procps iproute2 net-tools util-linux bsdmainutils -y
```

### 4. Criar utilizador e grupos obrigatórios

```bash
sudo adduser nome42
sudo usermod -aG sudo nome42
sudo groupadd user42
sudo usermod -aG user42 nome42
```

### 5. Ativar e configurar o SSH

```bash
sudo apt install openssh-server -y
sudo sed -i 's/#Port 22/Port 4242/' /etc/ssh/sshd_config
sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
sudo systemctl restart ssh
```

### 6. Ativar o UFW (firewall)

```bash
sudo ufw allow 4242/tcp
sudo ufw enable
```

### 7. Ativar o AppArmor

```bash
sudo systemctl enable apparmor
sudo systemctl start apparmor
```

### 8. Configurar política de senhas

```bash
sudo apt install libpam-pwquality -y
sudo nano /etc/login.defs
# Modificar ou garantir:
PASS_MAX_DAYS   30
PASS_MIN_DAYS   2
PASS_WARN_AGE   7

sudo nano /etc/pam.d/common-password
# Adicionar ou garantir:
password requisite pam_pwquality.so retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7
```

### 9. Configurar sudo

```bash
sudo mkdir /var/log/sudo
sudo nano /etc/sudoers.d/logging
# Conteúdo:
Defaults        logfile="/var/log/sudo/sudo.log"
Defaults        log_input
Defaults        log_output
Defaults        requiretty
Defaults        passwd_tries=3
Defaults        badpass_message="Senha incorreta! Tente novamente."
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

### 10. Criar o script `monitoring.sh`

```bash
sudo nano /usr/local/bin/monitoring.sh
# Colar o conteúdo do script (ver abaixo)
sudo chmod +x /usr/local/bin/monitoring.sh
```

### 11. Agendar execução automática

```bash
sudo crontab -e
# Adicionar a linha:
*/10 * * * * /usr/local/bin/monitoring.sh
```

---

## 📜 Comandos do monitoring.sh e Explicações

### 1. Arquitectura do Sistema

```bash
echo \#Arquitecture: $(uname -a | sed 's/ PREEMPT_DYNAMIC//g')
```

Exibe informações completas sobre o kernel e Arquitectura do sistema.

### 2. Número de Núcleos Físicos

```bash
echo \#CPU physical: $(grep "physical id" /proc/cpuinfo | wc -l)
```

Conta os processadores físicos.

### 3. Número de Núcleos Virtuais

```bash
echo \#vCPU: $(grep processor /proc/cpuinfo | wc -l)
```

Conta os processadores lógicos (vCPUs).

### 4. Memória RAM

```bash
echo \#Memory Usage: $(free -m | awk '/Mem:/{printf "%d/%d (%.2f%%)", $3, $2, $3/$2*100}')

```

Exibe memória usada, total e percentagem.

### 5. Espaço em Disco

```bash
df -m | grep "/dev/" | grep -v "/boot" | awk '{used+=$3} END{print used}'
df -m | grep "/dev/" | grep -v "/boot" | awk '{tot+=$2} END{printf("%.0f", tot/1024)}'
df -m | grep "/dev/" | grep -v "/boot" | awk '{u+=$3}{t+=$2} END{printf("%.2f%%", u/t*100)}'
```

Calcula uso do disco em MB/GB e percentagem.

### 6. Uso da CPU (%)

```bash
cpu_idle=$(vmstat 1 4 | tail -1 | awk '{print $15}')
echo "CPU Usage: $(awk \"BEGIN {printf \"%.1f%%\", 100 - $cpu_idle}\")"
```

Mostra percentagem de uso da CPU.

### 7. Último Reboot

```bash
who -b | awk '$1=="system"{print $3 " " $4}'
```

Data e hora do último boot do sistema.

### 8. LVM Ativo

```bash
if [ $(lsblk | grep -c lvm) -gt 0 ]; then echo "yes"; else echo "no"; fi
```

Verifica se há volumes LVM ativos.

### 9. Conexões TCP Estabelecidas

```bash
ss -ta | grep ESTAB | wc -l
```

Conta conexões TCP ativas.

### 10. Utilizadores Ativos

```bash
users | wc -w
```

Conta quantos utilizadores estão logados.

### 11. IP e MAC

```bash
hostname -I | awk '{print $1}'
ip link | grep "link/ether" | awk '{print $2}'
```

Mostra o endereço IP e MAC.

### 12. Comandos com sudo

```bash
journalctl _COMM=sudo | grep COMMAND | wc -l
```

Conta quantos comandos foram executados com `sudo`.

---

Bom estudo! 🚀