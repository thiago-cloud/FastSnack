# Aplicação FastSnack

Status: Desenvolvedor ⚠️


A aplicação de fastfood permite que os usuários personalizem seus hambúrgueres através de um formulário interativo, onde podem escolher ingredientes e montar o lanche conforme suas preferências. Após a criação do hambúrguer, o pedido é finalizado e enviado para uma página de gerenciamento de pedidos. Nesta página, os administradores podem visualizar todos os pedidos recebidos, verificar o status atual (como "preparando" ou "entregue"), além de permitir a exclusão ou atualização dos pedidos conforme necessário, garantindo um controle eficiente do fluxo de trabalho do restaurante.

## Tecnologias Utilizadas

- **Backend:**  <a href="https://www.npmjs.com/package/json-server">json-server</a> (Simula uma api REST.).
- **Frontend:** <a href="https://vuejs.org/guide/introduction.html">Vue</a> (Framework Javascript).
- 
## Pré-requisitos

- **NodeJS:** Ambiente de desenvolvimento backend para javascript. <a href="https://nodejs.org/pt">Download do Nodejs</a>
- **NPM:** Gerenciador de pacotes do nodejs.
- **Vue** Instalação do vue cli global, intruções de <a href="https://cli.vuejs.org/#getting-started">instalação</a>`.

## Estrutura do Repositório

- **src/views/:** Páginas principais da aplicação.
- **public/img/:** As imagens e o logo da aplicação estão localizadas no diretório.
- **db/db.json:** Contém as informações dos pedidos.
- **src/components/:** Contém os componentes reutilizaveis deixando o projeto com menos código repetitivo e mais limpo, que servem para colocar em páginas.
- **router/:** Diretório responsável pelo gerenciamento das rotas.
- **App.vue:** Componente principal que importa contém todos os outros componentes da aplicação.
- **README.md:** Este arquivo.

## Como Executar

1. Clone o projeto ou faça um fork, e em seguida de um ```npm install``` na raiz do projeto para instalação das dependências.
2. Abra um terminal na raiz do projeto e digite ```npm run backend``` para execução do backend json-server.
3. Abra outro terminal na raiz do projeto, digite ```npm run serve``` para execução do frontend vue.

