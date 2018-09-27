# Curso de back-end

## Ambiente
  ### DataGrip

## Banco de dados relacional

 - MySQL
 - Sqlite

 - Tabelas e esquema
   - tipos de dados
```SQL
create table tracks (
  id     INTEGER PRIMARY KEY AUTOINCREMENT,
  title  varchar(200),
  artist varchar(200)
);
```

```SQL
select * from tracks;
```

## Comandos

### INSERT
  ```SQL
  insert into tracks(title, artist) values
  ("Skank","Pacato Cidadão"),
  ("Pink Floyd", "The Wall - part 1"),
  ("Pink Floyd", "The Wall - part 2"),
  ("Pink Floyd", "The Wall - part 3");
  ```  
### SELECT
 - WHERE 
 - ORDER
 - AGREGATIONS and GROUP BY 

### UPDATE
### DELETE

### Relações

   - um para muitos
   - muitos para muitos

### Índices
 - Normalização

## ActiveRecord

### Instalação
```bash
npm install --save sequelize
npm install --save sqlite3 
# npm install --save mysql2 # para MySQL
```

### Configuração
```Javascript
const Sequelize = require('sequelize');
const sequelize = new Sequelize('laboratoria', 'username', 'password', {
  host: 'localhost',
  dialect: 'sqlite',
  // SQLite only
  storage: './laboratoria.sqlite'
});
``` 

```Javascript
sequelize
  .authenticate()
  .then(() => {
    console.log('Connection has been established successfully.');
  })
  .catch(err => {
    console.error('Unable to connect to the database:', err);
  });
```

### Definição do Esquema

```JavaScript
const Track = sequelize.define('track', {
  title: {
    type: Sequelize.STRING
  },
  artist: {
    type: Sequelize.STRING
  }
});

// force: true remove a tabela se já existir
Track.sync({force: false}).then(() => console.log("Tracks table created"));
```

### Criação (INSERT)
```JavaScript 
Track.create({
  title: 'Imagine',
  artist: 'The Beatles'
});
```

### Buscar
```JavaScript 
Track.findById(1).then(t =>{
  console.log(`Achei ${t.title} - ${t.artist}`)
});

Track.
```

### Relações

#### Um para muitos

Schema:

```JavaScript
const Artist = sequelize.define('artist', {
  name: {
    type: Sequelize.STRING
  },
  genre: {
    type: Sequelize.STRING
  }
});

const Link = sequelize.define('link', {
  link_type: {
    type: Sequelize.STRING
  },
  url: {
    type: Sequelize.STRING
  }
});

Artist.hasMany(Link);

Artist.sync();
Link.sync();
```

Criação de objetos:
```JavaScript
Artist.create({name: "Anitta", genre: "Pop"}).then(anitta => {
  Link.create({
    link_type: "Spotify",
    url: "https://open.spotify.com/artist/7FNnA9vBm6EKceENgCGRMb",
    artistId: anitta.id
  });
});
```

## Aplicação Musical

 - Catálogo de músicas
  - cadastro de artista *
  - cadastro de música *
  - cadastro de links *
  - consulta catálogo


 tracks <1--n> links
 album <1--n> tracks <n--n> artists
 normalização


