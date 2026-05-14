# User Stories - Sistema LTI (ATS/CRM)

A partir del análisis del Documento de Requisitos del Producto (PRD) y la Arquitectura del ecosistema LTI, se han derivado las siguientes User Stories principales. Todas aplican metodologías BDD (Behavior-Driven Development) y el marco de calidad INVEST.

---

## User Stories para el Sistema LTI

### 🏷️ US-01: Análisis Semántico y Matching de Currículums (NLP)
**Historia de Usuario:**
> Como Reclutador, quiero que el sistema analice los currículums recibidos y los compare semánticamente con la descripción de la vacante, para priorizar automáticamente a los candidatos más afines sin necesidad de revisión manual.

**Criterios de Aceptación (BDD):**
- **Escenario 1 (Éxito - Extracción y Matching):** Given que un candidato envía su CV en PDF, When el sistema recibe el archivo, Then el agente de NLP debe extraer las habilidades y calcular un "Match Score" porcentual en relación a la vacante en menos de 3 segundos.
- **Escenario 2 (Edge Case - Diferencias Semánticas):** Given una vacante que requiere "Desarrollo Frontend", When el candidato incluye el término "React Developer" en su currículum, Then el sistema debe reconocer la relación semántica e incrementar el Match Score adecuadamente.
- **Escenario 3 (Error/Límite - Archivo Dañado o Protegido):** Given el flujo de postulación, When un candidato sube un documento protegido con contraseña, Then el sistema debe abortar el parsing, mostrar el mensaje "El archivo no pudo leerse, por favor súbelo sin contraseña" y registrar el evento sin afectar al candidato.

**🛠️ Notas Técnicas y No Funcionales:**
- **Performance:** Tiempo máximo de parsing asíncrono (mediante Apache Kafka) < 3 segundos.
- **Seguridad:** Los archivos originales deben almacenarse en AWS S3 con encriptación en reposo (AES-256).
- **Accesibilidad:** Uso de directivas ARIA en los mensajes de alerta en el frontend para lectores de pantalla.

**✅ Evaluación INVEST:**
- [x] **I**ndependent: Funciona con independencia del módulo de video o el portal CRM.
- [x] **N**egociable: Los pesos específicos del Match Score son ajustables.
- [x] **V**aluable: Automatiza la tarea más intensiva en tiempo del reclutador (Criba curricular).
- [x] **E**stimable: Se puede estimar claramente el esfuerzo del agente NLP.
- [x] **S**mall: Abordar solo el parsing de PDF/DOCX es lo suficientemente pequeño para un Sprint.
- [x] **T**estable: Puede probarse subiendo 10 PDFs de control para verificar el JSON resultante y el score.

---

### 🏷️ US-02: Auditoría y Justificación Ética de IA (XAI)
**Historia de Usuario:**
> Como Director de RR.HH., quiero ver una explicación detallada de por qué la Inteligencia Artificial asignó un puntaje específico a un candidato, para asegurar un proceso ético, transparente y libre de sesgos discriminatorios.

**Criterios de Aceptación (BDD):**
- **Escenario 1 (Éxito - Visualización de Justificación):** Given que estoy en el perfil de un candidato evaluado, When hago clic en el botón "Ver justificación de IA", Then se despliega un panel que lista en lenguaje natural las variables exactas que justifican su Match Score.
- **Escenario 2 (Edge Case - Exclusión de Factores Sensibles):** Given que la IA procesa el perfil, When detecta variables protegidas por ley (ej. edad o género), Then el sistema debe ignorarlas en el puntaje y registrar en `REGISTRO_XAI` que fueron explícitamente excluidas.
- **Escenario 3 (Error/Límite - Registro XAI Faltante):** Given que un usuario consulta el panel XAI, When el registro ético aún no se ha generado por latencia, Then la UI debe indicar "Auditoría algorítmica en proceso, intente nuevamente en unos segundos" sin bloquear al usuario.

**🛠️ Notas Técnicas y No Funcionales:**
- **Integridad de Datos:** Uso de tablas relacionales (PostgreSQL) para garantizar integridad referencial estricta.
- **Seguridad (Compliance):** La base de datos XAI debe ser inmutable (Append-only) para evitar manipulaciones de auditoría.

