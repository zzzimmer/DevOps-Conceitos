## Curso Certificação Oracle Cloud Infraestructure: explorando o ambiente e funcionalidades.

- **Aula 01 Entendendo OCI**


    - OCI trabalha com 3 níveis de serviço:
        1.  **Infraestrutura:** Programação, VMs, Containers, LoadBalance, Monitoramento, Segurança.
        2.  **Plataforma:** Integração, IA, frameworks ligados a Oracle.
        3.  **Serviços:** Softwares de gerenciamento de empresa entregues prontos (HCL e ERP).

    - A organização da OCI se dá por **regiões** (espaço geográfico) > **domínios de disponibilidade** (data centers independentes na mesma região) > **domínios de falha** (subdivisões de hardware dentro de um domínio de disponibilidade para evitar ponto único de falha).
        - *Exemplo: Servidor principal no domínio de falha 1, servidor de redundância no domínio de falha 2.*

    - **Oracle Multicloud (Nuvem distribuída):**
        - **Problemas que resolve:**
            - Restrição de conformidade (ex: LGPD, que exige dados no país de origem).
            - Latência de rede.
            - Custo e performance variáveis.

    - **Tipos de nuvem:**
        - **Nuvem pública:** OCI Public Cloud.
        - **Nuvem dedicada:** Espaço físico exclusivo para um cliente.
        - **Oracle Alloy:** Nuvem personalizada.
        - **Oracle Cloud at Customer:** Serviço de nuvem rodando no data center do próprio cliente.
`1. Tenancy: Sua conta na OCI.`

`2. Compartimentos: Contêineres lógicos para organizar e controlar o acesso aos recursos (no mesmo nível das regiões).`

`3. Regiões: Localizações geográficas (como São Paulo ou Vinhedo) dentro da sua Tenancy.`

`4. Domínios de Disponibilidade (ADs): Datacenters independentes dentro de uma região.`

`5. Virtual Cloud Network (VCN): Rede virtual privada que reside dentro de uma região e abrange um ou mais ADs.`

`6. Sub-redes: Segmentos da VCN onde você aloca seus recursos (instâncias, bancos de dados, etc.).`

    > #### Cenário de Alta Disponibilidade
    >
    > **Pergunta:** Em uma região com um único domínio de disponibilidade, como implantar uma aplicação com 2 servidores e 1 banco de dados de 2 nós para alta disponibilidade?
    >
    > **Solução:** Colocar um servidor e um nó do banco de dados em um **domínio de falha**, e o segundo servidor e o segundo nó do banco de dados em **outro domínio de falha**.
    >
    > **Justificativa:** Isso distribui os componentes em hardwares físicos diferentes. Se um domínio de falha cair, o outro permanece ativo, garantindo a continuidade da aplicação.

- **Aula 02 Identity and Acess Management (IAM)**

    - O IAM da Oracle serve para criar e gerenciar usuários, grupos, permissões e políticas de segurança.

    - **Estrutura do IAM:**
        - **Domínios (Tenancy):** A estrutura principal que engloba tudo.
        - **Compartimentos:** "Pastas" para organizar recursos, aplicar políticas e isolar ambientes (ex: produção, desenvolvimento).
        - **Usuários e Grupos:** Entidades que realizam ações.
        - **Políticas:** Regras que definem o que um grupo pode fazer e em qual compartimento.

    - **Autenticação (AuthN) vs. Autorização (AuthZ):**
        - **AuthN:** "Quem é você?". Confirma a identidade do usuário (login, senha, MFA).
        - **AuthZ:** "O que você pode fazer?". Define as permissões de acesso via políticas.

    - **Boas práticas:**
        - Evitar usar a conta `Tenancy Admin` (master). Criar contas de administrador com permissões mais restritas (`OCI Admin-group`).
        - Usar compartimentos para isolar recursos.
        - Habilitar Autenticação Multifator (MFA).

    > #### Conceitos Chave
    >
    > - **Pergunta:** Qual componente do IAM ajuda a organizar vários usuários em uma equipe?
    > - **Resposta:** **Grupos**.
    >
    > - **OCID (Oracle Cloud Identifier):** Identificador único para cada recurso na OCI.

