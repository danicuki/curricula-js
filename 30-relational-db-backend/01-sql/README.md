## Ambiente

 - DataGrip

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
