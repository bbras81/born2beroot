---
Data: 17-05-2025
tags:
---
# ✅ Born2beRoot - Checklist para Avaliação Final

Este guia é um resumo direto dos **pontos obrigatórios e bónus** com base no PDF oficial do projeto e no guia de avaliação da intra. Usa este documento durante a defesa para garantir que cobres tudo corretamente.

---

## 🧾 Repositório Git e Signature

### Gerar a signature:

1. Acede à pasta onde está o `.vdi` da tua VM:
    

```bash
cd ~/VirtualBox\ VMs/NOME-DA-TUA-VM/
```

2. Gera o SHA1 do ficheiro `.vdi`:
    

```bash
sha1sum nome-da-imagem.vdi
```

3. Copia o hash gerado e cria o `signature.txt` com ele:
    

```bash
echo "<hash>" > signature.txt
```

Exemplo:

```bash
echo $(sha1sum born2beroot1.vdi | cut -d ' ' -f1) > signature.txt
```

> ⚠️ Este ficheiro `signature.txt` é o **único ficheiro** no repositório Git. A `.vdi` **não** deve ser enviada para o Git!

### Verificar a signature na avaliação:

1. Acede à pasta onde está o `.vdi`
    
2. Corre:
    

```bash
sha1sum nome-da-imagem.vdi
```

3. Compara com:
    

```bash
cat /caminho/para/signature.txt
```

Se quiseres automatizar a comparação:

```bash
diff <(sha1sum Born2beRoot.vdi | cut -d ' ' -f1) signature.txt
```

Se não houver saída, a assinatura está correta ✅

---

## 🔧 Sistema Operativo

-  Debian (ou Rocky, se tiveres experiência)
    
-  Sem interface gráfica (X.org, etc.)
    
-  AppArmor (Debian) ou SELinux (Rocky) ativo no arranque
    

---

## 🧑‍💻 Utilizadores

-  `root` e um utilizador com o teu login (ex: `brunmigu`)
    
-  Este utilizador está nos grupos `sudo` e `user42`
    
-  Criar um novo utilizador durante a defesa
    
-  Criar um grupo `evaluating` e adicioná-lo ao novo user
    

---

## 🔐 Política de Passwords

-  Expira a cada 30 dias
    
-  2 dias mínimos antes de mudar
    
-  Aviso 7 dias antes de expirar
    
-  Pelo menos 10 caracteres, com maiúsculas, minúsculas e números
    
-  Não pode conter o nome do utilizador
    
-  Não mais de 3 caracteres repetidos consecutivos
    
-  Root também cumpre a política
    

---

## 🔑 Sudo

-  Só permite 3 tentativas de password
    
-  Mensagem personalizada em caso de erro
    
-  Registo completo dos comandos em `/var/log/sudo/`
    
-  TTY obrigatório
    
-  `secure_path` limitado: `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin`
    

---

## 🔒 UFW

-  Ativo no arranque
    
-  Apenas porta 4242 aberta
    
-  Explicar o que é o UFW
    
-  Abrir e remover regra para porta 8080 durante a defesa
    

---

## 📡 SSH

-  Instalar e ativo na porta **4242**
    
-  Root login via SSH está desativado
    
-  Login funciona com o utilizador normal
    
-  Explicar o que é SSH e as suas vantagens
    

---

## 🧠 Hostname e Particionamento

-  Hostname é o login seguido de `42` (ex: `brunmigu42`)
    
-  Consegue alterá-lo para o do avaliador e depois restaurar
    
-  Usa LVM com pelo menos **2 partições cifradas**
    
-  Explica o que é o LVM
    

---

## 📜 Script `monitoring.sh`

-  Escrito em bash
    
-  Mostra:
    
    - Arquitetura
        
    - CPUs físicos e lógicos
        
    - RAM usada/total (+ %)
        
    - Disco usado/total (+ %)
        
    - Carga da CPU (%), reboot mais recente
        
    - LVM ativo ou não
        
    - Conexões TCP ESTABELECIDAS
        
    - Utilizadores ativos
        
    - IP e MAC
        
    - Comandos sudo executados
        
-  Corre a cada 10 minutos (via cron)
    
-  Demonstra como parar o script no arranque sem editar o script
    

---

## 🌟 Bónus (só avaliados se tudo acima estiver perfeito)

-  Particionamento extra (estrutura completa)
    
-  WordPress funcional com:
    
    - lighttpd
        
    - MariaDB
        
    - PHP
        
-  Serviço adicional (exceto nginx/apache2)
    
    - Exemplo: Webmin
        
    - Justificar sua utilidade durante a defesa
        

---

## 🎯 Dica final

Antes da defesa:

- Verifica logs: `journalctl -xe`, `tail -f /var/log/*`
    
- Testa conexões: `ping`, `curl localhost`, `ssh user@localhost -p 4242`
    
- Prepara explicações claras para:
    
    - `cron`, `ufw`, `AppArmor`, `sudo`, `lvm`, `wall`, `systemd`
        

Boa sorte! 💪