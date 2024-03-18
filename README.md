# mongo.studio

 bbdd documentales ("no-sql") vs bbdd sql

- [X] [base de datos no sql](https://es.wikipedia.org/wiki/NoSQL)
- [x] documento [json estructura](https://www.mclibre.org/consultar/informatica/lecciones/formato-json.html)





- [ ] .
- [ ] .
- [ ] .
- [ ] 


## equivalencia de dos esquemas


sql: empleado(nombre,IDjefe)

empleado (estado1)
| E  |  J   |
|:--:|:----:|
| E1 |  E2  |
| E2 |  E3  |
| E3 | null |
| E4 |  E2  |

empleado (estado2)
| E  |  J   |
|:--:|:----:|
| E1 |  E2  |
| E2 | null |
| E3 |  E2  |
| E4 |  E2  |

documento (estado1)
{"E1":"E2","E2":"E3","E3":NULL,"E4":"E2"}

documento (estado2)
{"E1":"E2","E2": NULL,"E3":E2,"E4":"E2"}




















