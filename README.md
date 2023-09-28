# Design Document: API REST CONTACTOS

## 1. Descripcion
Ejemplo de una API REST para  gestionar contactos en una DB utilizando FastAPI


## 2. Objetivo
Realizar un ejemplo de diseño de una API REST de tipo CRUD y su posterior codificacion utilizando el framework [FastAPI]( https://fastapi.tiangolo.com/)

## 3. Diseño de la BD
Para este ejemplo se utilizara el gestor de base de datos [SQLite3]( https://sqlite.org/) con las siguientes tablas :

3.1 Tabla :contactos
|||||

3.2 Script
CREATE TABLE IF NOT EXISTS contactos ( id_contacto INTEGER PRIMARY KEY, nombre VARCHAR(100) NOT NULL, primer_apellido VARCHAR(50) NOT NULL, segundo_apellido VARCHAR(50) NOT NULL, email VARCHAR(100) NOT NULL, telefono VARCHAR(13) NOT NULL );

## 4. Diseño del Endpoint

Diseño del end para el recurso contactos

4.1 Mostrar todos los contactos

## 1. Endpoint para obtener todos los contactos

| No. | Propiedad        | Detalle                                           |
| --- | ---------------- | ------------------------------------------------- |
| 1   | Description      | Endpoint para obtener todos los contactos       |
| 2   | Summary          | Endpoint todos los contactos                     |
| 3   | Method           | GET                                               |
| 4   | Endpoint         | `http://localhost:8000/contactos`                |
| 5   | Query Params     | `?limit=10&offset=10`                            |
| 6   | Path Param       | NA                                                |
| 7   | Data             | NA                                                |
| 8   | Version          | v1                                               |
| 9   | Status Code      | 200                                              |
| 10  | Response type    | `application/json`                               |
| 11  | Response         | `[{"id_contacto":int,"nombre":string,...}]`      |
| 12  | Curl             | `curl -X "GET" "http://localhost:8000/contactos?limit=10&offset=10" -H "accept:application/json"` |
| 13  | Status Code (error) | 429                                        |
| 14  | Response Type (error) | `application/json`                           |
| 15  | Response (error) | `{"message":"No hay registros"}`                  |

## 4.2 Buscar contactos por nombre

| No. | Propiedad        | Detalle                                           |
| --- | ---------------- | ------------------------------------------------- |
| 1   | Description      | Endpoint para obtener contactos por nombre       |
| 2   | Summary          | Endpoint contactos obtener por nombre            |
| 3   | Method           | GET                                               |
| 4   | Endpoint         | `http://localhost:8000/contactos`                |
| 5   | Query Params     | `?limit=10&offset=10&nombre={nombre}`            |
| 6   | Path Param       | NA                                                |
| 7   | Data             | NA                                                |
| 8   | Version          | v1                                               |
| 9   | Status Code      | 200                                              |
| 10  | Response type    | `application/json`                               |
| 11  | Response         | `[{"id_contacto":int,"nombre":string,...}]`      |
| 12  | Curl             | `curl -X "GET" "http://localhost:8000/contactos?limit=10&offset=10&nombre={nombre}" -H "accept:application/json"` |
| 13  | Status Code (error) | 432                                        |
| 14  | Response Type (error) | `application/json`                           |
| 15  | Response (error) | `{"message":"Contacto no encontrado"}`           |
| 16  | Status Code (error) | 433                                        |
| 17  | Response Type (error) | `application/json`                           |
| 18  | Response (error) | `{"message":"Parámetro vacío"}`                 |

## 4.3 Actualizar contactos por id_contacto

| No. | Propiedad        | Detalle                                           |
| --- | ---------------- | ------------------------------------------------- |
| 1   | Description      | Endpoint para editar los contactos por su id_contacto |
| 2   | Summary          | Endpoint contactos editar id_contacto             |
| 3   | Method           | PUT                                               |
| 4   | Endpoint         | `http://localhost:8000/contactos/{id_contacto}`     |
| 5   | Query Params     | NA                                                |
| 6   | Path Param       | `/{id_contacto}`                                   |
| 7   | Data             | `{"id_contacto":int,"nombre":string,...}`          |
| 8   | Version          | v1                                               |
| 9   | Status Code      | 202                                              |
| 10  | Response type    | `application/json`                               |
| 11  | Response         | `{"message":"Contacto actualizado"}`                |
| 12  | Curl             | `curl -X "PUT" "http://localhost:8000/contactos/{id_contacto}" -H "accept:application/json" -d "{"id_contacto": int, "nombre": string, ...}"` |
| 13  | Status Code (error) | 432                                       |
| 14  | Response Type (error) | `application/json`                          |
| 15  | Response (error) | `{"message":"Contacto no encontrado"}`             |
| 16  | Status Code (error) | 434                                       |
| 17  | Response Type (error) | `application/json`                          |
| 18  | Response (error) | `{"message":"Parámetros vacíos"}`                  |

## 4.4 Crear contactos

| No. | Propiedad        | Detalle                                           |
| --- | ---------------- | ------------------------------------------------- |
| 1   | Description      | Endpoint para crear contactos                     |
| 2   | Summary          | Endpoint contactos crear                          |
| 3   | Method           | POST                                              |
| 4   | Endpoint         | `http://localhost:8000/contactos`                |
| 5   | Query Params     | NA                                                |
| 6   | Path Param       | NA                                                |
| 7   | Data             | `{"nombre":string,"apellido_paterno":string,...}` |
| 8   | Version          | v1                                               |
| 9   | Status Code      | 201                                              |
| 10  | Response type    | `application/json`                               |
| 11  | Response         | `{"message":"Contacto creado"}`                   |
| 12  | Curl             | `curl -X "POST" "http://localhost:8000/contactos" -H "accept:application/json" -d "{"nombre": string, "apellido_paterno": string, ...}"` |
| 13  | Status Code (error) | 432                                       |
| 14  | Response Type (error) | `application/json`                          |
| 15  | Response (error) | `{"message":"Contacto no encontrado"}`             |
| 16  | Status Code (error) | 434                                       |
| 17  | Response Type (error) | `application/json`                          |
| 18  | Response (error) | `{"message":"Parámetros vacíos"}`                  |

## 4.5 Eliminar contactos por id_contacto

| No. | Propiedad        | Detalle                                           |
| --- | ---------------- | ------------------------------------------------- |
| 1   | Description      | Endpoint para eliminar los contactos por su id_contacto |
| 2   | Summary          | Endpoint contactos eliminar id_contacto          |
| 3   | Method           | DELETE                                           |
| 4   | Endpoint         | `http://localhost:8000/contactos/{id_contacto}`     |
| 5   | Query Params     | NA                                                |
| 6   | Path Param       | `/{id_contacto}`                                   |
| 7   | Data             | `{"id_contacto":int}`                            |
| 8   | Version          | v1                                               |
| 9   | Status Code      | 207                                              |
| 10  | Response type    | `application/json`                               |
| 11  | Response         | `{"message":"Contacto eliminado"}`                |
| 12  | Curl             | `curl -X "DELETE" "http://localhost:8000/contactos/{id_contacto}" -H "accept:application/json" -d "{"id_contacto": int}"` |
| 13  | Status Code (error) | 432                                       |
| 14  | Response Type (error) | `application/json`                          |
| 15  | Response (error) | `{"message":"Contacto no encontrado"}`             |
| 16  | Status Code (error) | 434                                       |
| 17  | Response Type (error) | `application/json`                          |
| 18  | Response (error) | `{"message":"Parámetro vacío"}`                   |
## 4.5 Eliminar contactos por id_contacto

| No. | Propiedad        | Detalle                                           |
| --- | ---------------- | ------------------------------------------------- |
| 1   | Description      | Endpoint para eliminar los contactos por su id_contacto |
| 2   | Summary          | Endpoint contactos eliminar id_contacto          |
| 3   | Method           | DELETE                                           |
| 4   | Endpoint         | `http://localhost:8000/contactos/{id_contacto}`     |
| 5   | Query Params     | NA                                                |
| 6   | Path Param       | `/{id_contacto}`                                   |
| 7   | Data             | `{"id_contacto":int}`                            |
| 8   | Version          | v1                                               |
| 9   | Status Code      | 207                                              |
| 10  | Response type    | `application/json`                               |
| 11  | Response         | `{"message":"Contacto eliminado"}`                |
| 12  | Curl             | `curl -X "DELETE" "http://localhost:8000/contactos/{id_contacto}" -H "accept:application/json" -d "{"id_contacto": int}"` |
| 13  | Status Code (error) | 432                                       |
| 14  | Response Type (error) | `application/json`                          |
| 15  | Response (error) | `{"message":"Contacto no encontrado"}`             |
| 16  | Status Code (error) | 434                                       |
| 17  | Response Type (error) | `application/json`                          |
| 18  | Response (error) | `{"message":"Parámetro vacío"}`                   |
