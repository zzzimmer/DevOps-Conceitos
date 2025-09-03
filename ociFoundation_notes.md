Aqui está a formatação refeita para o último bloco de notas, utilizando uma sintaxe Markdown mais universal para garantir a compatibilidade.

---

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