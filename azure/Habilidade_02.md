# **Habilidade 1.2: Descreva o benefício de usar serviços em nuvem**

**Esta seção abrange:**
- Alta disponibilidade e escalabilidade
- Confiabilidade e previsibilidade
- Segurança e governança
- Gerenciabilidade na nuvem

---

## **Alta disponibilidade e escalabilidade**

A disponibilidade de dados e aplicativos é crucial, seja em ambientes locais ou na nuvem. Problemas como falhas de rede, aplicativos, sistemas, energia ou dependências externas podem comprometer a disponibilidade.

Para minimizar esses riscos, é essencial ter uma infraestrutura robusta. Provedores de nuvem oferecem um **SLA (Contrato de Nível de Serviço)**, garantindo alta disponibilidade (próxima de 100%), mas cobrem apenas sistemas sob seu controle. Aplicativos na nuvem podem ser desenvolvidos pela empresa ou pelo próprio provedor.

---

### **Falha na rede**  
A conectividade de rede é essencial para o funcionamento dos aplicativos, tanto para usuários quanto para sistemas de back-end. Se houver falhas nessas conexões, o aplicativo pode ficar indisponível. No entanto, com um bom planejamento, é possível minimizar os impactos dessas falhas. Provedores de nuvem oferecem infraestrutura robusta e confiável, muitas vezes resolvendo problemas automaticamente antes que sejam percebidos.

Serviços para garantir conectividade redundante e alta disponibilidade:  
- **Azure Virtual Network (VNet)** – Isolamento lógico e conectividade segura.  
- **Azure Load Balancer** – Distribui tráfego para evitar sobrecarga em servidores.  
- **Azure Traffic Manager** – Roteamento inteligente entre regiões para melhor disponibilidade.  
- **Azure ExpressRoute** – Conexão privada e dedicada à nuvem, evitando a internet pública.  
- **Azure Front Door** – Balanceamento de carga global com proteção contra DDoS.  
- **Azure Route Server** – Melhor gerenciamento de rotas de rede.  

### **Falha na aplicação**  
Falhas em aplicativos geralmente são causadas por bugs ou problemas de design. Embora a nuvem ofereça ferramentas como o *Application Insights* para diagnosticar essas falhas com mais facilidade, o desenvolvedor ainda é responsável por corrigi-las. A nuvem também permite testar versões em ambientes isolados e fazer implantações graduais, facilitando o controle de problemas e a reversão, se necessário.

Serviços para monitoramento, diagnóstico e implantação segura:  
- **Azure Application Insights** – Monitoramento em tempo real de desempenho e falhas.  
- **Azure Monitor** – Coleta e analisa logs e métricas de aplicativos.  
- **Azure DevOps / GitHub Actions** – CI/CD para implantações controladas e rollback automático.  
- **Azure Blueprints** – Modelos padronizados para evitar erros de configuração.  
- **Azure Chaos Studio** – Teste de resiliência simulando falhas.  

### **Falha do sistema**  
Uma falha de sistema ocorre quando o computador que executa um serviço fica indisponível. Na nuvem, esses serviços geralmente rodam em máquinas virtuais (VMs), que são computadores baseados em software dentro de um servidor físico. VMs permitem melhor uso dos recursos e são comuns tanto na nuvem quanto em ambientes locais. Na nuvem, o provedor geralmente monitora e recupera automaticamente VMs com problemas, reduzindo o impacto de falhas.

Serviços para alta disponibilidade e recuperação automática:  
- **Azure Availability Sets** – Distribui VMs em domínios de falha distintos.  
- **Azure Availability Zones** – Replicação em zonas físicas separadas.  
- **Azure Virtual Machine Scale Sets (VMSS)** – Escalabilidade automática e autorrecuperação.  
- **Azure Site Recovery** – Replicação e failover para recuperação de desastres.  
- **Azure Backup** – Backup automatizado de VMs e dados.  

### **Falta de energia**  
A energia elétrica é essencial para a disponibilidade dos sistemas, e até mesmo pequenas interrupções podem causar reinicializações e indisponibilidade temporária. Provedores de nuvem investem em sistemas de energia redundantes e backups para evitar esses problemas. Em casos de quedas de energia em larga escala, é possível executar aplicativos em outras regiões não afetadas.

Serviços para redundância de energia e continuidade operacional:  
- **Datacenters Azure com UPS e geradores** – Infraestrutura redundante.  
- **Azure Availability Zones** – Regiões com fontes de energia independentes.  
- **Azure Site Recovery** – Replicação de cargas de trabalho para outras regiões.  

### **Problemas com um sistema dependente**  
Aplicativos podem depender de sistemas externos ou de outros provedores de nuvem. Se esses sistemas falharem, o aplicativo pode ficar indisponível. A nuvem oferece ferramentas para diagnosticar esses problemas e, em casos de sobrecarga de recursos ou tráfego excessivo, o escalonamento ajuda a manter a disponibilidade.

Serviços para mitigar falhas em dependências externas:  
- **Azure API Management** – Cache, limitação de requisições (*throttling*) e resiliência.  
- **Azure Service Bus / Event Grid** – Mensageria assíncrona para evitar acoplamento direto.  
- **Azure Circuit Breaker Pattern** (via **Polly** ou **Dapr**) – Padrão de tolerância a falhas.  
- **Azure Cache for Redis** – Cache distribuído para reduzir dependência de bancos externos.  

---

### **SLA (Contrato de Nível de Serviço)**

Um **SLA (Service Level Agreement)**, ou **Contrato de Nível de Serviço**, é um acordo formal entre um provedor de serviços e seus clientes (ou entre diferentes departamentos dentro de uma mesma organização). Ele define claramente os **níveis de serviço esperados** pelo cliente e as **obrigações do provedor** em relação a esses níveis.

Em resumo, o SLA estabelece:

* **Quais serviços serão fornecidos.**
* **Os padrões de desempenho esperados** para esses serviços (por exemplo, tempo de resposta, tempo de atividade, tempo de resolução de problemas).
* **As métricas** pelas quais o desempenho será medido.
* **As responsabilidades** de cada parte.
* **As consequências** caso os níveis de serviço não sejam atingidos (por exemplo, penalidades, créditos de serviço).

O principal objetivo do SLA é **alinhar expectativas**, garantir a **qualidade do serviço** e fornecer um **quadro de referência** para medir e gerenciar o desempenho do provedor.

---
