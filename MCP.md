# Model Context Protocol (MCP)

## Índice

- [Introducción a MCP](#introducción-a-mcp)
- [Origen y desarrollo](#origen-y-desarrollo)
- [Ventajas de MCP](#ventajas-de-mcp)
- [Desventajas de MCP](#desventajas-de-mcp)
- [Arquitectura de MCP](#arquitectura-de-mcp)
- [Usando MCP con Claude Desktop](#usando-mcp-con-claude-desktop)
  - [Requisitos previos](#requisitos-previos)
  - [Instalación](#instalación)
  - [Configuración](#configuración)
  - [Ejemplos de uso](#ejemplos-de-uso)
    - [MCP de Filesystem](#mcp-de-filesystem)
    - [MCP de PostgreSQL](#mcp-de-postgresql)
    - [MCP de Brave Search](#mcp-de-brave-search)
- [Referencias](#referencias)

## Introducción a MCP

El Model Context Protocol (MCP) es un estándar emergente en el ecosistema de inteligencia artificial que permite a los modelos de lenguaje de gran tamaño (LLMs) interactuar directamente con sistemas externos y herramientas. MCP funciona como un "puente" que conecta los modelos de IA con el mundo exterior, expandiendo significativamente sus capacidades más allá del procesamiento de texto.

En esencia, MCP permite que los modelos como Claude puedan:

- Acceder a información actualizada a través de búsquedas web
- Interactuar con sistemas de archivos
- Consultar bases de datos
- Controlar navegadores web
- Utilizar APIs externas
- Y muchas otras interacciones con sistemas y servicios

Esto transforma a los LLMs de simples procesadores de texto a asistentes capaces de realizar acciones concretas en el mundo digital, permitiéndoles resolver problemas más complejos con acceso a datos actualizados y recursos externos.

![Diagrama conceptual de MCP]()

## Origen y desarrollo

MCP surgió como respuesta a una limitación fundamental de los modelos de lenguaje: su incapacidad para interactuar directamente con sistemas externos. Aunque los LLMs son excelentes procesando y generando texto, tradicionalmente han sido "aislados" - limitados a trabajar con la información proporcionada en el prompt y su conocimiento pre-entrenado.

El desarrollo de MCP comenzó cuando empresas como Anthropic (creadores de Claude) y otras organizaciones en el espacio de IA reconocieron la necesidad de un protocolo estandarizado que permitiera a los modelos de lenguaje:

1. **Solicitar información externa** cuando su conocimiento interno fuera insuficiente
2. **Ejecutar acciones específicas** en sistemas externos cuando fuera necesario
3. **Mantener un flujo bidireccional de información** entre el modelo y herramientas externas

Los primeros pasos hacia MCP se vieron en implementaciones como el "function calling" de OpenAI y las capacidades de herramientas de otros modelos, pero MCP representa un esfuerzo para estandarizar estos enfoques en un protocolo coherente que pueda ser implementado de manera consistente en diferentes plataformas y modelos.

El desarrollo de MCP ha sido impulsado por la visión de crear asistentes de IA más útiles, precisos y capaces, que puedan funcionar como colaboradores efectivos en una amplia gama de tareas, superando las limitaciones inherentes de los modelos tradicionales.

## Ventajas de MCP

La implementación de MCP ofrece numerosas ventajas tanto para desarrolladores como para usuarios finales:

### 1. Acceso a información actualizada

- Los modelos pueden buscar en tiempo real información actual, superando las limitaciones de su fecha de corte de conocimiento
- Permite respuestas precisas sobre eventos recientes, datos actualizados y tendencias emergentes

### 2. Capacidades ampliadas

- Transformación de los LLMs de simples generadores de texto a agentes capaces de realizar acciones concretas
- Posibilidad de realizar tareas complejas que requieren interacción con sistemas externos

### 3. Mayor precisión

- Reducción significativa de alucinaciones al permitir que el modelo verifique información en fuentes externas
- Capacidad para citar fuentes de información concretas y actuales

### 4. Flexibilidad y extensibilidad

- Arquitectura modular que permite añadir nuevas herramientas y capacidades según sea necesario
- Adaptabilidad a diferentes casos de uso y dominios específicos

### 5. Mejora de la experiencia del usuario

- Interacciones más naturales y efectivas al permitir que el modelo resuelva problemas de extremo a extremo
- Menor necesidad de cambiar entre diferentes aplicaciones para completar tareas complejas

### 6. Potencial para automatización

- Posibilidad de automatizar flujos de trabajo complejos que antes requerían intervención humana
- Capacidad para orquestar diferentes sistemas y herramientas de manera coherente

### 7. Desarrollo más rápido de aplicaciones de IA

- Estandarización que facilita la implementación de capacidades avanzadas
- Reducción del tiempo necesario para desarrollar aplicaciones de IA con capacidades de interacción con el mundo exterior

![Comparación de capacidades con y sin MCP]()

## Desventajas de MCP

A pesar de sus numerosas ventajas, el uso de MCP también presenta algunos desafíos y limitaciones:

### 1. Consideraciones de seguridad

- Otorgar a los modelos acceso a sistemas externos aumenta la superficie de ataque potencial
- Necesidad de implementar medidas de seguridad robustas para prevenir usos malintencionados

### 2. Complejidad técnica

- Mayor complejidad en la implementación y mantenimiento de sistemas que utilizan MCP
- Curva de aprendizaje para desarrolladores al integrar múltiples herramientas y servicios

### 3. Dependencias externas

- Vulnerabilidad ante fallos en servicios externos o APIs de terceros
- Problemas potenciales de disponibilidad si los servicios externos no funcionan correctamente

### 4. Consideraciones de privacidad

- Riesgos potenciales al permitir que modelos accedan a datos sensibles o personales
- Necesidad de implementar controles de acceso y políticas de privacidad rigurosas

### 5. Inconsistencia entre implementaciones

- Diferencias en cómo distintas plataformas implementan el protocolo MCP
- Posibles problemas de compatibilidad entre diferentes sistemas

### 6. Costos adicionales

- Mayor consumo de recursos computacionales al interactuar con sistemas externos
- Posibles costos asociados con el uso de APIs y servicios de terceros

### 7. Problemas de latencia

- Tiempos de respuesta potencialmente más largos debido a la necesidad de interactuar con sistemas externos
- Experiencia de usuario afectada por retrasos en las respuestas

## Arquitectura de MCP

La arquitectura de Model Context Protocol (MCP) se basa en un diseño modular que facilita la comunicación bidireccional entre los modelos de lenguaje y una variedad de herramientas y sistemas externos. A continuación se describen los componentes principales:

### Componentes clave

1. **Runtime MCP**: Actúa como capa intermedia entre el modelo de lenguaje y las herramientas externas, gestionando el flujo de información y la ejecución de comandos.

2. **Modelo de lenguaje (LLM)**: El cerebro del sistema, responsable de entender las solicitudes del usuario, determinar qué herramientas utilizar y cómo interpretar los resultados.

3. **Herramientas (Tools)**: Módulos especializados que proporcionan funcionalidades específicas, como búsqueda web, operaciones de archivos, consultas a bases de datos, etc.

4. **Protocolos de comunicación**: Formatos estandarizados (generalmente basados en JSON) que definen cómo se estructuran las solicitudes y respuestas entre el modelo y las herramientas.

5. **Sistema de autorización y permisos**: Controla qué herramientas puede utilizar el modelo y qué acciones puede realizar con cada una de ellas.

### Flujo de operación

Un flujo típico de operación con MCP sigue estos pasos:

1. **Recepción de la solicitud del usuario**: El usuario envía una consulta o solicitud al modelo.

2. **Análisis y planificación**: El modelo analiza la solicitud y determina qué herramientas necesita utilizar para responderla adecuadamente.

3. **Invocación de herramientas**: El modelo genera una solicitud estructurada para la herramienta seleccionada a través del runtime MCP.

4. **Ejecución de la acción**: La herramienta recibe la solicitud, ejecuta la acción correspondiente y devuelve los resultados.

5. **Procesamiento de resultados**: El modelo recibe e interpreta los resultados proporcionados por la herramienta.

6. **Respuesta al usuario**: El modelo formula una respuesta coherente basada en la información obtenida y la envía al usuario.

7. **Iteración (si es necesario)**: Dependiendo de la complejidad de la tarea, este proceso puede repetirse varias veces, con el modelo utilizando diferentes herramientas o realizando consultas adicionales.

![Diagrama de arquitectura MCP]()

### Representación de herramientas

Las herramientas en MCP se definen típicamente siguiendo una estructura similar a JSON Schema, especificando:

- Nombre y descripción de la herramienta
- Parámetros requeridos y opcionales
- Tipos de datos esperados
- Restricciones y validaciones
- Formato de respuesta

Esta representación estandarizada permite que el modelo comprenda las capacidades y requisitos de cada herramienta, facilitando su uso correcto.

```json
{
  "name": "example_tool",
  "description": "This tool performs a specific function",
  "parameters": {
    "type": "object",
    "properties": {
      "param1": {
        "type": "string",
        "description": "Description of parameter 1"
      },
      "param2": {
        "type": "number",
        "description": "Description of parameter 2"
      }
    },
    "required": ["param1"]
  }
}
```

## Usando MCP con Claude Desktop

### Requisitos previos

Para utilizar las capacidades de MCP con Claude Desktop, necesitarás:

1. **Claude Desktop**: La versión más reciente de la aplicación Claude Desktop instalada en tu sistema.
2. **Cuenta de Anthropic**: Una cuenta activa que te permita acceder a Claude (en algunos casos, puede requerirse una suscripción).
3. **Permisos de sistema**: Dependiendo de las herramientas que desees utilizar, es posible que necesites otorgar permisos específicos a la aplicación (como acceso al sistema de archivos).
4. **Conexión a Internet**: Necesaria para herramientas como Brave Search y para la comunicación con los servidores de Anthropic.
5. **Software adicional**: Para herramientas específicas como PostgreSQL, necesitarás tener instalado y configurado el software correspondiente.

![Pantalla de inicio de Claude Desktop]()

### Instalación

1. **Descarga Claude Desktop**:
   - Visita el sitio oficial de Anthropic
   - Selecciona la versión correspondiente a tu sistema operativo (Windows, macOS, Linux)
   - Descarga e instala siguiendo las instrucciones específicas para tu plataforma

2. **Verificación de la instalación**:
   - Inicia Claude Desktop
   - Verifica que puedas iniciar sesión con tu cuenta de Anthropic
   - Confirma que la aplicación funciona correctamente realizando una consulta simple

![Pantalla de configuración de herramientas]()

### Configuración

#### Configuración general de MCP

- Abre Claude Desktop
- Navega al menú de configuración
- Selecciona la sección "Desarrollador"
- Selecciona la opción "Editar configuración". Esto mostrara el archivo de configuración llamado "claude_desktop_config.json"

#### Configuración específica por herramienta

##### Filesystem MCP

Dentro de **mcpServers** añadimos lo siguiente:

```
"filesystem": {
   "command": "npx",
   "args": [
      "-y",
     "@modelcontextprotocol/server-filesystem",
      "/Users/username/Desktop",
     "/path/to/other/allowed/dir"
   ]
}
```

> [!NOTE]
> Aqui puedes listar la ruta de los directorios a los que deseas dar acceso al MCP

##### PostgreSQL MCP

Dentro de **mcpServers** añadimos lo siguiente:

```
"postgres": {
   "command": "npx",
   "args": [
     "-y",
      "@modelcontextprotocol/server-postgres",
     "postgresql://localhost/mydb"
   ]
}
```

> [!NOTE]
> Aqui debes especificar la URL de conexxión a la base de datos

### Ejemplos de uso

#### MCP de Filesystem

El MCP de Filesystem permite a Claude interactuar directamente con el sistema de archivos de tu computadora, pudiendo leer, escribir y manipular archivos y directorios.

##### Ejemplo 1: Listar directorios y archivos

**Prompt:**

```
Muéstrame el contenido del directorio Escritorio y organiza la información en una tabla que incluya nombre del archivo, tipo y tamaño.
```

**Respuesta de Claude:**
Claude utilizará el MCP de Filesystem para acceder al directorio especificado, listar su contenido y presentar la información en el formato solicitado.

![Ejemplo de listado de directorio]()

##### Ejemplo 2: Crear y modificar archivos

**Prompt:**

```
Escribe un poema sobre el mar y guardalo en un archivo llamado "poema.md" en mi Escritorio.
```

**Respuesta de Claude:**
Claude creará el archivo solicitado con el poema generado.

![Ejemplo de creación de archivo]()

#### MCP de PostgreSQL

El MCP de PostgreSQL permite a Claude consultar y analizar datos directamente desde bases de datos PostgreSQL, lo que es útil para análisis de datos, generación de reportes y automatización de tareas relacionadas con bases de datos.

Para nuestros ejemplos usaremos una base de datos de una empresa de venta de autos.

![Base de datos](image.png)

URL de conexión:
```
postgresql://postgres.wxlfdwwjbmcbehypphud:postgres@aws-0-us-east-2.pooler.supabase.com:6543/postgres
```

##### Ejemplo 1: Consulta básica de listado

**Prompt:**

```
Conéctate a mi base de datos y muéstrame una lista de todos los clientes, incluyendo solo sus nombres y estados.
```

**Respuesta de Claude:**
Claude formulará una consulta SQL sencilla para extraer los datos de la tabla "clientes" y mostrará una lista ordenada con los nombres y estados de todos los clientes registrados.

##### Ejemplo 2: Consulta con relaciones simples

**Prompt:**

```
Necesito saber qué autos ha comprado cada cliente. Genera un reporte que muestre el nombre del cliente junto con la marca y modelo de los vehículos que ha adquirido.
```

**Respuesta de Claude:**
Claude creará una consulta que relacione las tablas "clientes", "ventas" y "autos" para mostrar qué vehículos ha comprado cada cliente. El reporte incluirá el nombre del cliente y los detalles (marca y modelo) de cada auto adquirido.

##### Ejemplo 3: Generación de informe basados en datos

**Prompt:**

```
Quiero analizar el rendimiento de ventas por ciudad. Genera un informe completo que muestre el total de ventas por ciudad, el vendedor con mejor desempeño en cada ubicación, los modelos más vendidos y el precio promedio de venta, organizando los resultados por volumen total de ventas en orden descendente.
```

**Respuesta de Claude:**
Claude desarrollará un análisis complejo que vinculará las tablas "ventas", "vendedores", "sucursales", "clientes" y "autos". El informe presentará estadísticas detalladas por ciudad, identificando a los vendedores con mejor desempeño, los modelos preferidos y los precios promedio, todo organizado según el volumen total de ventas en cada ubicación.

## Referencias

