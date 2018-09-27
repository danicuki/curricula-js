## ActiveRecord

### Instalação
```bash
npm install --save sequelize
npm install --save sqlite3 
# npm install --save mysql2 # para MySQL
```

### Configuração

[Documentação completa](http://docs.sequelizejs.com/manual/tutorial/models-usage.html)

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
// track.js

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

Track.create({
  title: 'Trem das Cores',
  artist: 'Daniella Alcarpe'
});

```


### Buscar
```JavaScript 
Track.findById(1).then(t =>{
  console.log(`Achei ${t.title} - ${t.artist}`)
});

Track.
```

```JavaScript
Track.findAll({where: {title: 'Trem das Cores'}}).then( list => {
  if (list.length > 0) {
    console.log(`Achei '${list[0].title}' da '${list[0].artist}'`);
  }
});
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