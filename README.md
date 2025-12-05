# no_sql_lab_sebastian-murcia
1. ¿Qué es una base de datos NoSQL y en qué se diferencia de una base de datos relacional (SQL)?
Una base de datos NoSQL es un tipo de base de datos que no usa tablas fijas ni esquemas rígidos como las BDs relacionales. Están diseñadas para manejar datos flexibles, semi-estructurados o grandes volúmenes distribuidos.
Diferencias clave:
usa tablas fijas y columnas, nosql Usa documentos, colecciones, grafos o key-value.

2. ¿Cuál es el rol de MongoDB dentro del ecosistema NoSQL?
MongoDB es una base de datos NoSQL orientada a documentos.
Guarda la información en documentos BSON (JSON binario), lo que permite almacenar datos complejos y anidados.
Por qué es adecuada para manejar JSON/BSON
El formato JSON es natural para aplicaciones web.
Permite guardar documentos con estructura variable.
Admite arrays y documentos dentro de documentos.

3. ¿Qué son una base de datos, una colección y un documento en MongoDB?
MongoDB organiza la información así:
Base de datos (database)
Es un contenedor general. Ej: tienda, hospital, juego.
Colección (collection)
Equivale a una “tabla”, pero sin esquema rígido.
Ej: productos, clientes, turnos.
Documento (document)
Es el registro en formato JSON/BSON.
Ejemplo de documento
{
  "nombre": "Laptop Gamer",
  "precio": 4500000,
  "stock": 12,
  "categoria": "Tecnología"
}

4. Ventajas del esquema flexible de MongoDB
Ventajas
No obliga a definir columnas fijas → puedes agregar nuevos campos sin alterar los demás documentos.
Se adapta a datos cambiantes → útil para apps ágiles o prototipos.
Riesgo si no se gestiona bien
Puede generar inconsistencias:
Ejemplo → documentos con campos diferentes (precio, costo, valor, etc.).

5. ¿Qué es Redis y por qué se llama “data structure server”?
Redis es una base de datos en memoria diseñada para acceder rápido.
No es solo un key-value simple, porque soporta estructuras avanzadas.
Tipos de datos que soporta :
Strings
Hashes
Lists
Sets
Sorted Sets (ZSets)
Streams
Bitmaps

6. Elegir 2 tipos de datos de Redis → uso y caso práctico
A. LISTS
Permiten almacenar listas que mantienen orden.
Comandos:
LPUSH lista valor
RPUSH lista valor
LRANGE lista 0 -1
Caso de uso:
Cola de turnos (Laboratorio).
Cada nuevo turno se agrega al final.

B. HASHES
Similares a “objetos”.
Comandos:
HSET usuario1 nombre "Juan"
HGETALL usuario1
Caso de uso:
Guardar estado rápido de un tamagochi, por ejemplo:
HSET tamagochi1 hambre 23 energia 80 humor 50

7. En el laboratorio de turnos (MongoDB + Redis)
¿Qué se guarda en MongoDB?
Los turnos históricos.
Los datos completos de cada usuario o solicitud.
Información que debe persistir.
¿Qué maneja Redis?
La cola de turnos actual (rápido acceso).
Datos temporales que cambian constantemente.
Lógica de la división
MongoDB = almacenamiento permanente.
Redis = rapidez para datos en movimiento.

8. En el laboratorio del tamagochi
¿Qué se guarda en MongoDB?

Información que no cambia tanto:

Nombre
Fecha de creación
Tipo de mascota
Historial
¿Qué va en Redis?
Valores que cambian cada segundo/minuto, por ejemplo:
hambre
energía
felicidad
temporizadores
Redis funciona como una “memoria viva”.

9. En tu propio proyecto (Mongo + Redis)
Criterio para decidir
MongoDB: información que debe quedar guardada incluso si el servidor se reinicia.
Redis: información rápida, temporal o que cambia frecuente.
Ejemplo concreto
 En MongoDB guardaría:
{
  "id": 101,
  "nombre": "Producto",
  "precio": 20000,
  "categoria": "Aseo"
}
En Redis guardaría:
stock:101 → 17
visitas:101 → 254
Mongo → datos principales
Redis → contadores, caché y estados rápidos.

10. Reflexión final
¿Cuándo usaría MongoDB como base principal?
Cuando necesito almacenar documentos estructurados y complejos.
Para proyectos con JSON natural:
→ API REST, inventarios, juegos, ecommerce.
¿Cuándo usaría Redis como apoyo?
Para acelerar las consultas (caché).
Sesiones de usuarios.
Contadores en tiempo real.
Rankings (sorted sets).
Estados que cambian rápido (como tamagochi o turnos).
Redis complementa a MongoDB para obtener un sistema rápido y persistente a la vez.




