---
title: Capa de Modelo de Dominio
date: 2019-06-26 13:00:00 -06:00
position: 5
---

Se utiliza **Java Persistence API** para anotar las entidades del negocio. 

Para ejemplificar las demás capas se utilizará la siguiente clase de dominio:
```java
@Entity
@Table(name = "entities")
public class Entity implements Serializable {

    private static final long serialVersionUID = 1L;

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @SequenceGenerator(name = "sequenceGenerator")
    private Long id;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }


}

```