<div align="center">

<h1>AURIGA</h1>

<h2>PROMPT MAESTRO</h2>

<p><strong>Especificación completa para construir una herramienta personal equivalente a AURIGA-PERSONAL 2.1.0</strong></p>

<p>
  <img alt="Versión 1.0" src="https://img.shields.io/badge/version-1.0-08796F?style=flat-square">
  <img alt="Uso personal" src="https://img.shields.io/badge/uso-personal-071521?style=flat-square">
  <img alt="Idiomas ES y EN" src="https://img.shields.io/badge/idiomas-ES%20%7C%20EN-647582?style=flat-square">
  <img alt="Arquitectura local-first" src="https://img.shields.io/badge/arquitectura-local--first-C78316?style=flat-square">
</p>

</div>

---

| Documento | Detalle |
| --- | --- |
| **Versión** | 1.0 |
| **Destino** | Uso personal, local-first y distribuible como paquete portátil sin firma |
| **Idiomas** | Castellano e inglés |
| **Fecha** | 17/07/2026 |

> [!IMPORTANT]
> Este documento debe entregarse completo a un agente de programación con acceso al sistema de archivos y capacidad de ejecutar pruebas. El agente no debe limitarse a generar una maqueta: debe implementar, verificar, empaquetar y devolver una aplicación funcional.

> [!WARNING]
> Clasificación: uso personal. La ausencia de firma de código no elimina los requisitos internos de cifrado, integridad, auditoría, copias y control de acceso.

---

## Índice

