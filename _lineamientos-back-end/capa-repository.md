---
title: Capa de Repositorio
date: 2019-06-26 13:00:00 -06:00
position: 4
---

Para crear los repositorios (o capa de acceso a datos) se prefiere el uso de la interfaz `JpaRepository` que nos proporciona métodos para el patrón CRUD (Create, Read, Update, Delete) y para consulta de entidades de manera paginada y ordenada. Además, de esta manera se pueden aprovechar los *derived queries* o consultas derivadas que son implementaciones generadas por Spring a partir de la firma del método en la interfaz.

```java
import org.springframework.data.jpa.repository.*;

@Repository
public interface EntityRepository extends JpaRepository<Entity, Long> {

    // Se creará una implementación a partir de la firma de este método
    // para consultar todas las instancias de esta Entidad 
    // que coincidan con el atributo y se ordenarán por fecha de creación
    // de manera ascendente
    List<Entity> findByAttributeOrderByCreatedDateAsc(String attribute);

}
```