# conversao-temperatura

## *Aplicação escrita em NodeJS*
  - Os passos a seguir descrevem como criar e excutar esta aplicação em containers.

## Criação do Dockerfile
  - As etapas de construção da imagem são descritas no exemplo Dockerfile abaixo:

```Dockerfile

FROM node:alpine3.14

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD ["node", "server.js"]

```

## Criando a imagem e enviando para o docker hub
  - Na criação da imagem para enviar para o registry do docker, é necessário um namespace válido e também adicionar um nome para o repositório e uma tag como utilizado logo abaixo:

  | Namespace | repositório | Tag |
  |-----------|-------------|-----|
  |machado1976 | conversao_temperatura|v1|
  |machado1976 | conversao_temperatura|latest|  

- Comando para criar a imagem.   
   `$ docker build -t machado1976/conversao_temperatura:v1 .`

- Enviando imagem com a tag v1 para o registry do docker.   
   `$ docker push machado1976/conversao_temperatura:v1`

- Adicionando tag latest.     
   `$ docker tag machado1976/conversao_temperatura:v1 conversao_temperatura:latest`

- Enviando imagem com a tag latest para o registry do docker.     
   `$ docker push machado1976/conversao_temperatura:latest`

## Criando o container
- Para criar e utilizar o container, basta executar o comando como descrito logo abaixo e alterar a porta que ficará exposta no host de acordo com a necessidade. Neste exemplo esta sendo utilizada a porta 8080 para ser acessada do host local.      

 `$ docker container run -d --name conversao_temperatura -p 8080:8080 machado1976/conversao_temperatura:v1`

 ## Acessando a aplicação
 - Agora para acessar a aplicação é só utilizar o browser com o seguinte endereço:      
   ` http://localhost:8080 `
