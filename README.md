# DevOps - Fundamentos

**Fontes:**

  - Curso DevOps: explorando conceitos, comandos e scripts no Linux CLI
  - Curso DevOps: trabalhando com tráfego seguro em comunicações web

**Referências:**

  - [GuiaFoca](https://www.guiafoca.org/)
  - [Artigo Linux](https://www.alura.com.br/artigos/linux)
  - [Conversa Cloud e DevOps](https://www.youtube.com/watch?v=SG0VBQG1O7o&ab_channel=Alura)

**Modelo do documento.MD baseado em:** [github/denisfreitas](https://github.com/denisfreitas999/DevOps-Guide)

-----

## Curso DevOps: explorando conceitos, comandos e scripts no Linux CLI

  - [x] **Aula 01 Linux e DevOps - Fundamentos**:

      - Linux é um termo popularmente empregado para se referir a sistemas operacionais que utilizam o Kernel Linux. As distribuições incluem o Kernel Linux, além de softwares de sistema e bibliotecas.
      - Conhecer o sistema de diretórios do Linux.
      - O DevOps é uma abordagem que une as equipes de desenvolvimento e operações para entregar mais e melhor. É uma "cultura", ou uma prática. Aparentemente, essa integração entre as pessoas tem resultado em software mais consistente e melhor ambiente de trabalho. Software mais condizente com a infraestrutura e entregas mais frequentes.
      - As empresas buscam profissionais que entendam de back-end e nuvem, visando um profissional mais generalista do que especializado. Esse profissional precisa também entender do aspecto de custos, visando gerenciar projetos de acordo com a necessidade da aplicação.
          - Contêiner
          - Kubernets/Dock Swarm
          - LoadBalance
      - Configuração do ambiente Linux: foi apresentado a VirtualBox e seu funcionamento através da instalação de um servidor Ubunto na maquina.
      - A introdução do conceito de túnel SSH esclarece como se dá a comunicação de um computador com um servidor a distância.

  - [x] **Aula 02 Explorando o Linux Server**:

      - Automatizar tarefas repetitivas utilizando as linguagens disponibilizadas pelo terminal.
      - Criação de tarefas com execução automática.
      - Automatizar a configuração e instalação de aplicações em novos sistemas.
      - Usar o PowerShell.
      - Apresenta-se uma sequência de comandos Linux e como navegar no server. Comandos como `touch`, `ls`, `mkdir`, `cat`, `echo`. Aprendemos suas funções para criar diretórios, arquivos e navegar entre arquivos.

  - [x] **Aula 03 Shell scripting**:

      - Introdução ao Shell (lógica de "concha" porque é um ambiente protegido).
      - Apresentação do editor de texto nano.
      - Foi desenvolvido o seguinte Script:
        ```sh
        #! /bin/bash

        if [ "$#" -lt 2 ]; then
                echo "O programa $0 requer nome do arquivo e arquivos a serem compactados"
                exit 1
        fi
        arquivo_saida="$1"
        arquivos=("${@:2}")
        tar -czf "$arquivo_saida" "${arquivos[@]}"
        echo "Compactado com sucesso em $arquivo_saida"
        ```
      - E outros scripts em situações problema como -\> Criar um script que será executado automaticamente a cada 24 horas para fazer o backup dos dados críticos da empresa; O script deve listar todos os arquivos e diretórios existentes no servidor, em seguida, criar um arquivo TAR com um nome baseado na data e hora atuais; Finalmente salvar esse arquivo em um diretório de backup designado.
        ```sh
        #! /bin/bash
        diretorio_backup="/path do diretório/"
        ls "$diretorio_backup"
        arquivo_backup="backup_$(date +%Y%m%d_%H%M%S).tar.gz"
        tar -czf "$arquivo_backup" "$diretorio_backup"
        echo "Backup concluído em $arquivo_backup."
        ```
      - Também é possível passar parâmetros para scripts:
        ```sh
        if [ $# -ne 2 ]; then
          echo "Erro! Nao foram fornecidos dois argumentos"
          exit 1
        fi

        arg1=$1
        arg2=$2

        echo "O primeiro argumento é: $arg1"
        echo "O segundo argumento é: $arg2"
        ```
      - **Prática:**
          - Elabore um script simples que exiba uma mensagem de boas-vindas quando executado.
            ```sh
            #!/bin/bash
            echo "Bem-vindo ao meu script!"
            ```
          - Construa um script que seja capaz de criar uma cópia de segurança de um diretório específico.
            ```sh
            #!/bin/bash
            tar -czf backup.tar.gz /caminho/do/diretorio
            ```
          - Crie um script que solicite ao usuário o nome de um diretório e, em seguida, o crie.
            ```sh
            #!/bin/bash
            echo "Digite o nome do diretório:"
            read nome_diretorio
            mkdir $nome_diretorio
            ```
          - Escreva um script que aceite um nome de arquivo como argumento e verifique se o arquivo existe.
            ```sh
            #!/bin/bash
            echo "Digite o nome do arquivo:"
            read nome_arquivo
            if [ -e $nome_arquivo ]; then
              echo "O arquivo existe."
            else
              echo "O arquivo não existe."
            fi
            ```
          - Desenvolva um script que utilize um loop para contar de 1 a 5.
            ```sh
            #!/bin/bash
            for i in {1..5}
            do
              echo $i
            done
            ```

  - [ ] **Aula 04 Automatizando Tarefas**:

  - [ ] **Aula 05 Monitoramento e agendamento**:

-----

## Curso DevOps: trabalhando com tráfego seguro em comunicações web

  - [ ] **Aula 01 Comunicação Web**:

      - Instalação do Node.js e subindo server:
        ```sh
        # baixando o backend
        git clone https://github.com/alura-cursos/api-alurabooks.git

        # acessando a pasta do backend
        cd api-alurabooks

        # instalando as dependências listadas no arquivo package.json
        npm install

        # executando o backend e o disponibilizando através de um servidor no endereço http://localhost:8000
        npm run start-auth

        # baixando o frontend do projeto
        git clone https://github.com/alura-cursos/curso-react-alurabooks.git

        # acessando a pasta do frontend
        cd curso-react-alurabooks

        # selecionando a versão correta
        git checkout aula-5

        # instalando as dependências
        npm install

        # compilando o frontend e o disponibilizando através de um servidor no endereço http://localhost:3000
        npm start
        ```
      - Depois de instalar, precisa entrar nas pastas e dar início:
        ```sh
        # front-end
        cd curso-react-alurabooks
        npm start

        # back-end
        cd api-alurabooks
        npm run start-auth
        ```
      - O DevOps busca juntar desenvolvimento e operações, apresentar um produto funcional que geralmente está em um servidor, o qual precisa interagir com o computador do usuário. Eis o modelo cliente-servidor via protocolo HTTP.
      - **Modelo P2P** - Em contraste ao modelo cliente-servidor, onde o servidor retém os recursos e processos (o que pode levar a falha/sobrecarga), o modelo P2P descentraliza a relação e onde "[...] cada dispositivo computacional possui equivalência em funcionalidade."
      - "[...]O modelo P2P se baseia no compartilhamento de recursos sem atuação de intermediários, como um servidor central, em que cada computador pode assumir tanto o papel de cliente como de servidor. Essa abordagem apresenta benefícios como maior escalabilidade, redundância e resistência a falhas."
      - O **Modelo TCP/IP** contém 5 camadas que mediam o transporte de dados entre os dispositivos cliente-servidor. Essa tecnologia de comunicação embarcada em diferentes dispositivos (modem, switch, roteador, etc) é constituída de 5 camadas:
          - Aplicação: Onde ocorre a interação entre as aplicações e rede.
          - Transporte: Nessa camada, o principal protocolo é o TCP, que recebe, organiza e encaminha a mensagem para a camada de rede.
          - Rede: Nessa camada, ocorre o endereçamento de IP destino e origem - visando a possibilidade de rastreamento do pacote pela rede.
          - Enlace
          - Física
      - Cada dispositivo tem um endereço IP.
      - Para as políticas de segurança: A camada **Aplicação** deve ser a prioridade.
          - **Motivo:** é nela que ficam os serviços acessíveis diretamente pelos atacantes (HTTP, SMTP, DNS, APIs, etc.). Vulnerabilidades em softwares e protocolos de aplicação são os principais vetores de intrusão (SQL injection, XSS, exploração de serviços mal configurados, APIs expostas).
          - Claro que segurança precisa ser em camadas (firewall na Rede, TLS na Transporte, autenticação e criptografia na Aplicação), mas o maior impacto e efetividade imediata está em reforçar políticas na camada de Aplicação.
      - O DevOps precisa compreender de rede para organizar os servidores de forma confiável. *O Servidor carrega a lógica de negócios e o front-end cuida da navegação e interação dos usuários.* O Http faz o meio de campo dessa interação.
          - Teste no terminal: `curl localhost:3000` ou qualquer site.

  - [ ] **Aula 02 Mapeamento de Recursos**:

      - `http://localhost:3000/`
          - `http:` -\> protocolo
          - `//localhost:` -\> servidor
          - `3000`-\> porta do server
          - `/` -\> Caminho do recurso
      - **Domain Name System (DNS)** Vincula nome de domínio com endereço de IP.
      - 
      - 
      - [https://www.alura.com.br/artigos/dns-o-que-e-qual-escolher](https://www.alura.com.br/artigos/dns-o-que-e-qual-escolher)
      - `ping www.utwente.nl`
      - `traceroute www.youtube.com.br`

  - [ ] **Aula 03 Explorando HTTP**:

      - HTTP se baseia em troca de mensagens com estrutura definida (visando a flexibilidade e escalabilidade). Os métodos em http indicam as intenções (GET, PUT, POST, DELETE, entre outros).
      - Infraestrutura como código.
      - Um servidor HTTP opera sem guardar informações de requisições passadas (**stateless**). Para contornar isso, usamos sessões e **cookies**, "lembrando" o servidor de quem somos.
      - Na prática, um token de acesso é criado via Postman e enviado no cabeçalho da requisição, permitindo acesso a páginas restritas. A segurança em aplicações web é crucial, exigindo senhas fortes e mecanismos de proteção eficazes.
      - As aplicações web são stateless, ou seja, não mantêm o estado após o encerramento da conexão do navegador. Cada requisição HTTP é independente.
      - Os servidores web não possuem a responsabilidade de armazenar, autenticar dados do cliente ou manter as sessões. É nesse cenário que os cookies entram em ação.
      - As solicitações de cookies podem ser realizadas através de um header (cabeçalho de resposta) chamado `Set-Cookie`, estabelecido pelo servidor. Ao acessar pela primeira vez uma página, as informações ficam armazenadas no seu computador. Na próxima requisição, o navegador envia os Cookies de volta ao servidor através do header `Cookie`.

  - [ ] **Aula 04 Comunicação segura**:

      - Introdução à ferramenta de monitoramento de rede **WireShark**, visando conhecer e mapear as vulnerabilidades de rede.
      - A perspectiva apresentada é da responsabilidade mútua, tanto de Dev quanto Ops, ligado à segurança de dados.
      - A ferramenta de captura demonstra os conteúdos de tráfego, expondo as fragilidades do HTTP. A segurança é aprimorada com o uso do **HTTPS**, que conta com uma camada de segurança que precisa ser implementada em código.
      - Introdução kit de ferramentas **OpenSSL**: Chave privada e certificado digital.
      - Deve-se acessar a pasta do projeto:
        `cd api-alurabooks;`
      - E executar o código de geração do certificado e chave do server:
        `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.crt`
      - Isso irá gerar os dois arquivos que deverão ser alterados na IDE para implementar o uso do HTTPS. No caso, `server.js` precisa ser alterado para que essa camada funcione antes das configurações de porta.
      - [https://www.alura.com.br/artigos/criptografia-diferencas-simetrica-assimetrica-homomorfica](https://www.alura.com.br/artigos/criptografia-diferencas-simetrica-assimetrica-homomorfica)
      - **Socket**: porta de entrada para comunicação (SSH usa isso).

**Refs:**

  - **Desconstruindo a web: as tecnologias por trás de uma requisição** (não gratuito, português, livro) Neste livro, o autor Willian Molinari explora separadamente cada item de uma requisição web.
  - **Requisições HTTP utilizando o AXIOS** (gratuito, português, texto) Esse artigo oferece informações valiosas para aprimorar suas práticas de desenvolvimento e otimizar o manuseio de requisições HTTP em seus projetos.
  - **Redes de computadores** (gratuito, português, livro) O livro de Redes de Computadores, escrito por Marcial Porto Fernández e editado pela Editora da Universidade Estadual do Ceará (EdUECE), está disponível para acesso no Portal eduCAPES.
  - **Roadmap back-end: Conhecendo o protocolo HTTP e arquiteturas REST** (não gratuito, português, livro) O livro oferece uma exploração detalhada do protocolo HTTP e das arquiteturas REST.
  - **Internet Engineering Task Force** (gratuito, inglês, texto) O IETF cria padrões voluntários que frequentemente são adotados por usuários da Internet, contribuindo para moldar o desenvolvimento da Internet.