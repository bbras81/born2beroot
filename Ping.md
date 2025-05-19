---
Data: 12-05-2025
tags:
---
# 🌐 Guia do Comando `ping` no Linux

O comando `ping` é uma ferramenta essencial para diagnosticar a conectividade de rede. Este guia apresenta a sua sintaxe, exemplos e opções úteis para estudo e prática.

---

## 📌 O que é o `ping`?

O `ping` envia pacotes ICMP para um endereço IP ou nome de domínio e mede:

- Se o destino está acessível
    
- O tempo de resposta (latência)
    
- A perda de pacotes
    

---

## 🧪 Sintaxe básica

```bash
ping destino
```

### Exemplo:

```bash
ping google.com
```

> Envia pacotes continuamente para `google.com` até que presses `Ctrl+C`.

---

## 🔧 Opções úteis

### 🔹 Limitar número de pacotes enviados

```bash
ping -c 4 destino
```

Envia apenas 4 pacotes ICMP.

### 🔹 Intervalo entre pacotes (em segundos)

```bash
ping -i 2 destino
```

Envia pacotes a cada 2 segundos.

### 🔹 Ping rápido (sem resolver DNS)

```bash
ping -n destino
```

Evita a resolução de nomes, útil para acelerar testes.

### 🔹 Ping com tamanho de pacote personalizado

```bash
ping -s 100 destino
```

Envia pacotes de 100 bytes em vez dos 56 por padrão.

### 🔹 Ver tempo total e estatísticas

```bash
ping -c 5 google.com
```

Ao final, mostra:

- Pacotes enviados/recebidos
    
- Percentagem de perda
    
- Mínimo/Máximo/Médio de tempo de resposta
    

---

## 📋 Exemplo de saída

```
64 bytes from 142.250.200.46: icmp_seq=1 ttl=116 time=18.5 ms
64 bytes from 142.250.200.46: icmp_seq=2 ttl=116 time=18.3 ms
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 18.300/18.400/18.500/0.100 ms
```

---

## 🚫 Parar o ping

Pressiona `Ctrl+C` para interromper o `ping` contínuo.

---

O comando `ping` é uma das ferramentas mais rápidas e confiáveis para verificar a ligação entre duas máquinas na rede. 🛰️