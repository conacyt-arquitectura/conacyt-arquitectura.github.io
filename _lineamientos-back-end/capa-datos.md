---
title: Capa de Datos
date: 2019-06-26 17:00:00 -06:00
position: 7
---

La creación del modelo de datos de las entidades de dominio y el versionamiento de los cambios que sufren estas se administra con [Liquibase](https://www.liquibase.org/). A continuación se muestra un ejemplo de un archivo xml con el que se crea la tabla correspondiente a la entidad `Entity`.


```xml
<?xml version="1.0" encoding="utf-8"?>
<databaseChangeLog
    xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
    xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.6.xsd
                        http://www.liquibase.org/xml/ns/dbchangelog-ext http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-ext.xsd">

    <property name="autoIncrement" value="true"/>

    <!--
        Added the entity Entity.
    -->
    <!-- 
        El id se forma con la estampa de tiempo y un consecutivo <yyyy><mm><dd><hh><mm><ss>-<consecutivo> 
    -->
    <changeSet id="20191231245959-1" author="jhipster">
        <createTable tableName="entity">
            <column name="id" type="bigint" autoIncrement="${autoIncrement}">
                <constraints primaryKey="true" nullable="false"/>
            </column>
            <!-- Aquí se agregan más columnas -->

            <!-- jhipster-needle-liquibase-add-column - JHipster will add columns here, do not remove-->
        </createTable>

    </changeSet>

    <!-- 
        Mismo id de la creación de la tabla pero agregando 'relations' al final
    -->
    <changeSet id="20191231245959-1-relations" author="jhipster">
        <!-- Aquí se agregan las relaciones de la entidad Entity con otras entidades -->
    </changeSet>
    <!-- jhipster-needle-liquibase-add-changeset - JHipster will add changesets here, do not remove-->

    <!--
        Load sample data generated with Faker.js
        - This data can be easily edited using a CSV editor (or even MS Excel) and
          is located in the 'src/main/resources/config/liquibase/data' directory
        - By default this data is applied when running with the JHipster 'dev' profile.
          This can be customized by adding or removing 'faker' in the 'spring.liquibase.contexts'
          Spring Boot configuration key.
    -->
    <!--
        Mismo id de la creación de la tabla pero agregando 'data' al final
    -->
    <changeSet id="20191231245959-1-data" author="jhipster" context="faker">
        <loadData
                  file="config/liquibase/data/entity.csv"
                  separator=";"
                  tableName="entity">
            <column name="id" type="numeric"/>
            <!-- jhipster-needle-liquibase-add-loadcolumn - JHipster (and/or extensions) can add load columns here, do not remove-->
        </loadData>
    </changeSet>

</databaseChangeLog>
```