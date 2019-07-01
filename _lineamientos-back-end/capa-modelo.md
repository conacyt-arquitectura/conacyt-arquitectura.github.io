---
title: Capa de Modelo de Dominio
date: 2019-06-26 13:00:00 -06:00
position: 5
---

Se utiliza **Java Persistence API** para anotar las entidades del negocio. 

Para ejemplificar las demás capas se utilizará la siguiente clase de dominio:

```java
package com.example.domain;

/**
* A Entity
*/
@Entity
@Table(name = "entity")
@Cache(usage = CacheConcurrencyStrategy.NONSTRICT_READ_WRITE)
public class Entity implements Serializable {

    private static final long serialVersionUID = 1L;

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) {
            return true;
        }
        if (!(o instanceof Entity)) {
            return false;
        }
        return id != null && id.equals(((Entity) o).id);
    }

    @Override
    public int hashCode() {
        return 31;
    }

    @Override
    public String toString() {
        return "Entity{" +
            "id=" + getId() +
            "}";
    }

}

```