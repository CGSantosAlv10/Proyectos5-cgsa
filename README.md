# Proyecto Integrador — Automatización de APIs con Serenity BDD y Screenplay

Suite de pruebas automatizadas de API REST sobre **Fake Store API** (`https://fakestoreapi.com`) enfocada en operaciones de ventas (productos y carritos), construida con **Java 17**, **Maven**, **Cucumber**, **Serenity BDD (3.1.20)**, **REST Assured (4.3.3)** y el patrón **Screenplay**.

## Estructura del proyecto

- `src/main/java/org/example/Taks/`
    - `GetCatalogProducts.java`: Consulta el listado de productos (`GET /products`).
    - `PostSaleProduct.java`: Registra un nuevo producto (`POST /products`).
    - `GetSalesCart.java`: Consulta todos los carritos (`GET /carts`).
    - `GetCartById.java`: Consulta un carrito por ID (`GET /carts/{id}`).
- `src/main/java/org/example/Questions/`
    - `ResponseCode.java`: Obtiene y valida el código de estado HTTP de la respuesta.
    - `ResponseValue.java`: Consulta valores de la respuesta.
    - `EmptyCartResponse.java`: Verifica si la respuesta de un carrito viene vacía o `null`.
- `src/main/java/org/example/StepDefinitions/`
    - `SalesStepDefinition.java`: Mapea los pasos de Gherkin con las `Tasks` y `Questions` de Screenplay.
    - `ParameterDefinition.java`: Define tipos/parámetros para Cucumber.
- `src/test/resources/features/Sales.feature`: Escenarios Gherkin para productos y carritos.
- `src/test/java/org/example/RunnerTest.java`: Clase runner para ejecutar la suite de pruebas.
- `pom.xml`: Configuración de dependencias y plugins (`maven-failsafe-plugin` y `serenity-maven-plugin`).

## Escenarios cubiertos

1. **Consultar todos los productos de venta** (`GET /products`) — Escenario positivo: verifica código `200`.
2. **Registrar un nuevo producto de venta** (`POST /products`) — Escenario positivo: envía datos del producto y verifica código `201`.
3. **Consultar todos los carritos de venta** (`GET /carts`) — Escenario positivo: verifica código `200`.
4. **Consultar un carrito inexistente por id** (`GET /carts/999999`) — Escenario negativo: verifica código `200` y valida con `EmptyCartResponse` que el cuerpo de respuesta venga vacío o `null`.

## Requisitos previos

- **JDK 17** configurado en el entorno.
- **Apache Maven** instalado o disponible vía wrapper (`./mvnw` / `mvnw.cmd`).
- Acceso a internet para comunicarse con `https://fakestoreapi.com`.

## Ejecución de pruebas y generación del reporte

Para limpiar compilaciones anteriores, ejecutar las pruebas de integración con Failsafe y generar el reporte consolidado de Serenity:

```bash
mvn clean verify