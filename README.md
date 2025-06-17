# Notas: Fetch API - Obtener Categorías de Comida

## Código Original
```javascript
function iniciarApp() {
    obtenerCategorias()

    function obtenerCategorias() {
        const url = 'https://www.themealdb.com/api/json/v1/1/categories.php'
        fetch(url)
            .then(respuesta => respuesta.json())
            .then(resultado => console.log(resultado))
    }
}

document.addEventListener('DOMContentLoaded', iniciarApp)
```

## Explicación Paso a Paso

### 1. Inicialización de la App
```javascript
document.addEventListener('DOMContentLoaded', iniciarApp)
```
- **¿Qué hace?** Espera a que el DOM esté completamente cargado antes de ejecutar la aplicación
- **¿Por qué es importante?** Garantiza que todos los elementos HTML estén disponibles antes de manipularlos
- **Analogía:** Es como esperar a que todas las piezas de un rompecabezas estén sobre la mesa antes de empezar a armarlo

### 2. Función Principal
```javascript
function iniciarApp() {
    obtenerCategorias()
}
```
- **Propósito:** Punto de entrada de la aplicación
- **Patrón:** Función orquestadora que coordina las operaciones principales

### 3. Petición HTTP con Fetch
```javascript
function obtenerCategorias() {
    const url = 'https://www.themealdb.com/api/json/v1/1/categories.php'
    fetch(url)
        .then(respuesta => respuesta.json())
        .then(resultado => console.log(resultado))
}
```

#### Desglose del Fetch:
- **`fetch(url)`**: Inicia la petición HTTP GET al endpoint
- **`.then(respuesta => respuesta.json())`**: Convierte la respuesta en formato JSON
- **`.then(resultado => console.log(resultado))`**: Maneja los datos obtenidos

## Conceptos Clave del Fetch API

### Promesas (Promises)
- Fetch devuelve una **Promise** que representa una operación asíncrona
- Las promesas pueden estar en 3 estados:
  - **Pending:** La operación está en progreso
  - **Fulfilled:** La operación se completó exitosamente
  - **Rejected:** La operación falló

### Método .then()
- Se ejecuta cuando la promesa se resuelve exitosamente
- Permite encadenar operaciones asíncronas
- Cada `.then()` devuelve una nueva promesa

## Versión Mejorada con Manejo de Errores

```javascript
function iniciarApp() {
    obtenerCategorias()

    async function obtenerCategorias() {
        const url = 'https://www.themealdb.com/api/json/v1/1/categories.php'
        
        try {
            const respuesta = await fetch(url)
            
            if (!respuesta.ok) {
                throw new Error(`Error HTTP: ${respuesta.status}`)
            }
            
            const resultado = await respuesta.json()
            console.log('Categorías obtenidas:', resultado)
            
        } catch (error) {
            console.error('Error al obtener categorías:', error)
        }
    }
}

document.addEventListener('DOMContentLoaded', iniciarApp)
```

## Mejoras Implementadas

### 1. Async/Await
- **Ventaja:** Código más legible y fácil de debuggear
- **Analogía:** En lugar de una cadena de promesas (como una escalera), tienes un código que se lee de arriba hacia abajo (como un ascensor)

### 2. Manejo de Errores
```javascript
if (!respuesta.ok) {
    throw new Error(`Error HTTP: ${respuesta.status}`)
}
```
- **Propósito:** Verificar si la respuesta del servidor es exitosa (status 200-299)
- **¿Por qué?** Fetch no rechaza automáticamente para códigos de error HTTP

### 3. Try/Catch
- **Función:** Captura y maneja cualquier error que pueda ocurrir
- **Incluye:** Errores de red, errores de parsing JSON, errores HTTP

## Estructura de la Respuesta de la API

La API de TheMealDB devuelve un objeto con esta estructura:
```javascript
{
    "categories": [
        {
            "idCategory": "1",
            "strCategory": "Beef",
            "strCategoryThumb": "https://...",
            "strCategoryDescription": "Beef is the culinary name..."
        },
        // ... más categorías
    ]
}
```