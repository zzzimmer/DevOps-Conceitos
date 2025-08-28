# DevOps - Fundamentos 

Fontes: 
- Curso DevOps: explorando conceitos, comandos e scripts no Linux CLI 
- Curso DevOps: trabalhando com tráfego seguro em comunicações web

Referencias:
- [text](https://www.guiafoca.org/)
- [text](https://www.alura.com.br/artigos/linux)

Modelo do documento.MD baseado em: [text](https://github.com/denisfreitas999/DevOps-Guide)

## Curso DevOps: explorando conceitos, comandos e scripts no Linux CLI 
- [x] **Aula 01 Linux e DevOps - Fundamentos**:
   - Linux é um termo popularmente empregado para se referir a sistemas operacionais que utilizam o Kernel Linux. As distribuições incluem o Kernel Linux, além de softwares de sistema e bibliotecas.
   - Conhecer o sistema de diretórios do Linux
   - O DevOps é uma avordagem que une as equipes de desenvolvimento e operações para a entregar mais e melhor. É uma "cultura", ou uma prática. Aparentemente, essa integração entre as pessoas tem resultado em software mais consistente e melhor ambiente de trabalho.
   - Configuração do ambiente Linux: foi apresentado a VirtualBox e seu funcionamento através da instalação de um servidor Ubunto na maquina.
   - A introdução do conceito de tunel SSH esclarece como se da a comunicação de um computador com um servidor a distância.
<!-- - [x] **Git e GitHub - Fundamentos**:
   - Git é um sistema de controle de versão distribuído gratuito e de código aberto projetado para lidar com tudo, desde projetos pequenos a muito grandes com velocidade e eficiência.
   - GitHub é um serviço de hospedagem para desenvolvimento de software e controle de versão usando Git.
   - Criar um repositório
   - Clonar um repositório
   - Fazer commit, push e pull de e para o repositório
   - Reverter um commit
   - Criar branches e pul requests
   - Lidar com merge e conflitos
- [x] **HTTP - Fundamentos**:
   - HTTP significa Hyper Text Transfer Protocol. A comunicação entre computadores cliente e servidores web é feita enviando solicitações HTTP e recebendo respostas HTTP.
   - Entender a diferença dos verbos HTTP
   - Testar os requests e ver os status codes no navegador
   - Saber fazer uma requisição HTTP na linha de comando com WGET
   - Baixar uma imagem com WGET
   - Fazer um post -->
- [x] **Aula 02 Explorando o Linux Server**:
   - Automatizar tarefas repetitivas utilizando as linguagens disponibilizadas pelo terminal.
   - Criação de tarefas com execução automática
   - Automatizar a configuração e instalação de aplicações em novos sistemas
   - Usar o PowerShell
   - Apresenta-se uma sequencia de comandos Linux e como navegar no server. Comandos como touch, ls, mkdir, cat, echo. Aprendemos suas funcoes para criar diretorios, arquivos e navegar entre arquivos.
   - [x] **Aula 03 Shell scripting**:
   - Introdução ao Shell (lógica de "concha" porque é um abiente protegido) 
   - Apresentação do editor de texto nano.
   - Foi desenvolvido o seguinte Script:
        GNU nano 7.2                                compactador                                         
#! /bin/bash

if [ "$#" -lt 2 ]; then
        echo "O programa $0 requer nome do arquivo e arquivos a serem compactados"
        exit 1
fi
arquivo_saida="$1"
arquivos=("${@:2}")
tar -czf "$arquivo_saida" "${arquivos[@]}"
echo "Compactado com sucesso em $arquivo_saida"
   - E outros scrips em situações problema como -> Criar um script que será executado automaticamente a cada 24 horas para fazer o backup dos dados críticos da empresa; O script deve listar todos os arquivos e diretórios existentes no servidor , em seguida, criar um arquivo TAR com um nome baseado na data e hora atuais; Finalmente salvar esse arquivo em um diretório de backup designado

#! /bin/bash
diretorio_backup="/path do diretório/"
ls "$diretorio_backup"
arquivo_backup="backup_$(date +%Y%m%d_%H%M%S).tar.gz"
tar -czf "$arquivo_backup" "$diretorio_backup"
echo "Backup concluído em $arquivo_backup."

- Também é possível passar parâmetros para scripts:

if [ $# -ne 2 ]; then
  echo "Erro! Nao foram fornecidos dois argumentos"
  exit 1
fi

arg1=$1
arg2=$2

echo "O primeiro argumento é: $arg1"
echo "O segundo argumento é: $arg2"

Pratica:
Elabore um script simples que exiba uma mensagem de boas-vindas quando executado.

#!/bin/bash
echo "Bem-vindo ao meu script!"

Construa um script que seja capaz de criar uma cópia de segurança de um diretório específico.

#!/bin/bash
tar -czf backup.tar.gz /caminho/do/diretorio

Crie um script que solicite ao usuário o nome de um diretório e, em seguida, o crie.

#!/bin/bash
echo "Digite o nome do diretório:"
read nome_diretorio
mkdir $nome_diretorio

Escreva um script que aceite um nome de arquivo como argumento e verifique se o arquivo existe.

#!/bin/bash
echo "Digite o nome do arquivo:"
read nome_arquivo
if [ -e $nome_arquivo ]; then
  echo "O arquivo existe."
else
  echo "O arquivo não existe."
fi

Desenvolva um script que utilize um loop para contar de 1 a 5.

#!/bin/bash
for i in {1..5}
do
  echo $i
done
- [ ] **Aula 04 Automatizando Tarefas**:


- [ ] **Aula 05 Monitoramento e agendamento**:

## Curso DevOps: trabalhando com tráfego seguro em comunicações web
- [ ] **Aula 01 Comunicação Web**:
   - Instalação do Node.js e subindo server:

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

-- Depois de instalar, precisa entrar nas pastas e dar inicio

-front-end
cd curso-react-alurabooks
npm start

-back-end
cd api-alurabooks
npm run start-auth

- O DevOps busca juntar des e operações, apesentar um produto funcional que geralmente esta em um servidor, o qual precisa interagir com o computador do usuario. Eis o modelo cliente-servidor via protocolo HTTP. 
- Modelo P2P - Em contraste ao modelo cliente-servidor, onde o servidor retem os recursos e processos (o que pode levar a falha/sobrecarga) o modelo P2P descentraliza a relação e onde "[...] cada dispositivo comutacional possui equivalencia em funcionalidade." 
- "[...]O modelo P2P se baseia no compartilhamento de recursos sem atuação de intermediários, como um servidor central, em que cada computador pode assumir tanto o papel de cliente como de servidor. Essa abordagem apresenta benefícios como maior escalabilidade, redundância e resistência a falhas."

- O Modelo TCP/IP contem 5 camadas que mediam o transporte entre de dados entre os dispositivos cliente-servidor. Essa tecnologia de comunicação embarcada em diferentes dispositivos (modem, switch, roteador, etc) é constituida de 5 camadas:
   - Aplicação: Onde ocorre a interação entre as aplicações e rede.
   - Transporte: Nessa camada, o principal protocolo é o TCP, que recebe, organiza e incaminha a mensagem para a camada de rede
   - Rede: Nessa camada, ocorre o endereçamento de IP destino e origem - visando a possibilidade de rastreamento do pacote pela rede.
   - Enlace: 
   - Física
- Cada dispisitivo tem um endereço IP. 
- Para as politicas de segurança: 
   A camada Aplicação deve ser a prioridade.

   Motivo: é nela que ficam os serviços acessíveis diretamente pelos atacantes (HTTP, SMTP, DNS, APIs, etc.). Vulnerabilidades em softwares e protocolos de aplicação são os principais vetores de intrusão (SQL injection, XSS, exploração de serviços mal configurados, APIs expostas).

   Claro que segurança precisa ser em camadas (firewall na Rede, TLS na Transporte, autenticação e criptografia na Aplicação), mas o maior impacto e efetividade imediata está em reforçar políticas na camada de Aplicação.

- O DevOps precisa compreender de rede para organizar os servidores de forma confiável. *O Servidor carrega a logica de negócios e o front-end cuida da navegação e interação dos usuarios* O Http faz o meio de campo dessa interação.
   - Teste no terminal: curl localhost:3000 / ou qualquer site. 



