---
title: Capa de Servicio
date: 2019-06-26 13:00:00 -06:00
position: 3
---

En la capa de servicio existen los métodos para el patrón CRUD (Create, Read, Update, Delete) y la lógica para cada uno de ellos.

```java
/**
* Implementación de Servicio para administrar {@link Entity}
*
*/
@Service
public class EntityService {

    private static final Logger LOG = LoggerFactory.getLogger(EntityService.class);

    EntityRepository entityRepository;

    public EntityService(EntityRepository entityRepository) {
        this.entityRepository = entityRepository;
    }

    /**
    * Guarda una entity
    *
    * @param entity la entidad a guardar
    * @return la entidad persistida
    */
    public Entity save(Entity entity) {
        LOG.debug("Request to save entity: {}", entity);
        return entityRepository.save(entity);
    }

    /**
    * Obtiene todas las entidades
    *
    * @param pageable la información de la paginación
    * @return la lista de entidades
    */
    public Page<Entity> findAll(Pageable pageable) {
        LOG.debug("Request to get all entities");
        return entityRepository.findAll(pageable);
    }

    /**
    * Obtiene la entidad por id
    *
    * @param id el id de la entidad
    * @return la entidad
    */
    public Optional<Entity> findOne(Long id) {
        LOG.debug("Request to get Entity : {}", id);
        return entityRepository.findOne(id);
    }

    /**
    * Borra la entidad por id
    *
    * @param id el id de la entidad
    */
    public void delete(Long id) {
        LOG.debug("Request to delete Entity: {}", id);
        return entityRepository.delete(id);
    }

}

```