**✅ Evaluación INVEST:**
- [x] **I**ndependent: El visor de auditoría solo necesita consultar la base de datos de auditoría, separada del core de IA.
- [x] **N**egociable: El formato de visualización y el nivel de detalle técnico mostrado.
- [x] **V**aluable: Es el diferenciador principal ("Ventaja Injusta") y previene riesgos legales graves.
- [x] **E**stimable: Desarrollo predecible (Endpoint GET y Modal Frontend).
- [x] **S**mall: Solo incluye la lectura de registros previamente generados por el servicio.
- [x] **T**estable: Verificable inyectando un log de XAI manual y validando su visualización en UI.

---

### 🏷️ US-03: Automatización del Cumplimiento RGPD (Borrado de Datos)
**Historia de Usuario:**
> Como Responsable Legal (DPO), quiero que el sistema administre automáticamente el ciclo de vida de los datos de los candidatos eliminando perfiles inactivos, para cumplir con el RGPD y evitar multas sancionatorias.

**Criterios de Aceptación (BDD):**
- **Escenario 1 (Éxito - Purga Automática):** Given que existen candidatos almacenados, When la fecha alcanza su `fecha_expiracion_datos` (ej. 2 años de inactividad), Then un cron job debe purgar los archivos (CVs, Videos) de AWS S3 y ofuscar sus datos identificativos (PII) en la base de datos.
- **Escenario 2 (Edge Case - Candidato Activo):** Given que un candidato cumple el plazo de expiración, When el candidato se encuentra activo en el pipeline ("Entrevista" o posterior), Then el sistema debe extender automáticamente la caducidad por 6 meses y registrar la acción.
- **Escenario 3 (Error/Límite - Fallo en S3):** Given que se ejecuta el job de purga, When el sistema no logra borrar el CV físico de S3, Then debe ofuscar la DB, generar una alerta "Crítica" de seguridad y marcar el registro para intervención manual.

**🛠️ Notas Técnicas y No Funcionales:**
- **Performance:** Las tareas de purga masiva deben ejecutarse en horas de bajo tráfico corporativo (ej. 03:00 AM).
- **Analítica:** La ofuscación de datos mantiene las claves foráneas, garantizando que el Dashboard predictivo de contratación global no pierda precisión estadística.

**✅ Evaluación INVEST:**
- [x] **I**ndependent: Es un background worker completamente desacoplado del flujo de reclutamiento web.
- [x] **N**egociable: Los plazos de retención y la granularidad de la ofuscación son parametrizables.
- [x] **V**aluable: Fundamental para empresas enterprise operando en Europa o con regulaciones estrictas.
- [x] **E**stimable: Scripts de bases de datos y llamadas S3 son altamente conocidos y estimables.
- [x] **S**mall: Puede implementarse solo el job de borrado de DB antes de integrar el borrado físico de S3.
- [x] **T**estable: Manipulando la `fecha_expiracion_datos` en staging se puede forzar y auditar la purga.

---

### 🏷️ US-04: Multiposting de Vacantes (Omnicanalidad)
**Historia de Usuario:**
> Como Reclutador, quiero publicar una nueva vacante de manera simultánea en varios portales de empleo (LinkedIn, Glassdoor) desde un solo panel, para maximizar el alcance de candidatos minimizando el tiempo operativo.

**Criterios de Aceptación (BDD):**
- **Escenario 1 (Éxito - Publicación múltiple):** Given que tengo una vacante aprobada, When selecciono "LinkedIn" e "Indeed" y presiono "Distribuir", Then el sistema conecta mediante APIs, publica la oferta y devuelve los enlaces generados de ambas plataformas.
- **Escenario 2 (Edge Case - Límite de Caracteres):** Given que la descripción de la vacante excede los límites de una plataforma destino, When intento distribuirla, Then el sistema debe truncar el texto o advertir pre-vuelo (pre-flight validation) para que se ajuste a los requisitos del proveedor.
- **Escenario 3 (Error/Límite - API externa caída):** Given que envío la oferta a las plataformas, When la API de LinkedIn devuelve un error 500, Then el ATS publica con éxito en Indeed, marca LinkedIn con "Error de publicación" y habilita un botón de reintento local.

**🛠️ Notas Técnicas y No Funcionales:**
- **Integraciones:** Adaptadores de Salida (Arquitectura Hexagonal) dedicados para plataformas externas.
- **Tolerancia a fallos:** Implementar políticas de "Retry" asíncronas para manejar la intermitencia en redes sociales.

