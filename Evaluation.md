---
Data: 18-05-2025
tags:
---
# Avaliação Born2beroot

## Clonar a VM

- Para evitar problemas com a assinatura.
- Para criar o hash da assinatura:

    ```bash
    echo <(sha1sum born2beroot1.vdi | cut -d ' ' -f1) > signature.txt
    ```

## Verificar a assinatura

- Se não houver resultado, significa que o ficheiro não é diferente, logo está correto:

    ```bash
    sha1sum ~/goinfre/born2beroot/born2beroot.vdi | cut -d ' ' -f1 | diff - signature.txt

    ```

---
## 🧠 Explicação simples: O que é uma máquina virtual?

> **“Uma máquina virtual é como um computador dentro de outro computador.”**

Ela simula um sistema completo (como se fosse um PC real), com disco, memória, CPU e sistema operativo — mas tudo isso a correr dentro de um programa (como o VirtualBox), que usamos no nosso sistema real (host).

---
## 🆚 **Rocky Linux vs. Debian**
## 🧠 Explicação prática para avaliação:

> **“Debian é mais aberto e simples, com foco em estabilidade e liberdade. Rocky Linux é voltado para empresas e segue as versões do Red Hat Enterprise Linux.”**

|Característica|**Debian** 🐧|**Rocky Linux** 🪨|
|---|---|---|
|**Base**|Projeto comunitário independente|Clonagem compatível com Red Hat (RHEL)|
|**Gestor de pacotes**|`apt` (com `.deb`)|`dnf` / `yum` (com `.rpm`)|
|**Foco**|Estabilidade + liberdade|Estabilidade empresarial (como CentOS)|
|**Sistema de init**|`systemd`|`systemd`|
|**Comunidade**|Muito ativa e antiga|Nova, mas apoiada por empresas|
|**Segurança padrão**|Usa AppArmor|Usa SELinux|
|**Instalação**|Simples, minimalista|Mais automatizada e enterprise|
|**Atualizações**|Mais frequentes e manuais|Mais lentas, pensadas para produção|

---

### ✅ Propósitos das VMs:

1. **📦 Isolamento:**  
    Cada VM funciona como um computador separado. Se uma VM for comprometida, o sistema real (host) continua seguro.
    
2. **🧪 Testes e desenvolvimento:**  
    Podemos testar sistemas operativos, configurações de rede, scripts ou aplicações sem arriscar o sistema principal.
    
3. **📁 Portabilidade:**  
    As VMs são ficheiros (`.vdi`, `.ova`, etc.) que podem ser copiadas e executadas em outros computadores com o mesmo estado.
    
4. **📚 Educação e formação:**  
    Ideais para ambientes de ensino como a 42, onde cada aluno pode ter o seu próprio ambiente controlado.
    
5. **🔁 Repetibilidade:**  
    Podemos criar snapshots, reverter estados e reproduzir testes facilmente.

---
## Diferença entre `apt` e `aptitude`

### ✅ `apt`

- Interface de linha de comandos (CLI)
    
- Mais leve e rápida
    
- Usada para tarefas básicas: instalar, atualizar, remover pacotes
    
- Comandos comuns:
    
    bash
    
    CopiarEditar
    
    `sudo apt update sudo apt install nome-do-pacote sudo apt remove nome-do-pacote`
    

---

### ✅ `aptitude`

- Interface mais avançada (tem **interface em modo texto** se usado sem argumentos)
    
- Resolve conflitos de dependências de forma **mais inteligente**
    
- Sugere várias soluções quando há problemas com pacotes
    
- Não vem instalada por padrão (precisa ser instalada com `sudo apt install aptitude`)

---

### UFW 
```bash
sudo ufw status
```

### SSH

```bash
sudo systemctl status ssh
```

```bash
sudo ss -tlpn | grep 4242
```

### Verificar se o sistema operativo é Debian

```bash
cat /etc/os-release
```
**Saída típica para Debian:**
```bash
PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
```


---

## Users

### addUser
```bash 
adduser <nome-do-user>
```

### [[Commands#Login|Pass Policy]]

### addGorup
```bash
sudo addgroup <nome-do-grupo>
```

---
### hostName

```bash 
sudo hostnamectl set-hostname novo-nome
```

- Pode ser atualizado tambem em /etc/hosts
```bash
sudo vim  /etc/hosts
127.0.0.1 <novo-host>
sudo reboot
```

### partitions
### O que é o LVM?

Imagina que o teu disco é como um conjunto de **caixas** onde guardas coisas.

Normalmente, quando instalas Linux, divides o disco em **partições fixas** — como se colasses etiquetas nas caixas e dissesses “esta é do sistema”, “esta é dos ficheiros”, etc. O problema? Se uma caixa ficar cheia, tens de mexer muito para reorganizar tudo.

O **LVM** (Logical Volume Manager) resolve isso. Ele transforma essas caixas **fixas** em **caixas elásticas**, que podes **aumentar, encolher ou juntar a outras** com facilidade.

---

### 🧱 Como funciona?

Imagina 3 etapas:

1. **PV (Volume físico)** → São os discos ou partições normais.
    
2. **VG (Grupo de volumes)** → Junta vários discos/partições num grande “armazém”.
    
3. **LV (Volume lógico)** → São as "caixas elásticas" dentro do armazém, onde podes guardar o que quiseres (por exemplo, o sistema, os dados, etc).
    

---

### 🎯 Exemplo prático:

- Tens dois discos: um de 100GB e outro de 200GB.
    
- Com LVM, podes **juntá-los** num só “Grupo de Volumes” de 300GB.
    
- Dentro desse espaço, crias “Volumes Lógicos” como quiseres: 100GB para o sistema, 50GB para música, 150GB para vídeos…
    
- E se a pasta dos vídeos crescer? Podes **aumentar o volume lógico** sem mexer nos outros!
    

---

### 💡 Vantagens:

- **Redimensionar** volumes facilmente.
    
- **Juntar discos** diferentes como se fossem um só.
    
- **Snapshots** (guardar o estado de um volume para backup).
    
- Muito útil para **servidores ou sistemas que crescem com o tempo**.

--- 

## SUDO
```bash
which sudo
```

```bash
sudo --version
```

```bash
sudo visudo
```

---

## **UFW**?

**UFW** significa **Uncomplicated Firewall** (firewall descomplicado).

É uma ferramenta que te ajuda a controlar **quem pode aceder ao teu computador pela rede** (internet ou local), **de forma simples**.


### 🛡️ Para que serve?

Serve para:

- **Bloquear acessos indesejados**
    
- **Permitir apenas o que tu queres** (por exemplo, permitir SSH e bloquear o resto)
    

É uma forma fácil de gerir o **iptables**, que é o firewall do Linux — mas o `iptables` é complicado, e o `ufw` torna tudo mais fácil.

### add rule

```bash
sudo ufw allow 8080
```

### remove rule
```bash
sudo ufw status numbered
sudo ufw delete [nbr]
```

---

## sudo 

```bash
sudo nano /etc/ssh/sshd_config
```

- **Verificar a port**
- **permitroot no**
---

## cron
- script
```bash
/usr/local/bin/monitoring.sh
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

```bash
sudo systemctl status
```

- **Ver o numero do processo**
```bash
sudo kill nr-processo
```