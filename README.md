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
| E  |  J   |
|:--:|:----:|
| E1 |  E2  |
| E2 |  E3  |
| E3 | null |
| E4 |  E2  |

tabla empleado (estado2)
| E  |  J   |
|:--:|:----:|
| E1 |  E2  |
| E2 | null |
| E3 |  E2  |
| E4 |  E2  |

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

# uso
mongosh
> use nueva
nueva> db.nueva.insert({"mama":"Feli"});
# {
#   acknowledged: true,
#   insertedIds: { '0': ObjectId('65f850a93e1857c6dddb83b2') }
# }
nueva> db.nueva.find()
# [ { _id: ObjectId('65f850a93e1857c6dddb83b2'), mama: 'Feli' } ]
nueva> db.nueva.insert({"papa":"Basilio"});
# {
#   acknowledged: true,
#   insertedIds: { '0': ObjectId('65f850c13e1857c6dddb83b3') }
# }
nueva> db.nueva.find()
# [
#   { _id: ObjectId('65f850a93e1857c6dddb83b2'), mama: 'Feli' },
#   { _id: ObjectId('65f850c13e1857c6dddb83b3'), papa: 'Basilio' }
# ]
