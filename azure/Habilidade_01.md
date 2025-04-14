# **Habilidade 1.1: Descreva a computação em nuvem**

## **Computação em Nuvem**:

A computação em nuvem refere-se ao uso de computadores e infraestrutura para executar aplicativos acessíveis pela internet. Isso envolve um provedor de nuvem, como a Microsoft com o Azure, que assume parte da responsabilidade pelos recursos da nuvem. Um dos principais benefícios é o financeiro, pois permite pagar apenas pelo que se usa, evitando grandes investimentos em infraestrutura e equipe de TI.

A definição de computação em nuvem inclui:
- **Acessibilidade pela internet**: Aplicativos e serviços são acessados online.
- **Provedor de nuvem**: Uma empresa que gerencia e oferece os recursos da nuvem.
- **Modelo de responsabilidade compartilhada**: O provedor e o usuário compartilham responsabilidades pela segurança e manutenção dos recursos.

---

## **Modelo de responsabilidade compartilhada**

No modelo de responsabilidade compartilhada, ao migrar para a nuvem, uma empresa transfere parte da responsabilidade pela infraestrutura e manutenção de seus aplicativos para o provedor de nuvem, como a gestão de servidores e rede, enquanto ainda mantém a responsabilidade pelo sistema operacional e aplicativos. Isso reduz custos e a necessidade de uma grande equipe de TI, pois o provedor de nuvem assume muitas das tarefas de gerenciamento e suporte.

**Tópicos:**
- **Hospedagem local vs. nuvem**: Comparação entre a responsabilidade total da empresa na hospedagem local e a divisão de responsabilidades na nuvem.
- **Redução de custos**: Como a migração para a nuvem pode economizar dinheiro em infraestrutura e folha de pagamento.
- **Responsabilidades do provedor de nuvem**: Tarefas que o provedor de nuvem assume, como gestão de servidores e rede.
- **Responsabilidades do usuário**: Tarefas que permanecem sob a responsabilidade da empresa, como o gerenciamento do sistema operacional e aplicativos.
- **Tipos de serviços de nuvem**: Diferentes níveis de responsabilidade compartilhada dependendo do serviço de nuvem escolhido (IaaS, PaaS, SaaS).

---

## **Modelos de Nuvem**

- **Nuvem Pública**: Recursos de computação são fornecidos por um provedor de serviços e compartilhados entre múltiplos clientes via internet. Exemplos incluem Microsoft Azure, Amazon Web Services (AWS) e Google Cloud Platform (GCP). É escalável e econômica, mas pode levantar preocupações de segurança e privacidade.

    - > _**Importante**_ - **Ambiente multilocatário**: Como você está compartilhando recursos em uma nuvem pública com outras pessoas que estão usando essa nuvem pública, muitas vezes você verá nuvens públicas sendo chamadas de _ambiente multilocatário_.

- **Nuvem Privada**: Infraestrutura de nuvem é dedicada exclusivamente a uma única organização, seja gerenciada internamente ou por um provedor externo. Oferece maior controle e segurança, ideal para empresas com requisitos rigorosos de conformidade e dados sensíveis.

    - > _**Importante**_ - **Ambiente de locatário único**: Como os recursos em uma nuvem privada são dedicados a uma única organização, você frequentemente verá a nuvem privada chamada de _ambiente de locatário único_.

    - A questão principal é que a diferença entre uma nuvem pública e uma privada é a privacidade da infraestrutura e dos dados. Realmente não importa quem é o proprietário da infraestrutura.

- **Nuvem Híbrida**: Combina elementos de nuvens públicas e privadas, permitindo que dados e aplicativos sejam compartilhados entre elas. Oferece flexibilidade e opções de implementação, permitindo que empresas aproveitem os benefícios de ambos os modelos enquanto atendem a necessidades específicas de segurança e desempenho.

    - > _**Importante**_ - **Híbrido nem sempre inclui local**: Lembre-se: uma nuvem privada é uma nuvem dedicada a uma única organização. Ela não precisa estar localizada no local. Também pode ser hospedada em um data center de terceiros, portanto, um modelo de nuvem híbrida pode ser a combinação de um data center de terceiros e uma nuvem pública.

---

### **Nuvem Pública**  

A **nuvem pública** é o modelo mais comum, onde a infraestrutura (rede, armazenamento e máquinas virtuais) é compartilhada entre vários usuários e acessada via internet, sendo gerenciada por provedores como **Microsoft Azure, AWS e Google Cloud**.  

#### **Principais características e vantagens:**  
✔ **Acesso facilitado:** Migração rápida, pois a infraestrutura já está pronta.  
✔ **Custo eficiente:** Paga-se apenas pelos recursos utilizados.  
✔ **Escalabilidade:** Recursos adicionais (como VMs) estão disponíveis sob demanda.  
✔ **Ambiente multilocatário:** Os recursos são compartilhados entre diversos usuários.  

> **Observação:** Acesso geralmente exige autenticação, mesmo sendo via internet.  

