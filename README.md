En este proyecto es parte del curso **React Avanzado: Fullstack Next.js, Apollo, MongoDB y GraphQL** en [Udemy](https://www.udemy.com/course/fullstack-react-graphql-y-apollo-de-principiante-a-experto/): 

instalamos chocolatey https://chocolatey.org/install

instalar nodejs
choco install nodejs.install
npm init
npm i apollo-server
npm i -D nodemon
npm i graphql

**en package.json agregar** ============
```javascript
"scripts": {
  "start": "node .",
  "dev": "nodemon ."
}
```

# **========== GrapgQL =========**
**query** - en un crud nos permite leer los registros, equivalente a select o get
**Mutation** - para actualizar, eliminar y crear registros
```javascript
    mutation eliminarProducto($id: ID){
    	eliminarProducto(id: $id)
    }
```
**Resolver** - son funciones para retornar los valores que existen en tu schema, los nombres deben ser iguales a los definidos en el schema
```javascript
obtenerClientes: async() => {
	const clientes = await Clientes.find();
	return clientes;
}
```
**Schema** - describe tipos de objetos, queries y datos de la app, query es obligatorio

## Schema y resolver =======
schema :
```javascript
type Query {
	obtenerCliente(id: ID): Cliente
}
type Cliente {
	id: ID
	nombre: String
	apellido: String
	empresa: String
	emails: [Email]
	edad: int
}
```
resolver:
```javascript
obtenerCliente: async (_, { id }) => {
	const cliente = await Cliente.findById( id)
	return cliente
}
```

### arreglo de cursos para ejemplosarreglo de cursos para ejemplos 
https://gist.github.com/codigoconjuan/625857eec22fad9ba3b4e41c11fafd0a
```javascript
const cursos = [
    {
        titulo: 'JavaScript Moderno Guía Definitiva Construye +10 Proyectos',
        tecnologia: 'JavaScript ES6',
    },
    ....
];
```

### input =======
el simbolo '!' significa que es obligatorio
```javascript
const typeDefs = gql`
    ...
    type Query {
        obtenerCursos(input: CursoInput!) : [Curso]
        obtenerTecologias: [Tecnologia]
    }
`;
```

### argumentos del resolver ====
1er: '_' - en un objeto con los resultados retornados 
2o: '{input}'
3o context - objeto que se comparte entre todos los resolvers
4o info - informacion sobre la consulta actual
```javascript
const resolvers = {
    Query: {
        obtenerCursos: (_, {input}, ctx, info )=> {
            console.log(input);
        }
    }
}
```

### variables en localhost:4000 ====
```javascript
query obtenerCursos($input: CursoInput! ) {
    obtenerCursos( input: $input){
      titulo
    }
}
```
variables :
```javascript
{
  "input": {
    "tecnologia": "React"
  }
}
```

### context ==
```javascript
const server =new ApolloServer({
    typeDefs,
    resolvers,
    context: ()=> {
        const miContext = "Hola";

        return {
            miContext
        }
    }
});
```

### minimo para comenzar un proyecto =====
index.js :
```javascript
const { ApolloServer } = require('apollo-server');
const typeDefs = require('./db/schema');
const resolvers = require('./db/resolvers')
//servidor
const server =new ApolloServer({
    typeDefs,
    resolvers
});
//arrancar el servidor
server.listen().then( ({url})=> {
    console.log(`Servidor listo en la URL ${url}`);
})
```

resolvers.js :
```javascript
// Resolvers
const resolvers = {
    Query: {

    }
}
module.exports = resolvers;
```

schema.js :
```javascript
const { gql } = require('apollo-server');
// Schema
const typeDefs = gql`

`;
module.exports = typeDefs
```

### tipos de datos =====
- int =entero
- float = numero con decimales
- string
- id = numero unico
- boolean

### hashear password ======
npm i bcryptjs
```javascript
const bcryptjs = require("bcryptjs");
const salt = await bcryptjs.getSalt(10)
input.password = await bcryptjs.hash(password, salt);
```
npm i jsonwebtoken

## ============= mongo ===========
crear un cluster en mongo atlas en la web

### instalar mongoose ======
npm i mongoose dotenv

npx create-next-app crmcliente
npm i formik yup
npm i @apollo/client node-fetch
npm i graphql
npm i apollo-link-context
npm install sweetalert2
npm i react-select
npm install recharts
