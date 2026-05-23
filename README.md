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