Para mais detalhes, consulte: [Azure Public Cloud](https://bit.ly/az900-publiccloud).

--- 

### **Nuvem Privada**  

A **nuvem privada** é um ambiente dedicado exclusivamente a uma única empresa, oferecendo os benefícios da nuvem com maior controle e privacidade. Pode ser hospedada **localmente** ou por um **provedor terceirizado**.  

#### **Principais características e vantagens:**  
✔ **Ambiente de locatário único:** Recursos exclusivos para uma organização.  
✔ **Maior privacidade e conformidade:** Ideal para requisitos regulatórios e dados sensíveis.  
✔ **Flexibilidade de hospedagem:** Pode ser **on-premises** (infraestrutura própria) ou **terceirizada** (em data center dedicado).  
✔ **Controle total:** Acesso restrito a uma rede privada, sem compartilhamento de recursos.  

> **Observação:** A infraestrutura pode ser própria ou de um provedor, mas sempre é dedicada a um único cliente.  

Para mais detalhes, consulte: [Azure Private Cloud](https://bit.ly/az900-privatecloud).

---

### **Nuvem Híbrida**  

A **nuvem híbrida** combina **nuvem pública** e **privada**, permitindo que empresas usem o melhor de ambos os ambientes de forma integrada.  

#### **Principais características e vantagens:**  
✔ **Flexibilidade:** Permite executar cargas de trabalho na nuvem pública enquanto mantém dados sensíveis ou sistemas legados em ambiente privado.  
✔ **Migração gradual:** Ideal para empresas que querem começar a usar a nuvem sem abandonar sistemas locais imediatamente.  
✔ **Cenários variados:** Pode integrar:  
   - Nuvem pública + infraestrutura local.  
   - Nuvem privada (hospedada local ou terceirizada) + serviços de nuvem pública.  
✔ **Controle e escalabilidade:** Mantém o gerenciamento de dados críticos enquanto aproveita a elasticidade da nuvem pública.  

> **Observação:** Nuvem híbrida **não exige infraestrutura local** – a parte privada pode estar em um data center terceirizado.  

Para mais detalhes, consulte: [Azure Hybrid Cloud](https://bit.ly/az900-hybridcloud).

---

## **Modelo baseado no consumo**

O modelo baseado no consumo permite que os usuários de computação em nuvem paguem apenas pelos recursos que realmente utilizam. É possível ajustar a quantidade e a potência das máquinas virtuais (VMs) conforme a necessidade, pagando somente pelo tempo de uso. Isso torna a nuvem mais econômica e eficiente em comparação com soluções locais, sendo uma das principais razões para a adoção crescente da computação em nuvem pelas empresas.

---

### **Resumo – Comparando modelos de nuvem**

Ao escolher um modelo de nuvem, é essencial considerar as necessidades específicas do cenário, pois cada modelo (público, privado e híbrido) tem vantagens e desvantagens.

- **Nuvem pública** é a mais usada, oferecendo economia e praticidade ao transferir a responsabilidade para o provedor. No entanto, há menor controle, possíveis limitações de configuração e preocupações com segurança.
  
- **Nuvem privada** proporciona maior controle e segurança, sendo ideal para setores com exigências rigorosas, como bancos ou empresas em áreas remotas. Em contrapartida, ela pode ter altos custos operacionais e exigir equipe especializada.

- **Nuvem híbrida** combina os benefícios das nuvens pública e privada, permitindo integração entre ambas. Embora ofereça flexibilidade, também traz desafios técnicos, como compatibilidade de dados, complexidade de rede e possível lentidão. Soluções como o **Azure Stack** ajudam a simplificar essa abordagem híbrida.

#### **Tópicos importantes**

- ✅ **Nuvem pública**:
  - Mais popular e econômica (modelo baseado em consumo).
  - Menor controle sobre a infraestrutura.
  - Riscos e exigências adicionais de segurança.
  - Pode haver limitações técnicas (ex: configurações fixas de VMs).

- ✅ **Nuvem privada**:
  - Maior controle e segurança.
  - Ideal para empresas com exigências regulatórias.
  - Custo elevado e necessidade de equipe técnica qualificada.
  - Perda de transparência e controle ao terceirizar a gestão.

- ✅ **Nuvem híbrida**:
  - Integra nuvens pública e privada.
  - Requer atenção à compatibilidade de dados e à performance.
  - Complexidade de rede e desenvolvimento.
  - Soluções como o **Azure Stack** facilitam a adoção híbrida.

---

## **Azure Stack**

Enquanto o Azure é uma plataforma de nuvem pública gerenciada pela Microsoft, o **Azure Stack** é uma extensão do Azure que permite executar aplicativos em um ambiente local e fornecer serviços do Azure no seu data center. Em resumo, o Azure Stack é uma plataforma de nuvem híbrida que traz a agilidade e a inovação da nuvem Azure para o seu próprio ambiente, seja ele um data center on-premises, um provedor de serviços terceirizado ou até mesmo em locais de borda.

Ele oferece uma maneira consistente de construir e implantar aplicativos na nuvem Azure e em ambientes locais, utilizando as mesmas ferramentas, APIs e portal de gerenciamento. Isso facilita a criação de soluções híbridas, onde parte da carga de trabalho reside na nuvem pública e outra parte no ambiente local, atendendo a requisitos de conformidade, latência ou conectividade.

Existem diferentes ofertas do Azure Stack, como o **Azure Stack Hub**, o **Azure Stack HCI** e o **Azure Stack Edge**, cada um otimizado para cenários de uso específicos, desde a execução de aplicativos em data centers até o processamento de dados na borda da rede.

---
