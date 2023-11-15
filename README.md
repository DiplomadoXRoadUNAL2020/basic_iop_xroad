# Escenario Básico de Interoperabilidad - XRoad

En este repositorio encontrará el material básico para levantar los contenedores del Servidor Central y Servidores de Seguridad de XRoad, además de un sistema de software (API Restful) basado en Golang que hace el papel del Ministerio de Tránsito en la descripción del escenario de interoperabilidad.

### Contenido

```
|

├── README.md <-- Este archivo de instrucciones

├── transito_si <-- Código fuente sistema de transito

└── docker-compose.yaml <-- Definición del stack de contenedores Docker

```

### Servicios del API (transito_si)
Los servicios que ofrece el API son:

Servicio de consulta por tipo y documento:
```
REQUEST: GET http://localhost:1002/citizen/runt-registry?document=&type=
RESPONSE (200):
{
	"hasRegistry": true, // Boolean, si existe retorna true, en caso contrario false
	"registryID": null // Opcional, si existe el registro retorna el ID
}
```

Servicio de creación de registros
```
REQUEST: POST http://localhost:1002/citizen/runt-registry/create
{
	"documentType": "", // String, tipo de documento como CC o CE
	"documentNumber": "", // String, número de documento
	"name": "", // String, nombre
	"lastname": "" // String, apellido
}
RESPONSE (200):
{
	"registryID": 1 // Integer, ID asignado al registro
}
```
### Ejecución

Ubíquese en la carpeta raíz del proyecto, descomprima el ZIP y ejecute el siguiente comando en caso que no esté aún en el mencionado directorio
```
cd basic_iop_xroad/
```
Para comprobar que esté ubicado correctamente, ejecute el siguiente comando: (en sistemas operativos basados en UNIX)
```
ls
```
O en Windows
```
dir
```
Y debería ver los dos archivos y una carpeta(transito_si) que contiene este directorio:
```
README.md  docker-compose.yml transito_si
```
Ejecute el siguiente comando para iniciar la instanciación de los contenedores:
```
docker-compose build && docker-compose up &
```
O, en caso que arroje un error de permisos (sistemas operativos basados en UNIX)
```
sudo docker-compose build && sudo docker-compose up &
```
Después, iniciará la descarga de las imágenes y la construcción de contenedores Docker para la ejecución del laboratorio. En el momento en que en su terminal vea las siguientes líneas:
```
transito_si | [GIN-debug] GET  /citizen/transit-registry --> unal.edu.co/rest-example/api/controller.GETUser (3 handlers)

transito_si | [GIN-debug] POST /citizen/transit-registry/create --> unal.edu.co/rest-example/api/controller.POSTUser (3 handlers)

transito_si | 2023/11/15 13:55:56 Listenig server 0.0.0.0:8080
```
Habrá finalizado la construcción de todos los componentes necesarios para ejecutar este laboratorio.