---
title: Capa REST
date: 2019-06-26 13:00:00 -06:00
position: 1
---

```java
package com.example.web.rest;

/**
 * REST controller for managing {@link com.example.domain.Entity}.
 */
@RestController
@RequestMapping("/api")
public class EntityResource {
    
    private final Logger log = LoggerFactory.getLogger(EntityResource.class);

    private static final String ENTITY_NAME = "solicitud";

    @Value("${jhipster.clientApp.name}")
    private String applicationName;

    private final EntityService entityService;

    private final EntityMapper entityMapper;

    public EntityResource(EntityService entityService, EntityMapper entityMapper) {
        this.entityService = entityService;
        this.entityMapper = entityMapper;
    }

    /**
     * {@code POST  /entities} : Create a new entity.
     *
     * @param entityDTO the entityDTO to create.
     * @return the {@link ResponseEntity} with status {@code 201 (Created)} and with body the new entityDTO, or with status {@code 400 (Bad Request)} if the entity has already an ID.
     * @throws URISyntaxException if the Location URI syntax is incorrect.
     */
    @PostMapping("/entity")
    public ResponseEntity<EntityDTO> createEntity(@Valid @RequestBody EntityDto entityDTO) throws URISyntaxException {
        log.debug("REST request to save entity : {}", entityDTO);
        if (entityDTO.getId() != null) {
            throw new BadRequestAlertException("A new entity cannot already have an ID", ENTITY_NAME, "idexists");
        }
        EntityDTO entity = entityService.save(entityDTO);
        return ResponseEntity.created(new URI("/api/entity/" + entity.getId()))
        .headers(HeaderUtil.createEntityAlert(applicationName, "es", ENTITY_NAME, entity.getId().toString()))
        .body(entity);
    }

    /**
     * {@code PUT  /entities} : Updates an existing entity.
     *
     * @param entityDTO the entityDTO to update.
     * @return the {@link ResponseEntity} with status {@code 200 (OK)} and with body the updated entityDTO,
     * or with status {@code 400 (Bad Request)} if the entityDTO is not valid,
     * or with status {@code 500 (Internal Server Error)} if the entityDTO couldn't be updated.
     * @throws URISyntaxException if the Location URI syntax is incorrect.
     */
    @PutMapping("/entities")
    public ResponseEntity<EntityDTO> updateEntity(@RequestBody EntityDTO entityDTO) throws URISyntaxException {
        log.debug("REST request to update Entity : {}", entityDTO);
        if (entityDTO.getId() == null) {
            throw new BadRequestAlertException("Invalid id", ENTITY_NAME, "idnull");
        }
        EntityDTO result = entityService.save(entityDTO);
        return ResponseEntity.ok()
            .headers(HeaderUtil.createEntityUpdateAlert(applicationName, true, ENTITY_NAME, entityDTO.getId().toString()))
            .body(result);
    }

    /**
     * {@code GET  /entities} : get all the entities.
     *
     * @param pageable the pagination information.
     * @param queryParams a {@link MultiValueMap} query parameters.
     * @param uriBuilder a {@link UriComponentsBuilder} URI builder.
     * @param criteria the criteria which the requested entities should match.
     * @return the {@link ResponseEntity} with status {@code 200 (OK)} and the list of entities in body.
     */
    @GetMapping("/entities")
    public ResponseEntity<List<EntityDTO>> getAllEntities(EntityCriteria criteria, Pageable pageable, @RequestParam MultiValueMap<String, String> queryParams, UriComponentsBuilder uriBuilder) {
        log.debug("REST request to get Entities by criteria: {}", criteria);
        Page<EntityDTO> page = entityQueryService.findByCriteria(criteria, pageable);
        HttpHeaders headers = PaginationUtil.generatePaginationHttpHeaders(uriBuilder.queryParams(queryParams), page);
        return ResponseEntity.ok().headers(headers).body(page.getContent());
    }

    /**
    * {@code GET  /entities/count} : count all the entities.
    *
    * @param criteria the criteria which the requested entities should match.
    * @return the {@link ResponseEntity} with status {@code 200 (OK)} and the count in body.
    */
    @GetMapping("/entities/count")
    public ResponseEntity<Long> countEntities(EntityCriteria criteria) {
        log.debug("REST request to count Entities by criteria: {}", criteria);
        return ResponseEntity.ok().body(entityQueryService.countByCriteria(criteria));
    }

    /**
     * {@code GET  /entities/:id} : get the "id" entity.
     *
     * @param id the id of the entityDTO to retrieve.
     * @return the {@link ResponseEntity} with status {@code 200 (OK)} and with body the entityDTO, or with status {@code 404 (Not Found)}.
     */
    @GetMapping("/entities/{id}")
    public ResponseEntity<EntityDTO> getEntity(@PathVariable Long id) {
        log.debug("REST request to get Entity : {}", id);
        Optional<EntityDTO> entityDTO = entityService.findOne(id);
        return ResponseUtil.wrapOrNotFound(entityDTO);
    }

    /**
     * {@code DELETE  /entities/:id} : delete the "id" entity.
     *
     * @param id the id of the entityDTO to delete.
     * @return the {@link ResponseEntity} with status {@code 204 (NO_CONTENT)}.
     */
    @DeleteMapping("/entities/{id}")
    public ResponseEntity<Void> deleteEntity(@PathVariable Long id) {
        log.debug("REST request to delete Entity : {}", id);
        entityService.delete(id);
        return ResponseEntity.noContent().headers(HeaderUtil.createEntityDeletionAlert(applicationName, true, ENTITY_NAME, id.toString())).build();
    }
}
```