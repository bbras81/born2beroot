---
Data: 08-05-2025
tags:
---


## Subject

## Instalaçao e configuração do sistema
``` bash
lsblk
```

- O `lsblk` lista todos os dispositivos de armazenamento em bloco, incluindo discos rígidos, unidades USB, e outros dispositivos de armazenamento. 
    
- **Formato de árvore:**
    
    A saída do `lsblk` é apresentada em formato de árvore, o que facilita a visualização da estrutura de partições dos dispositivos. 
    

- **Informações detalhadas:**
    
    O `lsblk` fornece informações como o nome do dispositivo, o tamanho, o tipo de dispositivo, o tipo de sistema de arquivos, o ponto de montagem e muito mais. 
    

- **Opções e filtros:**
    
    O `lsblk` oferece diversas opções para personalizar a saída, como filtrar por tipo de dispositivo, exibir informações específicas e selecionar quais colunas exibir. 
    

- **Uso em scripts:**
    
    A saída do `lsblk` é estável e pode ser usada em scripts para automatizar tarefas de gerenciamento de dispositivos.

### AppArmor 
É um módulo de segurança do kernel Linux que permite aos administradores de sistema restringir os recursos dos programas com perfis específico. Esses perfis definem o que cada programa pode ou não fazer, incluindo acesso à rede, operações de sistema e manipulação de ficheiros. É um sistema de controle de acesso mandatório (MAC) que funciona sobre a interface Linux Security Modules (LSM), conferindo uma camada adicional de segurança para além dos controles tradicionais de acesso discricionário (DAC). 

Em resumo, AppArmor:

- **Restringe recursos:** Define o que cada programa pode ou não fazer. 

- **Controlo de Acesso Mandatório (MAC):** Proporciona segurança adicionais ao nível do kernel. 

- **Perfis de Segurança:** Define as permissões para cada programa. 

- **Melhora a Segurança:** Ajuda a proteger o sistema de ameaças, incluindo ataques de dia zero, ao limitar o acesso de programas a recursos críticos. 

Como funciona:

- **1.** **Perfis:**
    
    Os administradores criam perfis que especificam quais recursos um programa pode usar, como acesso a ficheiros, rede, etc. 
    

- **2.** **Monitorização:**
    
    O kernel monitoriza as chamadas de sistema e, antes de as executar, verifica se o processo que as solicitou tem a permissão definida no perfil. 
    

- **3.** **Segurança Adicional:**
    
    Se uma chamada de sistema for feita por um programa sem a permissão adequada, a AppArmor impede que a operação seja realizada, aumentando a segurança do sistema. 
    

Benefícios:

- **Segurança aprofundada:** Complementa os controles de acesso discricionários tradicionais. 

- **Proteção contra malware:** Reduz o impacto de malware ao limitar o acesso dos programas a recursos cruciais. 

- **Defesa contra ataques de dia zero:** Previne a exploração de vulnerabilidades desconhecidas. 

- **Flexibilidade:** Permite a criação de perfis personalizados para diferentes aplicações e necessidades de segurança. 

Exemplo:

Um perfil para um serviço de impressão pode restringir o acesso do serviço apenas a ficheiros de impressão e à rede necessária para comunicar com a impressora, impedindo que o serviço aceda a outros ficheiros no sistema ou outras redes.
## Thinking...





