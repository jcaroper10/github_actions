En el presente documento se describirá la configuración de activo de adherencia backend.

===

<div class="menu">
  {% if config.get('plugins.page-toc.active') or attribute(page.header, 'page-toc').active %}
  <h5 style="margin-top:0px;">CONTENIDO</h5>
  <div class="page-toc">
    {% set table_of_contents = toc(page.content) %}
    {% if table_of_contents is not empty %}    
    {{ table_of_contents|raw }}
    {% endif %}
  </div>
  {% endif %}
</div>

# 1. CONTROL DE VERSIONES DEL DOCUMENTO

<div class="table_ad "></div>
|VERSIÓN|  FECHA   |DESCRIPCIÓN                                                                               |RESPONSABLE   |
|:-----:|:--------:|:-----------------------------------------------------------------------------------------|:-------------|
|1.0|06/04/2021|Activo de adherencia Backend|Samuel Ospina|
|1.1|06/04/2021|Añadido al portal de AD|Joan Peramas|

# 2. Propósito

El propósito de este documento es describir la confgiración del activo de adherencia backend.

# 3. Activo de adherencia Backend

El activo de adherencia backend es una libreria que se encarga de leer los archivo de su aplicación backend (microservicio) con la finalidad de obtener metricas respecto a los activos de backend de arquitectura digital que se usan en el proyecto.

Por el momento, solo se puede utilizar la adherencia backend en proyectos desplegados con Maven. Aún no es posible utilizarlo en despliegues con Gradle.


# 3.1. Configuración

Abrir el archivo **cfg/devops.properties** y configurar lo siguiente solo para el ambiente de desarrollo:

**PASO 1**

Añadir al dev.flow el paso de **scanstatic**:

```properties
dev.flow=scanstatic,unittest,scan,build,publish,package,delivery
```

**PASO 2**

Añadir debajo la configuración del paso:

```properties
# scanstatic
dev.stages.scanstatic.type=code
dev.stages.scanstatic.command=npm init -y && npm install @tdp/tdp-parse-java@latest && node node_modules/@tdp/tdp-parse-java/dist/src/index.js --scan --type maven
dev.stages.scanstatic.repository=genesis-npm-dev
```

**PASO 3**

Desplegar el proyecto backend en jenkis en el ambiente de desarrollo y validar que el paso de **scanstatic** paso correctamente.


![](scanstatic-1.png)