**✅ Evaluación INVEST:**
- [x] **I**ndependent: Este caso de uso aplica la relación de inclusión `<<include>>` modelada en UML pero corre en su propio flujo de red.
- [x] **N**egociable: Se puede empezar integrando 1 sola plataforma como MVP.
- [x] **V**aluable: Potencia drásticamente el flujo de talento orgánico hacia la empresa (Embudo de adquisición).
- [x] **E**stimable: La carga dependerá de la calidad de la documentación de API del proveedor externo.
- [x] **S**mall: Implementable en fases progresivas por cada portal integrado.
- [x] **T**estable: Probable contra los entornos *Sandbox* de los portales de terceros (ej. LinkedIn Developer).

---

### 🏷️ US-05: Evaluación Multimodal de Entrevistas Asíncronas
**Historia de Usuario:**
> Como Gerente de Adquisición de Talento, quiero que un agente inteligente analice los videos de entrevistas asíncronas, para obtener mediciones objetivas de habilidades blandas como la comunicación, el tono y la compatibilidad cultural.

**Criterios de Aceptación (BDD):**
- **Escenario 1 (Éxito - Reporte Emocional):** Given que un candidato sube su video respuesta, When el agente de IA lo procesa, Then devuelve un reporte (JSONB) identificando emociones, nivel de confianza en el habla y un resumen en texto del perfil actitudinal.
- **Escenario 2 (Edge Case - Baja calidad visual):** Given un video subido, When las condiciones de luz o resolución imposibilitan medir microexpresiones (menor a 480p), Then el agente visual omite esa métrica y se basa únicamente en el análisis de audio (NLP de transcripción y tono).
- **Escenario 3 (Error/Límite - Exceso de tamaño):** Given el formulario de entrevista en el portal de candidatos, When se intenta cargar un archivo >50MB, Then el Frontend (UI) bloquea instantáneamente la carga y solicita recortar el video.

**🛠️ Notas Técnicas y No Funcionales:**
- **Performance/Red:** Usar cargas *MultipartUpload* o pre-signed URLs hacia S3 para evitar saturar el ancho de banda del backend.
- **Inclusión y Equidad:** Los reclutadores podrán invalidar manualmente esta evaluación si el candidato tiene condiciones especiales declaradas de habla o motricidad.

**✅ Evaluación INVEST:**
- [x] **I**ndependent: Funcionalidad modular que extiende el proceso de evaluación según el UML `<<extend>>`.
- [x] **N**egociable: Puede limitarse a transcripción de audio inicialmente si el análisis visual es complejo.
- [x] **V**aluable: Digitaliza y estandariza las mediciones de 'soft skills', reemplazando entrevistas de primer filtro ineficientes.
- [x] **E**stimable: Requiere integración con APIs cognitivas existentes en el mercado (ej. AWS Rekognition/Transcribe).
- [x] **S**mall: Construir la prueba de concepto con un solo video es alcanzable.
- [x] **T**estable: Usar videos de control estandarizados para verificar que la IA detecta la misma línea base de emociones consistentemente.

---

## Backlog de Producto (Prompt Sencillo)

