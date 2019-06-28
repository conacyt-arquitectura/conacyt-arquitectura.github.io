---
title: Capa de DTO y Mappers
date: 2019-06-26 13:00:00 -06:00
position: 2
---

Se utilizan objetos DTO (Data Transfer Object) como entradas o salidas de los métodos de los controladores REST. 

```java
public class EntityDto {

    private Long id;

    public EntityDto() {
        // Vacío para su uso por Jackson
    }

    public EntityDto(Entity entity) {
        this.id = entity.getId();
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }
}
```

Para realizar el mapeo bidireccional entre entidad y DTO, se utiliza un *Mapper*

```java
/**
* Mapper bidireccional de Entity y EntityDto
*
*/
public class EntityMapper implements BaseEntityMapper<EntityDto, Entity> {

    @Override
    Entity toEntity(EntityDto dto) {
        Entity entity = new Entity();
        entity.setId(dto.getId());
        return entity;
    }

    @Override
    Dto toDto(Entity entity) {
        return new EntityDto(entity);
    }

}
```

```java
/**
* Contrato para mapper genérico de dto a entidad
* 
* @param <D> - parámetro de tipo de DTO
* @param <E> - parámetro de tipo de Entidad
*/
public interface BaseEntityMapper<D, E> {
    
    /**
    * Mapea un DTO a una entidad
    *
    * @param dto el DTO
    * @return la entidad
    */
    E toEntity(D dto);

    /**
    * Mapea una entidad a DTO
    * 
    * @param entity la entidad
    * @return el DTO
    */
    D toDto(E entity);

    /**
    * Mapea una lista de DTO a una lista de entidades
    *
    * @param dtoList la lista de DTO
    * @return la lista de entidades
    */
    default List<E> toEntity(List<D> dtoList) {
        if (dtoList == null || dtoList.isEmpty()) {
            return Collections.emptyList();
        }
        List<E> entityList = new ArrayList<>();
        for (D dto: dtoList) {
            dtoList.add(toEntity(entity));
        }
        return entityList;
    }

    /**
    * Mapea una lista de entidades a una lista de DTO
    * @param entityList la lista de entidades
    * @return la lista de DTO
    */
    default List<D> toDto(List<E> entityList) {
        if (entityList == null || entityList.isEmpty())  {
            return Collections.emptyList();
        }
        List<D> dtoList = new ArrayList<>();
        for (E entity: entityList) {
            dtoList.add(toDto(entity));
        }
        return dtoList;
    }
}
``` 