# Laboratório Windows Server 2025 – Infraestrutura Corporativa

**Status:** Ambiente funcional, em uso para estudos e simulação de cenário empresarial.  
**Domínio:** `carol.corp`  
**Controlador de Domínio:** `DC01` (Windows Server 2025 Datacenter - Core/GUI em Inglês)  
**Cliente de Teste:** `CL01-WIN10` (Windows 10 Pro)  

---

## 🎯 Objetivo

Simular um ambiente de infraestrutura corporativa Microsoft completo e aderente às melhores práticas de mercado, demonstrando competências em:
* **Active Directory Domain Services (AD DS):** Arquitetura, promoção e gerenciamento de identidades.
* **Segregação de Escopo:** Estruturação lógica de Unidades Organizacionais (OUs) orientada a departamentos.
* **Group Policy Objects (GPOs):** Implementação de políticas estritas de segurança (*hardening*) e automação de ambiente.
* **Serviços de Rede Essenciais:** Provisionamento e gerenciamento implícito de DNS e DHCP.
* **Operação Eficiente:** Gerenciamento centralizado de conexões remotas utilizando o *Remote Desktop Manager (RDM)*.
* **Virtualização Local:** Orquestração de hosts e redes isoladas via *VMware Workstation*.

---

## 🖥️ Ambiente Virtualizado (VMware Workstation)

| Ativo | Sistema Operacional | Memória RAM | Processadores (vCPUs) | Armazenamento | Função no Ambiente |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **DC01** | Windows Server 2025 (EN-US) | 8 GB | 4 | 120 GB + 20 GB | Controlador de Domínio Principal (AD DS), DNS e DHCP |
| **CL01-WIN10** | Windows 10 Pro (PT-BR) | 4 GB | 2 | 60 GB | Estação de Trabalho de Usuário (Ingressada no Domínio) |

* **Segmentação de Rede:** Modo NAT (`192.168.157.0/24`)  
* **Endereçamento IP Fixo (DC01):** `192.168.157.128` (Garantindo persistência para gerência via RDM)

---

## 🔐 Active Directory – Arquitetura de Unidades Organizacionais (OUs)

A árvore do domínio `carol.corp` foi projetada visando a alta escalabilidade e aplicação granular de políticas. A estrutura separa rigorosamente contas de colaboradores de ativos físicos (computadores):

```text
carol.corp
├── Matriz
│   ├── Financeiro
│   │   ├── Computadores
│   │   └── Usuarios
│   └── RH
│       ├── Computadores
│       └── Usuarios
├── TI
│   ├── Computadores
│   └── Usuarios
└── (OUs Nativas: Builtin, Computers, Domain Controllers, Users)

📸 Evidências de Validação (AD Users and Computers)Diretório Geral e Domain Controller Centralizado: Exibe o servidor principal catalogado nativamente com a tipagem Global Catalog (GC) e mapeamento de topologia de site.Estrutura do Departamento Financeiro:Estrutura do Departamento de Recursos Humanos (RH):Estrutura do Departamento de Tecnologia da Informação (TI): Nota: As OUs de computadores dos demais setores encontram-se estruturadas e prontas para provisionamento automatizado de novas estações de trabalho conforme a escalabilidade do negócio.

⚙️ Políticas de Grupo (GPO) AplicadasForam desenvolvidas e vinculadas GPOs focadas em Hardening (segurança de endpoint) e padronização da experiência do usuário final:Nome da GPOTipo de ConfiguraçãoImpacto / Efeito PráticoEscopo de VinculaçãoGPO_Bloqueio_USBComputerBloqueio estrito de leitura/escrita de dispositivos de armazenamento USB removíveis (Prevenção de vazamento de dados).OUs de ComputadoresGPO_Bloqueio_CMDUserRestringe o acesso ao Prompt de Comando (CMD) para mitigar a execução de scripts não autorizados por usuários comuns.OUs de UsuáriosGPO_Bloqueio_Painel_ControleUserImpede o acesso às configurações do Painel de Controle e Settings do sistema, mitigando alterações indesejadas no SO.OUs de UsuáriosGPO_Bloqueio_WallpaperUserForça a aplicação do papel de parede padrão corporativo da empresa e bloqueia a alteração pelo usuário.OUs de UsuáriosGPO_Mapeamento_Unidade_SUser (Drive Maps)Provisiona de forma totalmente automatizada o mapeamento do File Server na unidade de rede S: no momento do logon.OUs de Usuários(Insira aqui o seu print do console GPMC se tiver)
Nome da GPO,Tipo de Configuração,Impacto / Efeito Prático,Escopo de Vinculação
GPO_Bloqueio_USB,Computer,Bloqueio estrito de leitura/escrita de dispositivos de armazenamento USB removíveis (Prevenção de vazamento de dados).,OUs de Computadores
GPO_Bloqueio_CMD,User,Restringe o acesso ao Prompt de Comando (CMD) para mitigar a execução de scripts não autorizados por usuários comuns.,OUs de Usuários
GPO_Bloqueio_Painel_Controle,User,"Impede o acesso às configurações do Painel de Controle e Settings do sistema, mitigando alterações indesejadas no SO.",OUs de Usuários
GPO_Bloqueio_Wallpaper,User,Força a aplicação do papel de parede padrão corporativo da empresa e bloqueia a alteração pelo usuário.,OUs de Usuários
GPO_Mapeamento_Unidade_S,User (Drive Maps),Provisiona de forma totalmente automatizada o mapeamento do File Server na unidade de rede S: no momento do logon.,OUs de Usuários

🛠️ Ferramentas de Gerenciamento UtilizadasRemote Desktop Manager (RDM): Utilizado como console centralizado para sessões administrativas seguras via RDP no DC01.Server Manager: Dashboard central para auditoria de status das roles ativas (AD DS, DNS, DHCP).

📚 Habilidades Técnicas DemonstradasInstalação, provisionamento e sysprep de sistemas operacionais de servidor Microsoft em idioma nativo (Inglês).Arquitetura e implantação de Domain Controllers ativos.Administração de identidades e grupos de segurança globais no Active Directory.Provisionamento avançado de GPOs utilizando filtros de escopo precisos.Configuração e governança de permissões em compartilhamentos de rede automatizados.Documentação de arquitetura técnica de infraestrutura.

🔗 Referências TécnicasO ambiente foi construído seguindo rigorosamente os guias de design e boas práticas da documentação oficial da Microsoft:Microsoft Learn – Active Directory Domain Services ArchitectureGroup Policy Management and Hardening Guide

👩‍💻 AutoraAna Carolina Avellar – GitHubProfissional em transição de carreira, focada em Administração de Infraestrutura de TI e Cloud Computing. ---Última atualização: Junho / 2026
