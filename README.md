# Laboratório Windows Server 2025 – Infraestrutura Corporativa

> **Status:** Ambiente funcional, em uso para estudos e simulação de cenário empresarial.  
> **Domínio:** `carol.corp`  
> **Controlador de Domínio:** DC01 (Windows Server 2025 em inglês)  
> **Cliente:** CL01-WIN10 (Windows 10 Pro)

---

## 🎯 Objetivo

Simular um ambiente corporativo Microsoft completo, demonstrando habilidades em:
- Administração de **Active Directory Domain Services (AD DS)**
- Criação de **Unidades Organizacionais (OUs)** por departamentos
- Aplicação de **Políticas de Grupo (GPO)** para segurança e padronização
- Serviços de rede: **DNS, DHCP** (implicitamente configurados)
- Gerenciamento centralizado com **Remote Desktop Manager (RDM)**
- Virtualização com **VMware Workstation**

---

## 🖥️ Ambiente Virtualizado (VMware)

| Máquina | Sistema | RAM | CPUs | Disco | Função |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **DC01** | Windows Server 2025 (inglês) | 8 GB | 4 | 120 GB + 20 GB | Domain Controller, AD, DNS, DHCP |
| **CL01-WIN10** | Windows 10 Pro | 4 GB | 2 | 60 GB | Cliente domínio |

- **Rede:** Modo NAT (192.168.157.0/24)  
- **DC01 IP:** 192.168.157.128 (conforme RDM)

![Config DC01](./prints/vmware-dc01-config.png)  
![Config CL01](./prints/vmware-cl01-config.png)

---

## 🔐 Active Directory – Estrutura de OUs

Domínio: `carol.corp`

```text
carol.corp
├── Matriz
│   ├── Financeiro
│   │   ├── Computadores
│   │   └── Usuários
│   └── RH
│       ├── Computadores
│       └── Usuários
├── TI
│   ├── Computadores
│   └── Usuários
└── (Builtin, Computers, Domain Controllers, Users padrão)

**Prints de evidência:**

- OU Matriz:  
  ![OU Matriz](./prints/ad-ou-matriz.png)

- Departamentos Financeiro e RH:  
  ![Financeiro e RH](./prints/ad-ou-financeiro-rh.png)

- Departamento de TI:  
  ![TI](./prints/ad-ou-ti.png)

---

## ⚙️ Políticas de Grupo (GPO) Aplicadas

Foram criadas e vinculadas GPOs para endurecimento (hardening) e padronização:

| GPO | Efeito | Aplicada a |
|-----|--------|-------------|
| `GPO_Bloqueio_UBS` | Bloqueia dispositivos USB | OUs de Computadores |
| `GPO_Bloqueio_CMD` | Restringe acesso ao prompt de comando | OUs de Computadores |
| `GPO_Bloqueio_Panel de Controle` | Bloqueia acesso ao Painel de Controle | OUs de Computadores |
| `GPO_Bloqueio_Wallpaper` | Força wallpaper padrão da empresa | OUs de Computadores |
| `GPO_Mapeamento_Unidade_S` | Mapeia unidade de rede S: automaticamente | OUs de Usuários |

![Lista de GPOs](./prints/gpmc-gpos-list.png)

---

## 🛠️ Ferramentas de Gerenciamento

- **Remote Desktop Manager (RDM)** – Acesso centralizado ao DC01 via RDP  
  ![RDM Entry](./prints/rdm-dc01-entry.png)

- **Server Manager** – Roles instaladas: AD DS, DNS, DHCP  
  ![Server Manager Roles](./prints/server-manager-roles.png)

---

## 📚 Habilidades Demonstradas

- Instalação e configuração de Windows Server em inglês  
- Promoção a Domain Controller e criação de domínio  
- Estruturação de OUs por departamento  
- Criação e vinculação de GPOs de segurança  
- Mapeamento de unidade de rede via GPO  
- Virtualização com VMware Workstation  
- Documentação técnica organizada

---

## 🔗 Como Reproduzir

Este ambiente foi construído do zero seguindo documentação oficial Microsoft.  
Os passos principais podem ser encontrados em:

- [Microsoft Learn – Active Directory Domain Services](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/adds-on-premises-virtualization)
- [Gerenciamento de GPOs](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-overview)

---

## 👩‍💻 Autora

**Ana Carolina Avellar** – [GitHub](https://github.com/carolavellar)  
Este laboratório faz parte do meu portfólio de Infraestrutura TI.  
📫 Contato: (acavellar@hotmail.com)

---

*Última atualização: Maio/2026*