### Metodología de Priorización: MoSCoW
Para el contexto de LTI (un ATS/CRM impulsado por Inteligencia Artificial y enfocado en reclutamiento ético y cumplimiento normativo), la metodología **MoSCoW** (Must-have, Should-have, Could-have, Won't-have) es la más adecuada para definir el MVP (Minimum Viable Product). 

**Justificación:**
El sistema tiene requerimientos legales estrictos (RGPD) y promesas de valor fundamentales (XAI - Inteligencia Artificial Explicable). MoSCoW nos permite garantizar que el sistema no salga a producción sin cumplir con la ley y sin su principal diferenciador ético, relegando características atractivas pero secundarias a iteraciones posteriores.

### Backlog Priorizado

#### 🔴 MUST HAVE (Debe tener - Crítico para el MVP)
Estas historias conforman el núcleo operativo y ético-legal del ATS. Sin ellas, el producto carece de valor, viabilidad o incurre en graves riesgos regulatorios.
1. **US-01: Análisis Semántico y Matching de Currículums (NLP)**
   - *Razón:* Es el motor básico de cualquier ATS de nueva generación. Si los reclutadores no pueden evaluar y filtrar candidatos automáticamente, el sistema no resuelve el problema principal (carga administrativa).
2. **US-02: Auditoría y Justificación Ética de IA (XAI)**
   - *Razón:* Es la principal "Ventaja Competitiva" frente a soluciones tradicionales. Evita el modelo de "caja negra" y proporciona transparencia desde el primer día.
3. **US-03: Automatización del Cumplimiento RGPD (Borrado de Datos)**
   - *Razón:* Obligatorio legalmente. Operar un software de RR.HH. sin la gestión correcta del ciclo de vida de los datos personales expone a los clientes a multas millonarias.

#### 🟡 SHOULD HAVE (Debería tener - Importante pero no bloqueante)
Agregan un valor inmenso al negocio y a la experiencia de usuario, pero el sistema puede operar temporalmente sin ellas.
4. **US-04: Multiposting de Vacantes (Omnicanalidad)**
   - *Razón:* Es crucial para atraer candidatos, pero en un entorno inicial, los reclutadores pueden publicar manualmente en LinkedIn/Glassdoor y colocar el enlace de postulación hacia el ecosistema LTI.

#### 🔵 COULD HAVE (Podría tener - Deseable)
Funcionalidades avanzadas de alto impacto visual y funcional, pero que representan un alto costo técnico y de infraestructura.
5. **US-05: Evaluación Multimodal de Entrevistas Asíncronas**
   - *Razón:* Analizar microexpresiones y tono de voz es una característica altamente avanzada y premium. Encaja perfectamente en un segundo release o en un nivel de suscripción más alto (Tier Pro).

#### ⚪ WON'T HAVE (No tendrá - Fuera de alcance V1.0)
- *Ejemplo (Basado en PRD):* Generación automatizada de contratos laborales o módulo propio de gestión de nóminas (delegado vía integraciones).

---

## Backlog de producto con metodologia RICE con instrucciones de prompts especializados

A continuación, presento el Product Backlog refinado aplicando el framework estratégico DEEP y la metodología de priorización RICE (Reach, Impact, Confidence, Effort).

### 1. Tabla del Backlog

| ID | Prioridad | Título | Tipo | Estimación (Fibonacci) | Estado | RICE Score |
|---|:---:|---|---|:---:|---|:---:|
| **US-03** | 1 | Automatización del Cumplimiento RGPD (Borrado de Datos) | Story | 2 | Ready | **15.0** |
| **US-02** | 2 | Auditoría y Justificación Ética de IA (XAI) | Story | 3 | Ready | **8.0** |
| **US-01** | 3 | Análisis Semántico y Matching de Currículums (NLP) | Story | 5 | Ready | **4.8** |
| **US-04** | 4 | Multiposting de Vacantes (Omnicanalidad) | Epic / Story | 8 | In Refinement | **2.5** |
| **SP-01** | 5 | Spike: Pruebas de APIs Cognitivas para Análisis de Video | Spike | 3 | Ready | **N/A** |
| **US-05** | 6 | Evaluación Multimodal de Entrevistas Asíncronas | Story | 13 | Blocked | **0.38** |

### 2. Justificación de Prioridad (Metodología RICE)

El cálculo de RICE asume una escala de Alcance (Reach) de 1 a 10 y un Impacto (Impact) de 1 a 3. 

1. **US-03 (Cumplimiento RGPD):** 
   * *Cálculo:* R:10 (Aplica a toda la base) * I:3 (Riesgo legal crítico) * C:100% (Backend jobs predecibles) / E:2 = **15.0**.
   * *Razón:* Mitigar el riesgo de multas millonarias por privacidad es la prioridad #1. El esfuerzo es bajo y la ganancia es enorme.
2. **US-02 (Auditoría XAI):** 
   * *Cálculo:* R:10 * I:3 (Ventaja Injusta comercial) * C:80% / E:3 = **8.0**.
   * *Razón:* Es la propuesta de valor core de LTI. Genera un alto impacto comercial con un esfuerzo técnico moderado (solo requiere guardar el log y mostrarlo).
3. **US-01 (Matching NLP):** 
   * *Cálculo:* R:10 * I:3 (Core del ATS) * C:80% / E:5 = **4.8**.
   * *Razón:* Esencial para el negocio, pero el esfuerzo de implementar parsers asíncronos en Kafka aumenta la estimación.
4. **US-04 (Multiposting):** 
   * *Cálculo:* R:10 * I:2 (Ahorro de tiempo, pero es manualizable) * C:100% / E:8 = **2.5**.
   * *Razón:* Su estimación (8) disminuye dramáticamente el puntaje RICE debido a la complejidad de integrar múltiples APIs de terceros simultáneamente.
5. **US-05 (Multimodal de Video):** 
   * *Cálculo:* R:5 (No todos envían video) * I:2 * C:50% (Incertidumbre tecnológica enorme) / E:13 = **0.38**.
   * *Razón:* Alto riesgo y alto esfuerzo. Destruye el ROI temporal. Se requiere investigación previa (Spike).

### 3. Análisis de Riesgos (Gestión de Incertidumbre)

* **Riesgo Tecnológico y de Tiempos (US-01):** Extraer datos estructurados de un PDF sin formato fijo usando IA es propenso a latencias. Si la lectura excede los 3 segundos, se bloqueará la experiencia del usuario (por eso se planteó Kafka en los BDD).
* **Dependencias de Redes Sociales (US-04):** Integrarse a LinkedIn o Glassdoor depende estrictamente de cambios en sus APIs, *Rate Limiting* y posibles caídas del proveedor que bloqueen nuestras publicaciones.
* **Incertidumbre Extrema en Rendimiento (US-05):** Procesar y almacenar videos de 50MB para analizar microexpresiones tiene una complejidad algorítmica brutal. Presenta riesgos de escalabilidad (costos de S3/Bandwidth) y riesgos éticos (falsos positivos en lectura facial).

### 4. Sugerencia de Refinamiento (Grooming)

Como Product Owner, mi evaluación sobre la "Definición de Preparado" (Definition of Ready - DoR) es la siguiente:

1. **Para US-04 (Multiposting):** 
   * *Acción:* La estimación de 8 indica que estamos frente a una Épica. Sugiero aplicar un **patrón de división vertical por conector**. 
   * *Solución:* Cortar la US-04 en `US-04a: Multiposting LinkedIn` (Estimación: 3) y `US-04b: Multiposting Indeed` (Estimación: 3). Esto aumentará el RICE individual y permitirá incluirlas fácilmente en un Sprint.
2. **Para US-05 (Evaluación Multimodal de Video):** 
   * *Acción:* Actualmente **no cumple** el Definition of Ready (DoR). Una estimación de 13 y confianza del 50% significa que el equipo de desarrollo no tiene claro cómo implementarlo.
   * *Solución:* Mantener la US-05 bloqueada. En el próximo Sprint, introducir la tarea de investigación estructurada **SP-01 (Spike)** asignada al Arquitecto de Software para crear una prueba de concepto conectándose a *AWS Rekognition*. Una vez resuelta la incertidumbre, volver a estimar US-05.

---

## Backlog de producto con metodologia MoSCoW con instrucciones de prompts especializados

Como Guardián del Backlog, he aplicado el framework DEEP y la metodología **MoSCoW** (Must-have, Should-have, Could-have, Won't-have) para delimitar el Minimum Viable Product (MVP) garantizando el cumplimiento legal y el valor core del ATS.

### 1. Tabla del Backlog

| ID | Prioridad (MoSCoW) | Título | Tipo | Estimación (Fibonacci) | Estado |
|---|:---:|---|---|:---:|---|
| **US-03** | Must Have 🔴 | Automatización del Cumplimiento RGPD | Story | 2 | Ready |
| **US-02** | Must Have 🔴 | Auditoría y Justificación Ética (XAI) | Story | 3 | Ready |
| **US-01** | Must Have 🔴 | Análisis Semántico y Matching de CVs | Story | 5 | Ready |
| **US-04** | Should Have 🟡 | Multiposting de Vacantes (Omnicanalidad) | Epic | 8 | In Refinement |
| **SP-01** | Should Have 🟡 | Spike: Evaluación de APIs para Video | Spike | 3 | Ready |
| **US-05** | Could Have 🔵 | Evaluación Multimodal de Entrevistas | Story | 13 | Blocked |

### 2. Justificación de Prioridad (Metodología MoSCoW)

* **MUST HAVE (Innegociables para el MVP):**
  * **US-03 (RGPD):** Si no gestionamos el borrado de datos, el sistema es ilegal en Europa. El riesgo normativo lo convierte en la prioridad máxima absoluta.
  * **US-02 (Auditoría XAI):** Es la promesa de marca ("Reclutamiento Ético"). Sin esto, somos un ATS tradicional más del montón.
  * **US-01 (Matching NLP):** Es la base de la reducción de la carga administrativa. Sin parsing automático, no hay producto.
* **SHOULD HAVE (Importantes pero no bloqueantes):**
  * **US-04 (Multiposting):** Atrae mucho tráfico, pero temporalmente los reclutadores pueden publicar a mano. 
  * **SP-01 (Spike de Video):** Debe ejecutarse pronto para mitigar el riesgo futuro, pero no frena el flujo principal de candidatos basados en texto.
* **COULD HAVE (Deseables si hay capacidad):**
  * **US-05 (Video Asíncrono):** Muy costoso y complejo. Se prioriza para una versión V2 o como un add-on "Premium".

### 3. Análisis de Riesgos (Gestión de Incertidumbre)

* **Dependencia de Proveedores (US-04):** Integrarse a LinkedIn/Glassdoor nos sujeta a sus cambios de API. Si cambian un endpoint, el multiposting fallará.
* **Latencia y Fallos de IA (US-01):** El parsing con NLP o LLMs puede tardar o fallar con PDFs escaneados (como imágenes). Riesgo de mala experiencia si no se maneja asíncronamente (Kafka).
* **Viabilidad Técnica y Costos (US-05):** Analizar 50MB de video en tiempo real requiere GPUs y mucho ancho de banda. Además, los modelos de microexpresiones tienen riesgos éticos y de falsos positivos altísimos.

### 4. Sugerencia de Refinamiento (Grooming)

* **Falta de Preparación (DoR) en US-05:** La historia de evaluación de video es demasiado grande (13 puntos) y altamente incierta. He creado el **SP-01 (Spike)** para que el equipo investigue soluciones empaquetadas (AWS Rekognition) antes de intentar desarrollarlo. La US-05 queda bloqueada.
* **Descomposición Obligatoria en US-04:** Una estimación de 8 sugiere que la historia cruza demasiados límites (múltiples APIs). Aplicando *Slicing Vertical*, sugiero descomponerla en:
  * `US-04a: Publicación en LinkedIn` (Est. 3)
  * `US-04b: Publicación en Indeed` (Est. 3)
  Esto permitirá entregar valor real en menos tiempo y encajar en un Sprint estándar.


## Tickets de trabajo 

### 🧠 Proceso de Pensamiento (Chain of Thought)
- **Análisis de Dependencias:** El flujo afecta el modelo de datos `CURRICULUM` y `CANDIDATO`. A nivel de sistema, el procesamiento de PDFs pesados en tiempo real bloquea el Event Loop de Node.js, por lo que el Input no debe ser el binario en base64 en la petición REST, sino una pre-signed URL o referencia a AWS S3.
- **Identificación de Riesgos:** **Alta incertidumbre** en el motor de NLP para extraer *skills* de PDFs sin estructura predecible. La limitación de "< 3 segundos" solicitada en el BDD requiere procesamiento asíncrono estricto. Recomiendo que el adaptador NLP esté diseñado de forma agnóstica para poder intercambiar proveedores (AWS Textract vs GPT-4 API) en caso de un Spike futuro.
- **Contrato Sugerido (Input/Output API/DTO):**
  - **Entrada (Payload de Evento Kafka o POST Request):**
    ```json
    {
      "candidateId": "uuid-1234",
      "vacancyId": "uuid-5678",
      "cvFileUri": "s3://lti-bucket/resumes/uuid-1234.pdf"
    }
    ```
  - **Salida (Respuesta o Evento Emitido de Éxito):**
    ```json
    {
      "candidateId": "uuid-1234",
      "matchScore": 85,
      "extractedSkills": ["React", "TypeScript", "Node.js"],
      "status": "PROCESSED_SUCCESSFULLY"
    }
    ```

---

### 🎫 TICKET 1: [Dominio] Entidad Curriculum y MatchCalculatorService

1. **[Título]:** [Dominio] Implementar Entidad `Curriculum` y Servicio `MatchCalculatorService`.
2. **[Descripción]:** Encapsular la lógica de negocio pura que representa un currículum y el algoritmo determinista que compara los *skills* extraídos contra los requeridos por la vacante para obtener el porcentaje de afinidad.
3. **[Criterios de Aceptación BDD]:**
   - *Given* un arreglo de skills requeridas y un arreglo de skills extraídas, *When* el servicio ejecuta `calculateMatch()`, *Then* retorna un número del 0 al 100 sin afectar estados externos.
4. **[Prioridad]:** Crítica (Bloquea a las capas superiores).
5. **[Estimación]:** **2 pts**. Tarea de muy baja incertidumbre y baja complejidad. Solo es TypeScript puro (POJOs), sin dependencias externas.
6. **[Asignación Sugerida]:** Backend Developer.
7. **[Tags]:** `#Domain`, `#BusinessLogic`.
8. **[Notas Técnicas]:**
   - Crear: `src/domain/entities/Curriculum.ts`.
   - Crear: `src/domain/services/MatchCalculatorService.ts`.
9. **[Referencias]:** US-01.
10. **[Definition of Done (DoD)]:** 
    - [ ] Lógica implementada sin importar librerías de infraestructura.
    - [ ] 100% de Test Coverage (Jest) en el servicio, verificando edge cases (ej. CV sin skills, vacante sin skills).

---

### 🎫 TICKET 2: [Aplicación] Caso de Uso ProcessCurriculumUseCase

1. **[Título]:** [Aplicación] Implementar `ProcessCurriculumUseCase` para orquestación.
2. **[Descripción]:** Crear el caso de uso que controla el flujo principal: Recibe el DTO de entrada, descarga el CV vía puerto de Storage, lo envía al puerto de NLP, calcula el score con el Dominio y persiste el resultado vía puerto de Base de Datos.
3. **[Criterios de Aceptación BDD]:**
   - *Given* un Input DTO válido validado con Zod, *When* el caso de uso es invocado, *Then* llama correctamente a todos los puertos en orden y retorna el DTO de salida de éxito.
4. **[Prioridad]:** Alta.
5. **[Estimación]:** **3 pts**. Tarea estándar de orquestación. No implementa I/O real, pero requiere la definición rigurosa de las interfaces (Puertos).
6. **[Asignación Sugerida]:** Backend Developer.
7. **[Tags]:** `#Application`, `#UseCase`, `#Ports`.
8. **[Notas Técnicas]:**
   - Crear interfaces: `INlpParserPort`, `ICurriculumRepositoryPort`.
   - Crear: `src/application/use-cases/ProcessCurriculumUseCase.ts`.
   - Validación del payload entrante usando `Zod`.
9. **[Referencias]:** US-01, Ticket 1.
10. **[Definition of Done (DoD)]:**
    - [ ] Puertos (Interfaces) bien documentados y expuestos.
    - [ ] Tests unitarios inyectando Mocks de las dependencias.
    - [ ] Manejo explícito de excepciones de dominio (ej. `InvalidResumeFormatError`).

---

### 🎫 TICKET 3: [Infraestructura] Adaptador NLP, Repositorio y Consumer Kafka

1. **[Título]:** [Infraestructura] Integración PostgreSQL, API externa de NLP y Kafka Consumer.
2. **[Descripción]:** Implementación técnica de los adaptadores (Driven/Driving). Conecta la aplicación con AWS/Kafka para leer el evento de inicio, implementa la llamada HTTP real hacia el motor cognitivo, y guarda el `Curriculum` analizado en la BD.
3. **[Criterios de Aceptación BDD]:**
   - *Given* un mensaje en el topic Kafka `cv.uploaded`, *When* falla la API externa de NLP, *Then* el sistema debe reintentar hasta 3 veces antes de enviarlo a un Dead Letter Queue (DLQ).
4. **[Prioridad]:** Alta.
5. **[Estimación]:** **5 pts**. Alta complejidad por la coordinación de múltiples APIs reales externas, configuración de la base de datos (ORMs) y manejo de errores asíncronos y latencia de red.
6. **[Asignación Sugerida]:** Backend/Integrations Developer.
7. **[Tags]:** `#Infrastructure`, `#Kafka`, `#Database`, `#ExternalAPI`.
8. **[Notas Técnicas]:**
   - Crear: `src/infrastructure/database/PrismaCurriculumRepository.ts`.
   - Crear: `src/infrastructure/services/OpenAiNlpAdapter.ts` (Implementa `INlpParserPort`).
   - Crear: `src/infrastructure/messaging/KafkaCurriculumConsumer.ts`.
9. **[Referencias]:** US-01, Ticket 2.
10. **[Definition of Done (DoD)]:**
    - [ ] Adaptadores cumplen el contrato dictado por los Puertos de Aplicación.
    - [ ] Esquema Prisma (`schema.prisma`) actualizado y migraciones generadas.
    - [ ] Integration Tests comprobando flujos completos con BD real de testing y Mock Server (`nock`) para la API externa.
