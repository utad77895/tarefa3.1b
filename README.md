# Animalec
An animals Pedagogical app

Para iniciar a app Animalec com as novas entidades Patrocinadores e Especialistas:
```
npm run serve
```

# Using json-server 
Este projeto utiliza [json-server](https://github.com/typicode/json-server) para persistir os dados dos Patrocinadores e Especialistas.

Para instalar json-server:
```
npm install -g json-server
```

Iniciar o json-server:
```
cd db
json-server --watch db.json
```
