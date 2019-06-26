---
title: Ejemplos
date: 2019-06-26 13:05:46.559000000 -05:00
position: 12
---

## Ejemplo CRUD de la Entidad Carro

**RESOURCE**:
```
http://dads.infotec.mx/app/api/v1/carros
```
#### Operaciones CRUD
**POST** (create)
```
crea un nuevo carro
```
**GET** (read)
```
consulta la lista de carros disponibles
```
**PUT** (update)
```
actualiza uno o varios carros
```
**DELETE** (delete)
```
borra todos los carros disponibles
```

## Otros Ejemplos

A continuación, se muestran más ejemplos de peticiones HTTP utilizando los lineamientos vistos hasta el momento:


| HTTP Método | Resource Endpoint | input                       | Success Response                        | Error Response    |
|:-----------:|:-----------------:|-----------------------------|-----------------------------------------|-------------------|
| **GET**         | /polls            | Body:Empty                  | Status: 200  Body:Poll List             | Status: 500       |
| **POST**        | /polls            | Body:New Poll data          | Status:201  Body: Newly created poll id | Status: 500       |
| **PUT**         | /polls            | N/A                         | N/A                                     | Status: 400       |
| **DELETE**      | /polls            | N/A                         | N/A                                     | Status: 400       |
| **GET**         | /polls/{pollId}   | Body:Empty                  | Status: 200  Body: Poll data            | Status: 400 o 500 |
| **POST**        | /polls/{pollId}   | N/A                         | N/A                                     | Status: 400       |
| **PUT**         | /polls/{pollId}   | Body:Poll data with Updates | Status:200  Body:Empty                  | Status: 404 o 500 |
| **DELETE**      | /polls/{pollId}   | Body:Empty                  | Status:200                              | Status: 404 o 500 |

## Ejemplo de Implementación utilizando Java y Spring

Entidad : DataStore

Consultar todos los **DataStore**:

```java
    /**
     * GET /data-stores : get all the dataStores.
     *
     * @param pageable
     *            the pagination information
     * @return the ResponseEntity with status 200 (OK) and the list of
     *         dataStores in body
     */
    @GetMapping("/data-stores")
    @Timed
    public ResponseEntity<List<DataStore>> getAllDataStores(@ApiParam Pageable pageable) {
        log.debug("REST request to get a page of DataStores");
        Page<DataStore> page = dataStoreService.findAll(pageable);
        HttpHeaders headers = PaginationUtil.generatePaginationHttpHeaders(page, "/api/data-stores");
        return new ResponseEntity<>(page.getContent(), headers, HttpStatus.OK);
    }
```

Para consultar un elemento por su identificador

```java
    /**
     * GET /data-stores/:id : get the "id" dataStore.
     *
     * @param id
     *            the id of the dataStore to retrieve
     * @return the ResponseEntity with status 200 (OK) and with body the
     *         dataStore, or with status 404 (Not Found)
     */
    @GetMapping("/data-stores/{id}")
    @Timed
    public ResponseEntity<DataStore> getDataStore(@PathVariable String id) {
        log.debug("REST request to get DataStore : {}", id);
        DataStore dataStore = dataStoreService.findOne(id);
        return ResponseUtil.wrapOrNotFound(Optional.ofNullable(dataStore));
    }
```

Para crear una nueva entidad de tipo **DataStore**

```java
    /**
     * POST /data-stores : Create a new dataStore.
     *
     * @param dataStore
     *            the dataStore to create
     * @return the ResponseEntity with status 201 (Created) and with body the
     *         new dataStore, or with status 400 (Bad Request) if the dataStore
     *         has already an ID
     * @throws URISyntaxException
     *             if the Location URI syntax is incorrect
     */
    @PostMapping("/data-stores/test")
    @Timed
    public ResponseEntity<DataStore> testConnection(@Valid @RequestBody DataStore dataStore) throws URISyntaxException {
        log.info("REST connection DataStore : {}", dataStore);
        if (dataStoreService.testConnection(dataStore)) {
            return ResponseEntity.ok().headers(HeaderUtil.createSuccessDataStoreStatus(ENTITY_NAME, "ok"))
                    .body(dataStore);
        } else {
            return ResponseEntity.badRequest()
                    .headers(HeaderUtil.createFailureDataStoreStatus(ENTITY_NAME, "failure"))
                    .body(dataStore);
        }
    }

```

Para actualizar un elemento de tipo **DataStore**

```java
    /**
     * PUT /data-stores : Updates an existing dataStore.
     *
     * @param dataStore
     *            the dataStore to update
     * @return the ResponseEntity with status 200 (OK) and with body the updated
     *         dataStore, or with status 400 (Bad Request) if the dataStore is
     *         not valid, or with status 500 (Internal Server Error) if the
     *         dataStore couldnt be updated
     * @throws URISyntaxException
     *             if the Location URI syntax is incorrect
     */
    @PutMapping("/data-stores")
    @Timed
    public ResponseEntity<DataStore> updateDataStore(@Valid @RequestBody DataStore dataStore)
            throws URISyntaxException {
        log.debug("REST request to update DataStore : {}", dataStore);
        if (dataStore.getId() == null) {
            return createDataStore(dataStore);
        }
        DataStore result = dataStoreService.save(dataStore);
        return ResponseEntity.ok()
                .headers(HeaderUtil.createEntityUpdateAlert(ENTITY_NAME, dataStore.getId().toString())).body(result);
    }
```

Para borrar un recurso:

```java
    /**
     * DELETE /data-stores/:id : delete the "id" dataStore.
     *
     * @param id
     *            the id of the dataStore to delete
     * @return the ResponseEntity with status 200 (OK)
     */
    @DeleteMapping("/data-stores/{id}")
    @Timed
    public ResponseEntity<Void> deleteDataStore(@PathVariable String id) {
        log.debug("REST request to delete DataStore : {}", id);
        dataStoreService.delete(id);
        return ResponseEntity.ok().headers(HeaderUtil.createEntityDeletionAlert(ENTITY_NAME, id)).build();
    }
```
