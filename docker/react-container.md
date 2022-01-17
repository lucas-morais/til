# Criando container docker para aplicação react

## 1. Criando aplicação react
```bash
npx create-react-app react-dockerized  
``` 

<hr>

## 2. Criando arquivo .dockeringnore 
Este arquivo funciona de maneira similar ao *.gitignore*, todo seu conteúdo será ignorado quando a build da imagem for feita

```dockerignore
node_modules
``` 
<hr>

## 3. Dockerfile parte 1 - Node + Aplicação react
``` dockerfile
# container base node
FROM node:16-alpine AS build

# diretorio da aplicação
WORKDIR /app

# copiando arquivos de dependências
COPY package*.json ./

# instalando dependências
RUN npm install

# copiando demais arquivos
COPY . .

# criando build do projeto
RUN npm run build
``` 
<hr>

## 4. Dockerfile parte 2 - Servidor Nginx

```dockerfile
# servidor web nginx
FROM nginx:1.16.0-alpine AS prod

# compiando arquivos de build
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80
# ao iniciar servidor
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```


## 5. Dockerfile comleto
``` dockerfile
FROM node:16-alpine AS build

# diretorio da aplicação
WORKDIR /app

# copiando arquivos de dependências
COPY package*.json ./

# instalando dependências
RUN npm install

# copiando demais arquivos
COPY . .

# criando build do projeto
RUN npm run build

FROM nginx:1.16.0-alpine AS prod

# compiando arquivos de build
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80
# ao iniciar servidor
ENTRYPOINT ["nginx", "-g", "daemon off;"]

```

