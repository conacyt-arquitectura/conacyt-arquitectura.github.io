---
title: Capa REST
date: 2019-06-26 13:00:00 -06:00
position: 1
---

```java
public class EntityResource {
    
    private static final Logger LOG = LoggerFactory.getLogger(EntityResource.class);

    private EntityService entityService;

    private EntityMapper entityMapper;

    public EntityResource(EntityService entityService, EntityMapper entityMapper) {
        this.entityService = entityService;
        this.entityMapper = entityMapper;
    }

    @PostMapping("/entity")
    public ResponseEntity<Entity> createEntity(@Valid @RequestBody EntityDto dto) {
        LOG.debug("REST request to save entity from DTO: {}", dto);
        Entity entity = entityMapper.toEntity(dto);
        if (dto.getId() != null) {
            entity = entityService.save(entity);
        }
        return ResponseEntity.created(new URI("/api/entity/" + entity.getId()))
        .headers(HeaderUtil.createEntityAlert(applicationName, "es", ENTITY_NAME, entity.getId().toString()))
        .body(entity);
    }
}
```