1. [Cómo utilizar este documento](#1-como-utilizar-este-documento)
2. [Prompt maestro copiable](#2-prompt-maestro-copiable)
3. [Arquitectura de referencia](#3-arquitectura-de-referencia)
4. [Contratos de datos esenciales](#4-contratos-de-datos-esenciales)
5. [API local recomendada](#5-api-local-recomendada)
6. [Configuración y secretos](#6-configuracion-y-secretos)
7. [Plan de construcción paso a paso](#7-plan-de-construccion-paso-a-paso)
8. [Pruebas obligatorias](#8-pruebas-obligatorias)
9. [Matriz de aceptación final](#9-matriz-de-aceptacion-final)
10. [Empaquetado personal sin firma](#10-empaquetado-personal-sin-firma)
11. [Riesgos residuales](#11-riesgos-residuales-que-deben-declararse)
12. [Informe final](#12-informe-final-que-debe-devolver-el-agente)
13. [Próximas mejoras recomendadas](#13-proximas-mejoras-recomendadas)

---

## 1. Como utilizar este documento

Copie desde la seccion 2 hasta el marcador FIN DEL PROMPT MAESTRO y entreguelo a un agente de desarrollo. Adjunte, si existe, la version anterior de AURIGA o su repositorio para que pueda conservar arquitectura, flujos y formatos compatibles. El agente debe trabajar por fases, mantener un registro de decisiones y no declarar terminado el proyecto hasta superar todos los criterios de aceptacion.

- Conceda acceso de escritura unicamente a una carpeta de trabajo y a la carpeta final de entrega.
- No incluya claves API reales en el prompt ni en el repositorio. Configúrelas despues mediante la boveda cifrada.
- Exija una copia de seguridad antes de migrar datos de versiones anteriores.
- Solicite evidencia de pruebas: compilacion, resultados automatizados, arranque desde ZIP limpio, hashes y diagnostico.
- Para uso propio, emplee el iniciador portatil. Reserve la firma de codigo para distribucion profesional o a terceros.

> [!IMPORTANT]
> Resultado esperado: una aplicacion local-first funcional, no una demostracion visual ni un conjunto de archivos sin probar.

## 2. PROMPT MAESTRO COPIABLE

> [!IMPORTANT]
> INICIO DEL PROMPT MAESTRO

### ROL Y FORMA DE TRABAJO

> Actua como un equipo senior compuesto por arquitecto de software, ingeniero de seguridad, especialista multimedia, ingeniero de IA, diseñador UX bilingue, QA y responsable de release para Windows.
>
> Construye una herramienta nueva llamada AURIGA-PERSONAL, para uso propio, equivalente o superior a AURIGA-PERSONAL 2.1.0. Debe ser una aplicacion real, robusta, portable, local-first y apta para operar; no una maqueta.
>
> Trabaja con autonomia dentro de la carpeta autorizada. Inspecciona primero cualquier codigo o version anterior. Conserva lo que funciona, especialmente arquitectura, flujo de datos, formatos de expediente y controles de seguridad. Documenta cualquier incompatibilidad.
>
> Divide el trabajo en fases verificables. Tras cada cambio importante ejecuta comprobaciones proporcionales al riesgo. No declares completado el proyecto mientras exista un fallo de compilacion, arranque, dependencia, seguridad critica o perdida de datos.
>

### OBJETIVO DEL PRODUCTO

> AURIGA-PERSONAL debe organizar expedientes, incorporar grandes volumenes de evidencias y datos, conservar sus originales cifrados, extraer informacion determinista, solicitar valoraciones estructuradas a modelos de IA, permitir revision humana y emitir expedientes profesionales en PDF y otros formatos.
>
> Debe procesar imagen, audio, video, PDF, texto, CSV, TSV, JSON, JSONL, XML, HTML, Markdown, RTF, registros, codigo fuente, documentos ofimaticos y archivos binarios. Cuando no exista extractor nativo, debe conservar, catalogar, hashear y sellar el archivo, informando de la limitacion sin fingir que lo ha interpretado.
>
> Debe admitir captura autorizada en tiempo real desde camaras y microfonos del equipo. Los dispositivos estaran apagados por defecto, requeriran permiso explicito y mostraran un indicador persistente mientras estén activos.
>

### REQUISITOS NO NEGOCIABLES

> Interfaz completa en castellano e ingles, con selector visible y persistencia de idioma. Informes y expedientes tambien bilingues.
>
> Carga multiple. Limite predeterminado de 4 GB por archivo, configurable. No cargar archivos completos en memoria.
>
> Calculo SHA-256 por streaming sobre el original antes de incorporarlo al expediente.
>
> Cifrado autenticado AES-256-GCM por bloques. Cada bloque debe estar ligado criptograficamente a la cabecera, el indice, el tamaño y el orden para detectar sustitucion, reordenacion, truncado o alteracion.
>
> Compatibilidad de lectura con evidencias de la version anterior. Las migraciones deben ser atomicas, recuperables y precedidas por copia.
>
> Entrega HTTP de audio y video mediante Range requests sin descifrar el archivo completo en memoria.
>
> Archivos temporales de subida y procesamiento en carpetas separadas. Limpieza segura de mejor esfuerzo tanto en exito como en error.
>
> Base, auditoria, metricas, boveda de secretos, clave de firma y evidencias cifradas en reposo.
>
> Clave maestra protegida mediante DPAPI CurrentUser en Windows. En otros sistemas, frase maestra obligatoria derivada con scrypt o Argon2id.
>
> Nunca registrar ni devolver claves API, tokens, contraseñas o contenido sensible en logs de error.
>
> Aplicacion enlazada solo a 127.0.0.1 por defecto. Cabeceras de seguridad, CSP, limitacion de peticiones, validacion estricta y roles administrador, analista y consulta.
>
> No ejecutar, abrir como codigo ni servir con MIME ejecutable los archivos incorporados. Tratar todos los contenidos como no confiables.
>

### CAPTURA Y PROCESAMIENTO EN TIEMPO REAL

> Ofrecer modos camara, microfono y camara+microfono mediante MediaDevices y MediaRecorder o una tecnologia equivalente.
>
> Segmentos configurables de 10, 30, 60 y 300 segundos. Cada segmento debe ser un archivo reproducible independiente, no un fragmento sin cabecera.
>
> Al cerrar cada segmento: calcular hash, cifrar, registrar cadena de custodia, extraer metadatos y actualizar el expediente.
>
> Valoracion IA automatica opcional, desactivada por defecto. Antes de activarla, advertir que puede enviar datos a terceros y generar costes.
>
> Permitir detener inmediatamente la captura, cerrar todas las pistas y mostrar el estado real del dispositivo. Detener pistas tambien al abandonar el componente o cerrar el expediente.
>
> Para flujo sostenido, usar una cola con concurrencia acotada y backpressure. Si el analisis se retrasa, seguir sellando segmentos y mostrar pendientes sin perder datos.
>

### PROVEEDORES DE IA

> Implementar adaptadores separados para Google Gemini, OpenAI/ChatGPT, Anthropic Claude (incluidos Fable, Opus, Sonnet y Haiku cuando la cuenta los ofrezca), xAI Grok, Alibaba Qwen, DeepSeek, Ollama local y una pasarela compatible con OpenAI.
>
> Las claves se configuran mediante una boveda cifrada y nunca viajan al navegador. Ollama debe funcionar sin clave en 127.0.0.1 y descubrir los modelos instalados.
>
> No fijar la logica a nombres de modelos que caducan. Mantener catalogos sugeridos actualizables, campo de modelo editable y descubrimiento cuando el proveedor lo permita.
>
> Declarar capacidades por proveedor: texto, imagen, audio, video y PDF. Rechazar de forma clara una combinacion no admitida.
>
> No enviar archivos de varios GB en base64. Definir un limite MAX_INLINE_AI_MB; por encima, extraer contexto, segmentar, muestrear o pedir una seleccion reproducible.
>
> Validar todas las respuestas contra un esquema estricto antes de persistirlas. Registrar proveedor, modelo, fecha, duracion, tokens, coste estimado, version de esquema y limitaciones.
>
> Implementar reintentos con espera exponencial solo para errores transitorios. No reintentar automaticamente errores de autorizacion, validacion o tamaño.
>
> Ofrecer consenso entre dos y seis modelos y mostrar acuerdo, desacuerdo, ejecuciones fallidas y coste. No convertir consenso de modelos en hecho probado.
>

### ANALISIS Y UTILIDADES

> Protocolos: general multimodal, seguridad, integridad, comparacion, audio, agricultura y señales observables de salud sin diagnostico.
>
> Extraccion determinista: EXIF, ffprobe, music-metadata, tamaño, MIME real, duracion, streams, codecs, resolucion, frecuencia, texto y estructura basica.
>
> OCR local con Tesseract para imagenes. Extraccion textual acotada para texto, CSV, JSON, XML, HTML, RTF y registros, indicando si la muestra fue truncada.
>
> Segmentacion fisica no destructiva de audio y video con FFmpeg. La salida se incorpora como nueva evidencia derivada con referencia al original y rango temporal.
>
> Procesamiento por lotes en segundo plano con identificador de trabajo, estado, total, completados, fallidos, resultado por elemento y concurrencia configurable de 1 a 4.
>
> Paginacion y busqueda para expedientes con miles de evidencias. Evitar respuestas JSON gigantes y operaciones Promise.all sobre todos los originales.
>

### EXPEDIENTES Y SALIDAS

> Generar PDF profesional con portada, identificacion del expediente, aviso metodologico, inventario de evidencias, hashes, resultados, revisiones humanas, limitaciones y auditoria encadenada.
>
> Exportar tambien HTML autocontenido e imprimible, Markdown, TXT, JSON estructurado, CSV y ZIP firmado con manifiesto y originales descifrados por streaming.
>
> Firmar manifiestos y revisiones humanas con Ed25519. Proteger la clave privada cifrada. Incluir huella de clave publica y datos suficientes para verificar fuera de AURIGA.
>
> Proporcionar copia sellada local de solo lectura como mejor esfuerzo y explicar que no equivale a WORM ni a sello de tiempo RFC 3161.
>
> Webhooks opcionales para SIEM, VMS y eDiscovery, firmados, con lista permitida de destinos y sin seguir redirecciones a redes no autorizadas.
>

### EXPERIENCIA DE USUARIO

> Interfaz intuitiva, sobria, accesible y adaptable a escritorio y movil. Estados de carga y error comprensibles, sin jerga innecesaria.
>
> Panel de expedientes, inventario de evidencias, visor multimedia, configuracion de analisis, utilidades deterministas, historial, chat restringido al analisis y revision humana firmada.
>
> Mostrar siempre que las conclusiones de IA son observaciones de cribado. No realizar identificacion facial, diagnostico medico, inferencias de atributos sensibles ni atribucion de culpabilidad.
>
> No bloquear el navegador al cargar archivos grandes. Mostrar progreso, cola, tamaño, hash corto, tipo detectado, fecha y estado de procesamiento.
>
> La vista previa de camara apagada debe decirlo expresamente; no mostrar una pantalla negra que pueda confundirse con un fallo.
>

### CALIDAD, SEGURIDAD Y ENTREGA

> Aplicar TypeScript estricto, validacion Zod o equivalente, manejo centralizado de errores y separacion clara entre cliente, API, dominio, almacenamiento, seguridad, proveedores y exportacion.
>
> Crear pruebas unitarias, integracion, seguridad, streaming, rangos, cifrado, manipulacion de cabecera, auditoria, roles, migracion y esquema de respuesta.
>
> Ejecutar pruebas con archivos sinteticos grandes y comprobar que el consumo de memoria se mantiene acotado.
>
> Generar SBOM CycloneDX, auditoria de dependencias de produccion, documentacion de amenazas, operaciones, compatibilidad, copias, restauracion e incidentes.
>
> Construir paquete Windows x64 autocontenido con runtime Node portable y dependencias fisicas, sin junctions, symlinks ni reparse points.
>
> La edicion personal debe iniciarse con INICIAR_AURIGA_PERSONAL.cmd sin instalacion, firma, certificado ni administrador. Mantener la consola abierta y abrir http://127.0.0.1:4174.
>
> Crear manifiesto JSON y archivo SHA-256 junto al ZIP. Extraer el ZIP en una carpeta limpia y arrancarlo antes de entregar.
>
> Conservar data y .env durante actualizaciones. Nunca sustituirlos ni borrarlos al desplegar una nueva version.
>

### ENTREGABLES OBLIGATORIOS

> Codigo fuente completo, compilacion de produccion, runtime portable, dependencias de produccion, pruebas y documentacion.
>
> Carpeta funcional AURIGA y ZIP AURIGA-PERSONAL-<version>.zip para uso propio.
>
> INICIAR_AURIGA_PERSONAL.cmd, CONFIGURAR_CLAVES.cmd, DIAGNOSTICO.cmd, CREAR_COPIA.cmd y RESTAURAR_COPIA.cmd.
>
> README, CHANGELOG, SECURITY, modelo de amenazas, arquitectura, operaciones, evaluacion de IA y guia de firma opcional.
>
> Informe final con version, ubicaciones, SHA-256, pruebas superadas, riesgos residuales y pasos exactos para iniciar.
>

### CONDICION DE TERMINACION

> Solo confirma finalizacion cuando: compila sin errores; pasan todas las pruebas; arranca la carpeta instalada; arranca una extraccion limpia del ZIP; el endpoint de salud informa la version correcta; la auditoria es valida; el limite grande es efectivo; la captura permanece apagada por defecto; los idiomas ES/EN funcionan; y los hashes publicados coinciden.
>
> Si una dependencia falta, un binario nativo no existe, un ZIP pierde enlaces transitivos o la aplicacion no escucha el puerto, corrige el problema, vuelve a empaquetar y repite toda la validacion final.
>

> [!IMPORTANT]
> FIN DEL PROMPT MAESTRO

## 3. Arquitectura de referencia

La arquitectura recomendada conserva el navegador como cliente no privilegiado y concentra secretos, cifrado, proveedores y archivos en el servidor local. Ninguna clave API debe incorporarse al bundle del cliente.

```text
Navegador React/TypeScript
  |-- UI ES/EN
  |-- carga multiple y captura MediaDevices/MediaRecorder
  |-- visor con Range requests
  |-- panel de trabajos y resultados
  v
API Express en 127.0.0.1
  |-- autenticacion y roles
  |-- validacion Zod y rate limiting
  |-- servicios de casos, evidencias, analisis y exportacion
  |-- cola de trabajos con concurrencia acotada
  +--> Almacenamiento local cifrado
  |      |-- database.enc / audit.enc / metrics.enc
  |      |-- cases/<caseId>/<evidenceId>.auriga
  |      +-- vault y claves protegidas con DPAPI
  +--> Herramientas locales
  |      |-- FFmpeg / ffprobe
  |      |-- EXIF / music-metadata
  |      +-- Tesseract OCR
  +--> Adaptadores de IA
         |-- Gemini / OpenAI / Anthropic / xAI
         |-- Qwen / DeepSeek
         |-- Ollama
         +-- OpenAI compatible
```

### 3.1 Flujo de incorporacion de archivos

- Multer o equivalente escribe en upload-temp con nombre aleatorio y limite configurable.
- Detectar tipo por contenido cuando sea posible; usar extension solo como ayuda, nunca como prueba suficiente.
- Calcular SHA-256 leyendo el archivo secuencialmente.
- Cifrar por bloques hacia un archivo temporal dentro del directorio de destino.
- Sincronizar, renombrar atomica y unicamente entonces registrar la evidencia y la auditoria.
- Eliminar el temporal de subida en un bloque finally. Si falla el registro, retirar el cifrado huerfano.

### 3.2 Formato cifrado por bloques

Una implementacion sencilla y verificable puede utilizar la siguiente estructura. La cabecera y los campos de orden deben autenticarse como AAD en todos los bloques.

```text
Cabecera:
  magic[8]             = AURIGA3\0
  chunk_size_uint32    = 4 MiB por defecto
  plaintext_size_u64   = tamaño total original

Por cada bloque:
  plaintext_len_u32
  iv[12]               = aleatorio y unico
  tag[16]
  ciphertext[n]

AAD por bloque:
  cabecera completa + indice_u64 + plaintext_len_u32
```

> [!WARNING]
> No reutilizar IV. Rechazar tamaños absurdos, archivos truncados, etiquetas invalidas y texto descifrado que exceda el limite previsto. Ante un error, eliminar cualquier salida parcial.

### 3.3 Estructura de carpetas propuesta

```text
AURIGA/
  dist-client/                 cliente compilado
  dist-server/                 API compilada
  runtime/node.exe             runtime portable
  node_modules/                dependencias fisicas de produccion
  data/                        nunca se incluye en actualizaciones
    cases/<caseId>/
    upload-temp/
    temp/
    database.enc
    audit.enc
    master-key.dpapi
    secrets.vault
  src/                         interfaz
  server/                      API y servicios
  shared/                      esquemas compartidos
  tests/                       pruebas
  docs/                        arquitectura, amenazas y operaciones
  INICIAR_AURIGA_PERSONAL.cmd
  CONFIGURAR_CLAVES.cmd
  DIAGNOSTICO.cmd
  CREAR_COPIA.cmd
  RESTAURAR_COPIA.cmd
```

## 4. Contratos de datos esenciales

### 4.1 Evidencia

```text
EvidenceRecord {
  id: UUID
  caseId: UUID
  originalName: string <= 255
  storedName: string
  mimeType: string
  size: positive integer
  sha256: 64 hex
  label: string
  capturedAt: ISO datetime | null
  ingestedAt: ISO datetime
  derivedFromEvidenceId?: UUID | null
  enrichment?: {
    extractedAt: ISO datetime
    technical: object
    extractedText: string <= configured cap
    language: string
    truncated?: boolean
  }
}
```

### 4.2 Resultado de analisis

- Resumen y observaciones con confianza, marca temporal nullable y base visual, audio, metadatos o multimodal.
- Objetos o entidades con etiqueta, estado, atributos, confianza y caja normalizada 0..1000 cuando proceda.
- Eventos con categoria, severidad, confianza, tiempo y observacion.
- Audio con idioma, extracto de transcripcion, sonidos y notas.
- Cribado de integridad: consistent, suspicious o inconclusive, siempre con aviso metodologico.
- Comparacion reproducible con evidencia de referencia, similitud nullable, diferencias y conclusion limitada.
- Valoracion contextual de riesgo y coherencia audiovisual.
- Lista no vacia de limitaciones.

### 4.3 Auditoria encadenada

```text
AuditEntry {
  sequence: integer creciente
  id: UUID
  timestamp: ISO datetime
  action: string
  caseId: UUID | null
  evidenceId: UUID | null
  details: object sin secretos
  previousHash: SHA-256 o GENESIS
  hash: SHA-256(JSON canonico de todos los campos anteriores)
}
```

La verificacion debe recorrer la cadena completa y devolver valid, numero de entradas y primera secuencia invalida. Para gran escala, evolucionar a registros append-only segmentados sin romper la compatibilidad del verificador.

## 5. API local recomendada

| Metodo | Ruta | Funcion |
| --- | --- | --- |
| GET | /api/health | Version, capacidades, proveedores, limites y auditoria |
| GET/POST | /api/cases | Listar y crear expedientes |
| GET/DELETE | /api/cases/:caseId | Recuperar o eliminar con confirmacion |
| POST | /api/cases/:caseId/evidence | Incorporar un archivo por streaming |
| GET | /api/cases/:caseId/evidence/:id/content | Contenido descifrado con Range |
| POST | /api/cases/:caseId/evidence/:id/enrich | Metadatos, texto y OCR |
| POST | /api/cases/:caseId/evidence/:id/segment | Crear recorte fisico derivado |
| POST | /api/cases/:caseId/evidence/:id/analyze | Analisis con proveedor/modelo |
| POST | /api/cases/:caseId/evidence/:id/consensus | Consenso multmodelo |
| POST | /api/cases/:caseId/batch/enrich | Trabajo por lote en segundo plano |
| GET | /api/jobs/:jobId | Estado y progreso del trabajo |
| POST | /api/cases/:caseId/analyses/:id/review | Revision humana Ed25519 |
| GET | /api/cases/:caseId/report.pdf | Expediente PDF ES/EN |
| GET | /api/cases/:caseId/document.:format | HTML, MD, TXT, JSON o CSV |
| GET | /api/cases/:caseId/export.zip | Paquete firmado con originales |
| GET | /api/cases/:caseId/audit | Auditoria y verificacion |

## 6. Configuracion y secretos

| Variable | Valor inicial | Uso |
| --- | --- | --- |
| PORT | 4174 | Puerto local |
| MAX_UPLOAD_MB | 4096 | Limite por archivo |
| MAX_INLINE_AI_MB | 25 | Tope de envio directo a IA |
| ENCRYPTION_CHUNK_MB | 4 | Bloque AES-GCM |
| *_API_KEY | vacio | Migrar inmediatamente a boveda cifrada |
| *_MODEL | editable | Modelo sugerido por proveedor |
| OLLAMA_BASE_URL | 127.0.0.1:11434 | Servidor local Ollama |
| AURIGA_ACCESS_TOKEN | generado | Administrador |
| AURIGA_ANALYST_TOKEN | opcional | Analista |
| AURIGA_VIEWER_TOKEN | opcional | Solo lectura |
| AURIGA_DATA_DIR | ./data | Almacen cifrado |

> [!WARNING]
> No mostrar las claves configuradas en la interfaz, ni siquiera enmascaradas parcialmente. Permitir sustituirlas o eliminarlas. Proteger la boveda con la misma clave maestra y autenticar el contenido.

## 7. Plan de construccion paso a paso

### Fase 0 - Descubrimiento y copia

Inventariar repositorio, dependencias, formatos de datos y flujos. Crear copia verificable. Documentar riesgos y no modificar datos reales durante el desarrollo.

### Fase 1 - Esqueleto y contratos

Crear cliente, API, shared schemas, configuracion, manejo de errores y pruebas basicas. Fijar version y estructura de release.

### Fase 2 - Custodia segura

Implementar DPAPI/frase maestra, boveda, cifrado atomico, streaming por bloques, hashes, auditoria y compatibilidad de lectura anterior.

### Fase 3 - Ingesta de volumen

Multer en disco, carga multiple, tipos amplios, limites, temporales, progreso, Range requests y pruebas de memoria.

### Fase 4 - Metadatos y medios

Integrar ffprobe, FFmpeg, EXIF, music-metadata, texto, OCR y evidencias derivadas.

### Fase 5 - Tiempo real

Implementar permisos, vista previa, MediaRecorder, segmentos independientes, cola, backpressure, sellado y apagado fiable.

### Fase 6 - Adaptadores IA

Implementar interfaz comun, capacidades, modelos editables, proveedores cloud, Ollama, validacion de resultados, reintentos, uso y costes.

### Fase 7 - Lotes y consenso

Crear trabajos persistibles, progreso, errores por elemento, concurrencia acotada y consenso multmodelo.

### Fase 8 - Interfaz bilingue

Traducir todos los estados, formularios, modales, errores, ayuda, accesibilidad y formatos de fecha. Probar escritorio y movil.

### Fase 9 - Informes y firma

PDF profesional, HTML, Markdown, TXT, JSON, CSV, ZIP streaming, manifiesto Ed25519 y revisiones humanas.

### Fase 10 - Producto distribuible

Scripts de inicio, instalacion opcional, actualizacion conservadora, copia, restauracion, diagnostico, SBOM y documentacion.

### Fase 11 - Seguridad y calidad

Pruebas, auditoria de dependencias, manipulacion, roles, limites, fallos parciales, migracion, evaluacion de IA y amenazas.

### Fase 12 - Validacion limpia

Empaquetar dependencias fisicas, verificar binarios, cero reparse points, extraer ZIP limpio, arrancar, comprobar health y publicar hashes.

## 8. Pruebas obligatorias

| Area | Prueba | Criterio |
| --- | --- | --- |
| Cifrado | Round-trip de archivo > varios bloques | Contenido y SHA-256 identicos |
| Cifrado | Alterar cabecera, orden, tag o ciphertext | Descifrado rechazado; sin temporal residual |
| Streaming | Archivo sintetico grande | Memoria acotada; sin Buffer del total |
| Range | Solicitar rango intermedio | 206, Content-Range y bytes exactos |
| Carga | Tipo desconocido | Conservado como octet-stream; nunca ejecutado |
| Carga | Superar limite | 413 claro y temporal eliminado |
| Auditoria | Modificar entrada | Cadena invalida y secuencia detectada |
| Roles | Viewer intenta POST/DELETE | 403 |
| IA | Respuesta fuera de esquema | No persistida; error controlado |
| IA | Archivo > MAX_INLINE_AI_MB | Segmentar/resumir o rechazar con guia |
| Tiempo real | Iniciar y detener | Permiso, indicador, segmentos y pistas cerradas |
| Tiempo real | Analisis mas lento que captura | Cola visible y ninguna perdida |
| Exportacion | Caso con evidencia grande | ZIP por streaming; manifiesto verificable |
| Bilingue | Recorrido completo ES/EN | Sin textos residuales del otro idioma |
| Actualizacion | Instalar sobre datos existentes | data y .env conservados |
| Portabilidad | Extraer ZIP limpio | Arranca sin instalar Node ni dependencias |
| Dependencias | Buscar reparse points e ip-address | 0 enlaces; transitivas presentes |

## 9. Matriz de aceptacion final

- [ ] 01. La version mostrada en UI, health, diagnostico, package.json y manifiestos coincide.

- [ ] 02. Todos los originales nuevos se guardan en formato cifrado por bloques autenticados.

- [ ] 03. Se pueden incorporar varios archivos y un archivo mayor de 20 MB sin agotar memoria.

- [ ] 04. El limite efectivo es 4 GB salvo configuracion explicita diferente.

- [ ] 05. Audio y video permiten reproduccion y salto temporal mediante rangos.

- [ ] 06. Camara y microfono estan apagados por defecto, requieren permiso y muestran indicador activo.

- [ ] 07. Cada segmento en directo es independiente, queda sellado y aparece en auditoria.

- [ ] 08. Los ocho adaptadores de proveedor existen y Ollama descubre modelos locales.

- [ ] 09. Los modelos son editables y las claves permanecen exclusivamente en servidor/boveda.

- [ ] 10. La interfaz principal, modales, errores, informes y exportaciones funcionan en ES y EN.

- [ ] 11. PDF, HTML, MD, TXT, JSON, CSV y ZIP se generan sin errores.

- [ ] 12. El ZIP firmado no carga todas las evidencias simultaneamente.

- [ ] 13. Las pruebas automatizadas y la compilacion final terminan con codigo 0.

- [ ] 14. La auditoria de produccion no contiene vulnerabilidades criticas conocidas sin documentar.

- [ ] 15. El paquete portable contiene runtime, binarios multimedia y dependencias fisicas sin enlaces.

- [ ] 16. Una extraccion limpia arranca y devuelve health correcto.

- [ ] 17. El iniciador personal funciona sin firma, certificado ni administrador.

- [ ] 18. La actualizacion conserva data y .env.

- [ ] 19. Se publican SHA-256 y manifiesto para cada ZIP.

- [ ] 20. Se documentan riesgos residuales y limites; no se presenta la IA como peritaje concluyente.

## 10. Empaquetado personal sin firma

Para uso propio puede entregarse el programa sin firma de codigo. El paquete debe ser autocontenido, pero no debe intentar desactivar SmartScreen, Smart App Control, antivirus, UAC ni politicas corporativas.

```bat
INICIAR_AURIGA_PERSONAL.cmd

@echo off
setlocal EnableExtensions
cd /d "%~dp0"
title AURIGA - Edicion personal
if not exist "runtime\node.exe" (
  echo [ERROR] Falta runtime\node.exe
  pause
  exit /b 1
)
if not exist "data" mkdir "data"
start "" "http://127.0.0.1:4174"
"runtime\node.exe" --enable-source-maps dist-server\server\index.js
if errorlevel 1 pause
endlocal
```

- El ZIP personal puede contener tambien scripts de instalacion, pero el flujo recomendado usa el iniciador portatil.
- Incluir USO_PERSONAL_SIN_FIRMA.txt con inicio, claves, copias, integridad y limitaciones.
- La ausencia de firma no reduce el cifrado ni la auditoria interna; solo impide acreditar publicamente al editor.
- Para distribuir a terceros, firmar ejecutables/instalador con un certificado o servicio de firma reconocido y sello RFC 3161.

## 11. Riesgos residuales que deben declararse

- DPAPI protege frente a copia del disco, no frente a malware que controle la sesion abierta del usuario.
- La sobrescritura en SSD es de mejor esfuerzo. Para destruccion estricta se requiere cifrado de volumen y destruccion de claves.
- Un archivo de solo lectura no es WORM ni custodia certificada.
- Las valoraciones de IA pueden ser incompletas o erroneas y requieren revision humana cualificada.
- La deteccion de integridad o deepfake generativa no sustituye mediciones forenses especializadas.
- Los limites y formatos de los proveedores cambian. La aplicacion debe degradar de forma controlada y mantener modelos configurables.
- Una base JSON cifrada completa puede ser suficiente para uso personal, pero para millones de registros debe migrarse a una base transaccional cifrada con indices y paginacion.
- El analisis de documentos ofimaticos depende de extractores disponibles; conservar no significa interpretar.

## 12. Informe final que debe devolver el agente

```text
1. Resultado: version final y estado operativo.
2. Ubicacion de carpeta instalada y ZIP personal.
3. SHA-256 de cada paquete.
4. Funciones implementadas y funciones deliberadamente limitadas.
5. Pruebas ejecutadas y resultados exactos.
6. Verificacion desde extraccion limpia.
7. Estado de auditoria de dependencias y SBOM.
8. Pasos de inicio para uso personal.
9. Como configurar claves cloud y Ollama.
10. Copias, restauracion y migracion.
11. Riesgos residuales y recomendaciones futuras.
```

## 13. Proximas mejoras recomendadas

- Base transaccional cifrada y paginada para cientos de miles o millones de evidencias.
- Workers persistentes con reanudacion tras reinicio y prioridades por expediente.
- Transcripcion local de audio mediante Whisper compatible y diarizacion opcional sin identificacion.
- Extraccion segura en sandbox para DOCX, XLSX, PPTX, ODF y PDF con limites anti-bomba ZIP.
- Muestreo reproducible de videos largos con indice de escenas, miniaturas y mapa temporal.
- Sellado RFC 3161 y almacenamiento WORM externo opcional.
- Conectores propietarios firmados para VMS, SIEM y eDiscovery concretos.
- Actualizaciones verificadas mediante manifiesto firmado y rollback automatico.
- Evaluaciones reproducibles por proveedor/modelo con datasets de referencia y umbrales de regresion.

---

> [!IMPORTANT]
> FIN DEL DOCUMENTO - AURIGA-PROMPT
