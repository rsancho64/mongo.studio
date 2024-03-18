# mongo.studio

 bbdd documentales ("no-sql") vs bbdd sql

- [X] [base de datos no sql](https://es.wikipedia.org/wiki/NoSQL)
- [x] documento [json estructura](https://www.mclibre.org/consultar/informatica/lecciones/formato-json.html)
- [X] cli mongo install
- [X] cli [mongo example](https://www.digitalocean.com/community/tutorials/how-to-use-the-mongodb-shell)
- [ ] .

## equivalencia de dos esquemas

sql: `empleado(nombre, IDjefe)`

tabla empleado (estado1)
|   E   |   J   |
| :---: | :---: |
|  E1   |  E2   |
|  E2   |  E3   |
|  E3   | null  |
|  E4   |  E2   |

tabla empleado (estado2)
|   E   |   J   |
| :---: | :---: |
|  E1   |  E2   |
|  E2   | null  |
|  E3   |  E2   |
|  E4   |  E2   |

documento empleado (estado1)
`{"E1":"E2","E2":"E3","E3":NULL,"E4":"E2"}`

documento empleado (estado2)
`{"E1":"E2","E2": NULL,"E3":E2,"E4":"E2"}`

## ubuntu install mongo

[recipe](https://blog.stackademic.com/mongodb-cluster-setup-on-ubuntu-23-04-x64-223193fcdb5e)

```sh
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2_amd64.deb;
sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2_amd64.deb;
# apt update;
# apt install libssl1.1;

echo "deb [ arch=amd64,arm64,trusted=yes ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list;
# see https://askubuntu.com/questions/732985/force-update-from-unsigned-repository
sudo apt update;
sudo apt install -y mongodb-org;

sudo systemctl enable mongod;
sudo systemctl start  mongod;
sudo systemctl status mongod;

mongosh
```

```json
// > 
// > use nueva // new prompt: "nueva>"
db.dropDatabase()                    // vaciado 
db.nueva.insert({"yaya":"Alicia"});  // inserción ----------
db.nueva.find();
db.nueva.insert({"yayo":"Angel"});   // inserción ----------
db.nueva.find();
db.nueva.find({ mama: { $exists: true } }); // consulta con selección ----------
db.nueva.find({ yaya: { $exists: true } }); // consulta con selección ----------
db.nueva.insert({"yaya":"Felicidad"});      // inserción de una k repetida ? ----------
db.nueva.find();
// [
//   { _id: ObjectId('65f8a02e3e1857c6dddb83b6'), yaya: 'Alicia' },
//   { _id: ObjectId('65f8a0323e1857c6dddb83b7'), yayo: 'Angel' },
//   { _id: ObjectId('65f8a06b3e1857c6dddb83b8'), yaya: 'Felicidad' }
// ]
// ... no: no hay tal clave repetida, es la misma clave en dos diccionarios distintos.
// la BD 'nueva' tiene ahora tres objetos que son diccionarios.
```

## Volcado a bson

```bash
mongodump
# 2024-03-18T21:26:53.460+0100 writing admin.system.version to dump/admin/system.version.bson
# 2024-03-18T21:26:53.461+0100 done dumping admin.system.version (1 document)
# 2024-03-18T21:26:53.461+0100 writing nueva.nueva to dump/nueva/nueva.bson
# 2024-03-18T21:26:53.462+0100 done dumping nueva.nueva (3 documents)
tree dump
# dump
# ├── admin
# │   ├── system.version.bson
# │   └── system.version.metadata.json
# └── nueva
#     ├── nueva.bson
#     └── nueva.metadata.json
file dump/nueva/nueva.bson            # data (not text)
file dump/nueva/nueva.metadata.json   # json text (meta!)data (try cat)
rm -Rf dump/
mongosh
```

```json
use nueva
db.nueva.insert({"mama":"Beatriz"}); // inserción ----------
db.nueva.insert({"papa":"Ramon"});   // inserción ----------
exit
```

```bash
mongodump
mongosh
```

```json
db.dropDatabase()  // vaciado 
db.nueva.find();   // vacia
exit
```

## Restauración desde bson

```bash
mongorestore -d nueva ./dump/nueva/
# 2024-03-18T21:43:08.684+0100 The --db and --collection flags are deprecated for this use-case; please use --nsInclude instead, i.e. with --nsInclude=${DATABASE}.${COLLECTION}
# 2024-03-18T21:43:08.684+0100 building a list of collections to restore from dump/nueva dir
# 2024-03-18T21:43:08.684+0100 reading metadata for nueva.nueva from dump/nueva/nueva.metadata.json
# 2024-03-18T21:43:08.700+0100 restoring nueva.nueva from dump/nueva/nueva.bson
# 2024-03-18T21:43:08.711+0100 finished restoring nueva.nueva (3 documents, 0 failures)
# 2024-03-18T21:43:08.711+0100 no indexes to restore for collection nueva.nueva
# 2024-03-18T21:43:08.711+0100 5 document(s) restored successfully. 0 document(s) failed to restore.
mongosh
```

```json
use nueva
db.nueva.find() // : restaurada.
```

## MongoDB GUI client

[What is a good one?](https://askubuntu.com/questions/196136/what-is-a-good-mongodb-gui-client)?

- [ ] try *Robo 3T* (**Studio 3T**) (antes RoboMongo) ,, wget (ubuntu): `studio-3t-linux-x64.tar`
  - [X] [intall tar](https://studio3t.com/knowledge-base/articles/how-to-install-studio-3t-on-linux/)
  
```sh
tar -xvzf studio-3t-linux-x64.tar.gz   # unpack
./studio-3t-linux-x64.sh # run installer ...
```  
- [X] EULA ... 30 d.trial ; downgrade to free

```sh
ls /home/ray/studio3t/Studio-3T # run
```

- [ ] get url de conexion a la bd local al lanzar el CLI client (`mongosh`) :
Connecting to: `mongodb://127.0.0.1:27017/`

## TO DO: WORK WITH A SQL (rdb) SCHEMA (1 TABLA)

### TO DO: DOS TABLAS (CON UN VINCULO FK)

### TO DO: CONVERTIR A ESQUEMA DOCUMENTAL

