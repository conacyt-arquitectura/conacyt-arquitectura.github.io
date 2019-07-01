---
title: Capa de Servicio
date: 2019-06-26 13:00:00 -06:00
position: 3
---

En la capa de servicio existen los métodos para el patrón CRUD (Create, Read, Update, Delete) y la lógica para cada uno de ellos.

```java
package com.example.service;

/**
 * Service Interface for managing {@link com.example.domain.Entity}.
 */
@Service
public interface EntityService {

   /**
     * Save a entity.
     *
     * @param entityDTO the entity to save.
     * @return the persisted entity.
     */
    EntityDTO save(EntityDTO entityDTO);

    /**
     * Get all the entities.
     *
     * @param pageable the pagination information.
     * @return the list of entities.
     */
    Page<EntityDTO> findAll(Pageable pageable);


    /**
     * Get the "id" entity.
     *
     * @param id the id of the entity.
     * @return the entity.
     */
    Optional<EntityDTO> findOne(Long id);

    /**
     * Delete the "id" entity.
     *
     * @param id the id of the entity.
     */
    void delete(Long id);

}

```

```java
package com.example.service.impl;

/**
 * Service Implementation for managing {@link com.example.domain.Entity}.
 */
@Service
@Transactional
public class EntityServiceImpl implements EntityService {

    private final Logger log = LoggerFactory.getLogger(EntityServiceImpl.class);

    private final EntityRepository entityRepository;

    private final EntityMapper entityMapper;

    public EntityService(EntityRepository entityRepository, EntityMapper entityMapper) {
        this.entityRepository = entityRepository;
        this.entityMapper = entityMapper;
    }

    /**
     * Save a entity.
     *
     * @param entityDTO the entity to save.
     * @return the persisted entity.
     */
    @Override
    public EntityDTO save(EntityDTO entityDTO) {
        log.debug("Request to save Entity : {}", entityDTO);
        Entity entity = entityMapper.toEntity(entityDTO);
        Entity = entityRepository.save(entity);
        return entityMapper.toDto(entity);
    }

    /**
     * Get all the entities.
     *
     * @param pageable the pagination information.
     * @return the list of entities.
     */
    @Override
    @Transactional(readOnly = true)
    public Page<EntityDTO> findAll(Pageable pageable) {
        log.debug("Request to get all Entities");
        return entityRepository.findAll(pageable)
            .map(entityMapper::toDto);
    }


    /**
     * Get one entity by id.
     *
     * @param id the id of the entity.
     * @return the entity.
     */
    @Override
    @Transactional(readOnly = true)
    public Optional<EntityDTO> findOne(Long id) {
        log.debug("Request to get Entity : {}", id);
        return entityRepository.findById(id)
            .map(entityMapper::toDto);
    }

    /**
     * Delete the entity by id.
     *
     * @param id the id of the entity.
     */
    @Override
    public void delete(Long id) {
        log.debug("Request to delete Entity : {}", id);
        entityRepository.deleteById(id);
    }

}

```