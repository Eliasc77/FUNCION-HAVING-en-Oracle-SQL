# FUNCION-HAVING-en-Oracle-SQL
#### Nos permite seleccionar o rechazar un grupo de registros al momento de realizar una consulta en una tabla, generalmente la clausula HAVING va seguido de una condicion de busqueda para seleccionar ciertas filas retornadas x la clausula GROUP BY.
#### Having solo funciona con count ojito :d

```sql
 create table clientes (
  nombre varchar2(30) not null,
  domicilio varchar2(30),
  ciudad varchar2(20),
  provincia varchar2(20),
  telefono varchar2(11)
);

 insert into clientes
  values ('Lopez Marcos','Colon 111','Cordoba','Cordoba','null');
 insert into clientes
  values ('Perez Ana','San Martin 222','Cruz del Eje','Cordoba','4578585');
 insert into clientes
  values ('Garcia Juan','Rivadavia 333','Villa del Rosario','Cordoba','4578445');
 insert into clientes
  values ('Perez Luis','Sarmiento 444','Rosario','Santa Fe',null);
 insert into clientes
  values ('Pereyra Lucas','San Martin 555','Cruz del Eje','Cordoba','4253685');
 insert into clientes
  values ('Gomez Ines','San Martin 666','Santa Fe','Santa Fe','0345252525');
 insert into clientes
  values ('Torres Fabiola','Alem 777','Villa del Rosario','Cordoba','4554455');
 insert into clientes
  values ('Lopez Carlos',null,'Cruz del Eje','Cordoba',null);
 insert into clientes
  values ('Ramos Betina','San Martin 999','Cordoba','Cordoba','4223366');
 insert into clientes
  values ('Lopez Lucas','San Martin 1010','Posadas','Misiones','0457858745');
 ```
 
 ```sql
 select * from clientes
 ```
 
 | nombre            | domicilio           |   ciudad   |  provincia   |  telefono   |  
 | ------------------|:----------------:|----------------:| ---------:| -----------:| 
 | Lopez Marcos | Colon 111|  Cordoba |Cordoba | null |
 | Perez Ana | san Martin 222| Cruz del Eje   |Cordoba | 4578585 |
 | Garcia Juan | Rivadavia 333 |  Villa del Rosario  | Cordoba | 4578445 |
 | Perez Luis | Sarmiento 444 |  Rosario   | Santa Fe | null | 
 | Pereyra Lucas | San Martin 555 | Cruz del Eje   |Cordoba  | 4253685 |
 | Gomez Ines| San Martin 666 |  Santa Fe  |Santa Fe  | 0345252525 |
 | Torres Fabiola | Alem 777 |  Villa del Rosario | Cordoba | 4554455 | 
 | Lopez Carlos | null |  Cruz del Eje | Cordoba | null |
 | Ramos Betina | San Martin 999 |  Cordoba | Cordoba | 4223366 |
 | Lopez Lucas |  San Martin 1010   | Posadas       |  Misiones        | 0457858745|
 
 ```sql
select ciudad,provincia, count(*) as "Cantidad"
from clientes
group by ciudad, provincia;
```

|   ciudad   |  provincia   |  Cantidad   |  
| ------------------|:----------------:|----------------:|
| Cordoba |  Cordoba | 2 |
| Posadas |  Misiones | 1 |
| Villa del Rosario | Cordoba | 2 |
| Cruz del Eje   |Cordoba | 3 |
|  Rosario   | Santa Fe | 1 |
|  Santa Fe  |Santa Fe  | 1| 

____

 ```sql
select ciudad,provincia, count(*) as "Cantidad"
from clientes
group by ciudad, provincia
having count(*)>1;
```
|   ciudad   |  provincia   |  Cantidad   |  
| ------------------|:----------------:|----------------:|
| Cordoba |  Cordoba | 2 |
| Villa del Rosario | Cordoba | 2 |
| Cruz del Eje   |Cordoba | 3 |

#### filtra una cantidad especifica de registros q ya fueron agrupados al momento de hacer la consulta .

``` sql
select ciudad, count(*) from clientes
where domicilio like '%San Martin%' -- sistema busca que coincida exactamente todo el texto
group by ciudad
having count(*)<2
and ciudad <> 'Cordoba';
```
|   ciudad   |  provincia   |  Cantidad   |  
| ------------------|:----------------:|----------------:|
|  Rosario   | Santa Fe | 1 |
|  Santa Fe  |Santa Fe  | 1| 

##### va filtrar la cantidad de registros menores a 2 y excluyendo cordoba
