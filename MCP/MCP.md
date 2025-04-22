# Model Context Protocol (MCP)

## Índice

- [Introducción a MCP](#introducción-a-mcp)
- [Origen, desarrollo y relevancia actual del MCP](#origen-desarrollo-y-relevancia-actual-del-mcp)
- [Arquitectura de MCP](#arquitectura-de-mcp)
  - [Componentes clave y capas de transporte](#componentes-clave-y-capas-de-transporte)
- [Ventajas de MCP](#ventajas-de-mcp)
- [Desventajas de MCP](#desventajas-de-mcp)
- [Problemas de seguridad críticos de MCP](#problemas-de-seguridad-críticos-de-mcp)
  - [1. Memoria compartida: potente pero riesgosa](#1-memoria-compartida-potente-pero-riesgosa)
  - [2. Invocación de herramientas: automatización o puertas para exploits](#2-invocación-de-herramientas-automatización-o-puertas-para-exploits)
  - [3. Versionado: cuando los pequeños cambios lo rompen todo](#3-versionado-cuando-los-pequeños-cambios-lo-rompen-todo)
- [Marco de seguridad para agentes: hoja de ruta](#marco-de-seguridad-para-agentes-hoja-de-ruta)
- [Usando MCP con Claude Desktop](#usando-mcp-con-claude-desktop)
  - [Requisitos previos](#requisitos-previos)
  - [Instalación](#instalación)
  - [Configuración](#configuración)
    - [Configuración general de MCP](#configuración-general-de-mcp)
    - [Configuración específica por herramienta](#configuración-específica-por-herramienta)
      - [Filesystem MCP](#filesystem-mcp)
      - [PostgreSQL MCP](#postgresql-mcp)
  - [Ejemplos de uso](#ejemplos-de-uso)
    - [MCP de Filesystem](#mcp-de-filesystem)
      - [Ejemplo 1: Listar directorios y archivos](#ejemplo-1-listar-directorios-y-archivos)
      - [Ejemplo 2: Crear y modificar archivos](#ejemplo-2-crear-y-modificar-archivos)
    - [MCP de PostgreSQL](#mcp-de-postgresql)
      - [Ejemplo 1: Consulta básica de listado](#ejemplo-1-consulta-básica-de-listado)
      - [Ejemplo 2: Consulta con relaciones simples](#ejemplo-2-consulta-con-relaciones-simples)
      - [Ejemplo 3: Generación de informe basados en datos](#ejemplo-3-generación-de-informe-basados-en-datos)
- [Referencias](#referencias)

## Introducción a MCP

El Model Context Protocol (MCP) es un estándar emergente en el ecosistema de inteligencia artificial que permite a los modelos de lenguaje de gran tamaño (LLMs) interactuar directamente con sistemas externos y herramientas. Actúa como una capa de comunicación que conecta agentes de IA y servicios a través de una interfaz común, compartiendo memoria y reutilizando funcionalidades sin necesidad de código de integración personalizado ni sistemas de recuperación-augmented generation (RAG).

## Origen, desarrollo y relevancia actual del MCP

El Model Context Protocol (MCP) surgió como respuesta a una limitación fundamental de los modelos de lenguaje: su incapacidad para interactuar directamente con sistemas externos. Aunque los LLMs son excelentes procesando y generando texto, tradicionalmente han estado "aislados", restringidos al conocimiento pre-entrenado y la información contenida en el prompt.

El desarrollo de MCP comenzó cuando empresas como Anthropic (creadores de Claude) y otras organizaciones del ámbito de la inteligencia artificial identificaron la necesidad de un protocolo estandarizado que permitiera a los modelos:

- Solicitar información externa cuando su conocimiento interno fuera insuficiente.

- Ejecutar acciones específicas en sistemas externos según el contexto.

- Mantener un flujo bidireccional de información con herramientas externas.

Los primeros indicios de este avance se manifestaron en características como el function calling de OpenAI o las herramientas integradas en otros modelos. Sin embargo, MCP representa un esfuerzo por unificar y estandarizar estos enfoques en un protocolo coherente, aplicable en diversas plataformas y arquitecturas de modelos.

Actualmente, MCP ha ganado un gran interés, especialmente en su versión para entornos multiagente —los llamados Multi-Agent Context Protocols, promovidos por Anthropic—, que han sido descritos como el _“USB-C de los agentes de IA”_. Esta analogía destaca su promesa de convertirse en una interfaz universal que permita conectar nuevas funcionalidades de forma inmediata dentro de un ecosistema de agentes inteligentes.

## Arquitectura de MCP

### Componentes clave y capas de transporte

   ![Componentes clave de MCP](./arquitectura_mcp.gif)

En esta arquitectura, el **host MCP** (Claude Desktop, IDE o AI Tools) envía peticiones al **cliente MCP**, que a su vez se comunica con el **servidor MCP**. El servidor expone módulos especializados (herramientas, recursos, plantillas de prompt, notificaciones, muestreo) que interactúan con servicios locales y remotos.

## Ventajas de MCP

- Acceso en tiempo real a datos y eventos recientes, reduciendo alucinaciones.
- Conversión de LLMs en agentes capaces de realizar acciones concretas.
- Arquitectura modular y extensible que acelera el desarrollo de nuevas capacidades.
- Automatización de flujos de trabajo complejos sin intervención humana.
- Mejora de la experiencia de usuario con interacciones más naturales.

## Desventajas de MCP

- Mayor superficie de ataque y necesidad de controles de seguridad.
- Complejidad técnica en la implementación y mantenimiento.
- Dependencia de APIs externas con posibles latencias o indisponibilidades.
- Riesgos de privacidad y variabilidad entre implementaciones.
- Costos asociados al uso de servicios de terceros.

## Problemas de seguridad críticos de MCP

### 1. Memoria compartida: potente pero riesgosa

La memoria persistente permite coordinar agentes, pero un solo agente comprometido puede inyectar datos maliciosos en el espacio común. Otros agentes, al confiar sin validación, ejecutan instrucciones tóxicas y provocan fallos en cadena.

### 2. Invocación de herramientas: automatización o puertas para exploits

Sin sanitizar esquemas y documentación, los atacantes pueden ocultar instrucciones maliciosas en definiciones de herramientas. El resultado es un exploit sistémico similar a un prompt injection a gran escala.

### 3. Versionado: cuando los pequeños cambios lo rompen todo

La falta de control de versiones genera incompatibilidades silenciosas. Un esquema modificado o una herramienta desactualizada puede ser utilizada para inyectar código o conceder accesos no autorizados.

## Marco de seguridad para agentes: hoja de ruta

Para garantizar un ecosistema fiable es imprescindible:

- Definir controles de acceso granulares y auditorías firmadas.
- Sanitizar descripciones y parámetros de herramientas.
- Versionar formalmente interfaces y rechazar esquemas desconocidos.
- Ejecutar herramientas en sandboxes con monitorización y rollback.
- Implementar modelos de propagación de confianza que rastreen el origen de cada fragmento de información.

## Usando MCP con Claude Desktop

### Requisitos previos

Para utilizar las capacidades de MCP con Claude Desktop, necesitarás:

1. **Claude Desktop**: La versión más reciente de la aplicación Claude Desktop instalada en tu sistema.
2. **Cuenta de Anthropic**: Una cuenta activa que te permita acceder a Claude (en algunos casos, puede requerirse una suscripción).
3. **Permisos de sistema**: Dependiendo de las herramientas que desees utilizar, es posible que necesites otorgar permisos específicos a la aplicación (como acceso al sistema de archivos).
4. **Conexión a Internet**: Necesaria para herramientas como Brave Search y para la comunicación con los servidores de Anthropic.
5. **Software adicional**: Para herramientas específicas como PostgreSQL, necesitarás tener instalado y configurado el software correspondiente.

### Instalación

1. **Descarga Claude Desktop**:
   - Visita el sitio oficial de Anthropic
   - Selecciona la versión correspondiente a tu sistema operativo (Windows, macOS, Linux)
   - Descarga e instala siguiendo las instrucciones específicas para tu plataforma

2. **Verificación de la instalación**:
   - Inicia Claude Desktop
   - Verifica que puedas iniciar sesión con tu cuenta de Anthropic
   - Confirma que la aplicación funciona correctamente realizando una consulta simple

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

##### Ejemplo 2: Crear y modificar archivos

**Prompt:**

```
Escribe un poema sobre el mar y guardalo en un archivo llamado "poema.md" en mi Escritorio.
```

**Respuesta de Claude:**
Claude creará el archivo solicitado con el poema generado.

#### MCP de PostgreSQL

El MCP de PostgreSQL permite a Claude consultar y analizar datos directamente desde bases de datos PostgreSQL, lo que es útil para análisis de datos, generación de reportes y automatización de tareas relacionadas con bases de datos.

Para nuestros ejemplos usaremos una base de datos de una empresa de venta de autos.

![Base de datos](./image.png)

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

- [Anthropic: Model Context Protocol (anuncio oficial)](https://www.anthropic.com/news/model-context-protocol)
- [Medium: MCP is a Security Nightmare. Here’s How the Agent Security Framework Fixes It](https://medium.com/data-science-collective/mcp-is-a-security-nightmare-heres-how-the-agent-security-framework-fixes-it-fd419fdfaf4e)
- [Repositorio oficial de MCP en GitHub](https://github.com/modelcontextprotocol)
- [Documentación de MCP en Anthropic](https://docs.anthropic.com/en/docs/agents-and-tools/mcp)
