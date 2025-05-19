# 📜 Script `monitoring.sh`

```bash
#!/bin/bash
architecture=$(uname -a | sed 's/ PREEMPT_DYNAMIC//g')
cpu_physical=$(grep "physical id" /proc/cpuinfo | wc -l)
vcpu=$(grep processor /proc/cpuinfo | wc -l)
mem_used=$(free -m | awk '/Mem:/{print $3}')
mem_total=$(free -m | awk '/Mem:/{print $2}')
mem_percent=$(free -m | awk '/Mem:/{printf "%.2f", $3/$2*100}')

disk_total=$(df -BG | grep "^/dev" | grep -v "/boot" | awk '{sum += $2} END {print sum}')
disk_used=$(df -BG | grep "^/dev" | grep -v "/boot" | awk '{sum += $3} END {print sum}')
disk_percent=$(df -BG | grep "^/dev" | grep -v "/boot" | awk '{t += $2} {u += $3} END {printf("%d", u/t*100)}')

cpu_load=$(grep 'cpu ' /proc/stat | awk '{usage=($2+$4)*100/($2+$4+$5)} END {printf "%.1f", usage}')
last_boot=$(who -b | awk '{print $3 " " $4}')

lvm_use=$(lsblk -o TYPE | grep -q lvm && echo "yes" || echo "no")

tcp_conn=$(ss -Ht state established | wc -l)
user_log=$(users | wc -w)

ip_address=$(hostname -I | awk '{print $1}')
mac_address=$(ip link | grep "link/ether" | awk '{print $2}')

sudo_count=$(journalctl -q _COMM=sudo | grep COMMAND | wc -l)

# Montagem da mensagem
wall "# Architecture: $architecture
# CPU physical: $cpu_physical
# vCPU: $vcpu
# Memory Usage: ${mem_used}/${mem_total}MB (${mem_percent}%)
# Disk Usage: ${disk_used}/${disk_total}GB (${disk_percent}%)
# CPU load: ${cpu_load}%
# Last boot: $last_boot
# LVM use: $lvm_use
# Connections TCP : $tcp_conn ESTABLISHED
# User log: $user_log
# Network: IP $ip_address ($mac_address)
# Sudo : $sudo_count cmd"
```

---

# 📊 Resumo do Script de Monitorização (`monitoring.sh`)

Este documento resume de forma clara e simples cada comando utilizado no script `monitoring.sh`, que recolhe informações sobre o sistema. Ideal para estudo e defesa técnica no projeto **Born2beRoot**.

---

## 🖥️ Sistema

### 🔹 Arquitetura

```bash
echo #Architecture: $(uname -a | sed 's/ PREEMPT_DYNAMIC//g')
```

Mostra a arquitetura e o kernel da máquina, limpando a saída.

---

## 🧠 CPU

### 🔹 Núcleos físicos

```bash
echo #CPU physical: $(grep "physical id" /proc/cpuinfo | wc -l)
```

Conta o número de CPUs físicas.

### 🔹 Núcleos lógicos (vCPUs)

```bash
echo #vCPU: $(grep processor /proc/cpuinfo | wc -l)
```

Conta o total de núcleos lógicos.

---

## 🧮 Memória RAM

### 🔹 Uso de RAM

```bash
echo #Memory Usage: $(free -m | awk '/Mem:/{printf "%d/%d (%.2f%%)", $3, $2, $3/$2*100}')
```

Mostra a memória usada, total e a percentagem em MB.

---

## 💽 Disco

### 🔹 Espaço total, usado e percentagem

```bash
disk_total=$(df -BG | grep "^/dev" | grep -v "/boot" | awk '{disk_t += $2} END {print disk_t}')
disk_use=$(df -BG | grep "^/dev" | grep -v "/boot" | awk '{disk_u += $3} END {print disk_u}')
disk_percent=$(df -BG | grep "^/dev" | grep -v "/boot" | awk '{disk_t += $2} {disk_u += $3} END {printf("(%d%%)", disk_u/disk_t*100)}')
echo #Disk Usage: ${disk_use}/${disk_total}GB ${disk_percent}
```

Mostra espaço em uso, total e percentagem.

---

## ⚙️ Carga da CPU

### 🔹 Uso em tempo real

```bash
echo #CPU load: $(grep 'cpu ' /proc/stat | awk '{usage=($2+$4)*100/($2+$4+$5)} END {printf "%.1f%%", usage}')
```

Mostra a carga atual da CPU.

---

## 🔁 Último Reboot

### 🔹 Data e hora do último arranque

```bash
echo #Last boot: $(who -b | awk '{print $3 " " $4}')
```

---

## 💾 LVM

### 🔹 Está ativo?

```bash
lvm=$(lsblk -o TYPE | grep -q lvm && echo "yes" || echo "no")
echo #LVM use: $lvm
```

Indica se o sistema usa LVM.

---

## 🌐 Rede

### 🔹 Conexões TCP estabelecidas

```bash
connections=$(ss -Ht state established | wc -l)
echo #Connections TCP : $connections ESTABLISHED
```

Conta quantas conexões TCP estão ativas.

### 🔹 Utilizadores ativos

```bash
echo #User log: $(users | wc -w)
```

Conta quantos utilizadores estão com sessões abertas.

### 🔹 Endereço IP e MAC

```bash
net_w=$(hostname -I | awk '{print $1}')
net_w6=$(ip link | grep "link/ether" | awk '{print $2}')
echo #Network: IP $net_w ($net_w6)
```

Mostra o IP e o MAC da máquina.

---

## 🔐 Comandos sudo executados

```bash
echo #Sudo : $(journalctl -q _COMM=sudo | grep COMMAND | wc -l) cmd
```

Conta quantos comandos foram executados com `sudo`.

---

Este script é executado automaticamente a cada 10 minutos (via cron) e fornece uma visão rápida e completa do estado da máquina Linux monitorizada. 🛡️