- **Aula 03 Networking**

    - **VCN (Virtual Cloud Network):** Rede virtual personalizável, de baixa latência e alta disponibilidade.

    - **Problemas que a VCN visa resolver:**
        - Acesso não autorizado e falhas de segurança.
        - Desempenho e latência da rede.
        - Dificuldade em conectar ambientes híbridos (nuvem + on-premises).
        - Escalabilidade.

    - **Componentes da VCN:**
        - **Sub-redes:** Divisões da VCN. Podem ser **públicas** (acessíveis da internet) ou **privadas** (acesso restrito).
        - **CIDR:** Notação que define o intervalo de endereços IP da rede.
        - **Gateways:**
            - **Internet Gateway:** Permite comunicação de mão dupla entre a sub-rede pública e a internet.
            - **NAT Gateway:** Permite que recursos em sub-redes privadas acessem a internet (apenas saída), sem serem acessíveis de fora.
            - **Service Gateway:** Permite acesso a outros serviços públicos da Oracle (ex: Object Storage) sem passar pela internet.
            - **Dynamic Routing Gateway:** Conecta a VCN com redes fora da OCI (ambientes híbridos).

    > #### Arquitetura de Aplicação (Caso de Uso Real)
    >
    > **Pergunta:** Como organizar uma aplicação com API e banco de dados em uma VCN?
    >
    > **Resposta (Arquitetura de 3 camadas):**
    > 1.  **Sub-rede Pública:** Coloca-se a máquina virtual com a **API**. Ela se comunica com o mundo externo através de um `Internet Gateway`.
    > 2.  **Sub-rede Privada:** Coloca-se o **banco de dados**. Ele não tem acesso direto à internet e só pode ser acessado pela API, garantindo a segurança.
    >
    > A comunicação entre a API e o banco de dados ocorre de forma segura dentro da VCN.

    > #### Conexão de Ambientes Híbridos
    >
    > **Pergunta:** Como a VCN conecta um data center local (on-premises) com a nuvem?
    >
    > **Resposta:** Através de duas principais formas:
    > - **VPN:** Uma conexão criptografada segura pela internet. Mais econômica.
    > - **FastConnect:** Uma conexão de rede privada, dedicada e de alta velocidade. Ideal para baixa latência e grande volume de dados.
    >
    > **Exemplo:** Uma loja de varejo pode manter seu sistema de estoque *on-premises* e rodar seu site de e-commerce na nuvem OCI. Usando `FastConnect`, o site na nuvem pode consultar o estoque local em tempo real de forma segura e rápida.

    - **Load Balancer:** Distribui o tráfego de rede entre múltiplos servidores para garantir alta disponibilidade e desempenho.


    - **Aula 04 Compute**

    Visto os conteudos anteriores, chegamos a parte de Compute da OCI. Nessa parte, utiliza-se todos os conhecimentos anteriores (dominio de disponibilidade, compartment, VCN, tenancy).

### Resumo dos Conceitos Essenciais da OCI

- **Instância:** Um servidor virtual (VM) ou físico (Bare Metal) criado na OCI para executar aplicações e serviços.

- **Compartment:** Contêiner lógico para organizar e isolar recursos, controlar acesso, aplicar políticas de segurança e gerenciar custos.

- **VCN (Virtual Cloud Network):** Rede virtual privada na OCI, permitindo comunicação segura entre instâncias e configuração de sub-redes, roteamento e gateways.

- **Domínio de Disponibilidade (AD):** Datacenters isolados dentro de uma região, garantindo alta disponibilidade e tolerância a falhas.

- **Tenancy:** Raiz da conta na OCI, representando a organização e contendo todos os recursos, compartments e políticas.

#### Hierarquia da OCI:
1. **Tenancy:** Nível mais alto, representando a conta.
2. **Compartment:** Organização de recursos em "pastas".
3. **VCN:** Rede virtual privada dentro de um compartment.
4. **Domínio de Disponibilidade (AD):** Datacenter dentro de uma região.
5. **Instância:** Máquina virtual ou física criada em uma VCN e AD.

#### Analogia:
- **Tenancy:** O prédio inteiro (sua empresa).
- **Compartments:** Andares do prédio (departamentos).
- **VCN:** Rede interna de cada andar.
- **Instâncias:** Computadores individuais nos andares.
- **Domínios de Disponibilidade:** Prédios diferentes no mesmo complexo, garantindo continuidade em caso de falhas.

ssh -i ssh-key-ARQUIVO-CHAVE.key -p PORTA-SSH USUARIO@IP_DO_SERVIDOR

Pós maquina criada, com OS e capacidade escolhido, é só acessar via SSH. Esse serviço da OCI visa solucionar os diversos problemas de manter uma estrutura física, como:

- Custo de hardware e manutenção
- Dificuldade de escalabilidade
- Baixo desempenho e limitacões tecnicas
- Complexidade de gerenciamento

Dessa forma, cria-se um ambiente virtual ou bare metal, que conta com toda estrutura de REDE fornecida, com um sistema operacional escolhido, processadores de diferentes marcas, volumes de armazenamento escolhidos...
Enfim, tem uma sequencia de configurações recomendadas para as maquinas, como deixar a OCI escolher um dominio de falha especifico, algo nesse sentido. 
Também tem o recurso de Live Migration, que ajuda a prevenir falhas

**Scanling e OKE**

- O Scaling é a capacidade de aumentar ou reduzir recursos computacionais conforme a demanda da aplicação, de forma manual ou automática. Nos interessa essa possibilidade devido a possíveis momentos de alta demanda em um servidor, ou então de demanda reduzida e recurso sobrando. Ademais, essa possibilidade de mudança de escala é importante em aplicações distribuidas.

O *Scaling vertical*, se trata de modificar recursos computacionais ligados a memória e processamento, enquanto *Scaling horizontal* esta ligado a 

Vertical - planejado, fora do horário de produção (pode gerar um downtime no servidor, ocasionando perdas)

Scaling vertical significa aumentar a capacidade computacional (memoria e cpu) de UMA determinada instância, enquanto scaling horizontal é aumentar a quantiade DE INSTANCIAS ?

- OKE Oracle Kubernates Engine é um mecanismo oferecido pela Oracle, mas você pode escolher gerenciar manualmente.

Serviço gerenciado de Kubernates da Oracle

- Oracle Functions - Serviço Servless(sem servidor) dentro da OCI





  