# Prompts utilizados

Se uso NotebookLM para construir la conceptualización, el modelo de negocio y la arquitectura del sistema LTI:

## prompts para crear el contexto en NotebookLM

### Dominio del Problema

**1. Prompts para entender el Ecosistema y los "Dolores" de Recursos Humanos**
El primer paso para definir el dominio del problema es identificar las tareas que consumen tiempo y generan frustración en los clientes:
*   "¿Qué es un sistema ATS (Applicant Tracking System) y cuáles son las principales fricciones en su uso diario?".
*   "¿Cuáles son los mayores retos de productividad y pérdida de tiempo que sufren los departamentos de RR. HH. en la selección de personal?"
*   "Cómo afecta la mala experiencia del candidato (candidate experience) durante el proceso de postulación a las empresas."
*   "¿Qué alternativas o soluciones rudimentarias usan actualmente las empresas para el emparejamiento de talento cuando no tienen un ATS moderno?".

**2. Prompts para investigar la problemática de la Inteligencia Artificial (Sesgos y "Caja Negra")**
Uno de los problemas centrales que LTI busca resolver es la falta de ética y transparencia en la tecnología actual:
*   "Riesgos de sesgo algorítmico y discriminación en el uso de Inteligencia Artificial para el reclutamiento de talento".
*   "¿Qué es el problema de la 'caja negra' en los algoritmos de aprendizaje profundo aplicados a Recursos Humanos?".
*   "Diferencias entre la IA tradicional y la IA Explicable (XAI) para mitigar decisiones arbitrarias en la selección de personal".
*   "Casos de estudio sobre algoritmos de contratación que han mostrado sesgos contra mujeres o minorías".

**3. Prompts para delimitar las Restricciones Legales y de Privacidad de Datos**
El dominio del problema también está delimitado por el marco regulatorio en el que operará el software:
*   "¿Cuáles son las obligaciones legales y de cumplimiento del RGPD (Reglamento General de Protección de Datos) para las plataformas de software ATS?".
*   "Privacidad de datos en la contratación: gestión del consentimiento y derechos de los candidatos frente a la toma de decisiones automatizada".
*   "Requisitos de la Ley de Inteligencia Artificial de la UE para sistemas de IA de alto riesgo aplicados al empleo".

**4. Prompts para la Metodología de Validación del Problema**
Para estructurar el análisis del dominio del problema desde la perspectiva del emprendimiento y la ingeniería de software:
*   "Cómo diseñar entrevistas de problema y validación de clientes según la metodología Running Lean de Ash Maurya".
*   "Cómo identificar a los 'Early Adopters' (primeros usuarios) que padecen el problema de manera más crítica en un modelo de negocio B2B".
*   "Técnicas de abstracción en el modelado de sistemas para separar el dominio del problema de los detalles de la solución de software".

### Base Técnica

**1. Prompts sobre Arquitectura de Software y Diseño de Alto Nivel**
Para definir la estructura base del sistema, el aislamiento de la lógica de negocio y la comunicación entre los servicios:
* "¿Cuáles son las diferencias entre Clean Architecture y Arquitectura Hexagonal, y cuándo conviene usar cada una?".
* "Cómo integrar el Diseño Guiado por el Dominio (DDD) dentro de una Arquitectura Hexagonal definiendo entidades, puertos y adaptadores".
* "Patrones de observabilidad y diseño resiliente en arquitecturas de microservicios".
* "Mejores prácticas para implementar arquitecturas orientadas a eventos (Event-Driven) y microservicios modernos".

**2. Prompts sobre UML y Casos de Uso**
Para establecer los requisitos funcionales y entender las interacciones de los actores con el sistema:
* "Mejores prácticas, tutoriales y ejemplos para diseñar diagramas de casos de uso efectivos".
* "Definición formal y diferencias entre las relaciones 'include' y 'extend' en los diagramas de casos de uso de UML".
* "¿Es útil seguir utilizando casos de uso y diagramas UML en proyectos con metodologías ágiles o Scrum?".

**3. Prompts sobre Modelado de Bases de Datos**
Para diseñar la estructura de persistencia políglota y asegurar la integridad de la información:
* "Cómo definir e identificar correctamente entidades, atributos y relaciones en el diseño de bases de datos".
* "Guía paso a paso para crear un diagrama Entidad-Relación (ER) y documentar restricciones y supuestos".
* "Cómo aplicar las reglas de Codd y el proceso de normalización de bases de datos usando claves primarias y dependencias funcionales".
* "Reglas para la transformación de un modelo conceptual Entidad-Relación a un modelo relacional físico".

**4. Prompts sobre el Modelo C4**
Para visualizar la arquitectura desde una perspectiva de alto nivel (contexto) hasta el detalle de los componentes:
* "¿Qué es el modelo C4 de Simon Brown, cuáles son sus 4 niveles principales de abstracción y sus componentes?".
* "Comparación entre el Modelo C4 y UML: ¿cuál elegir para documentar sistemas de software modernos?".
* "Cómo pensar y preparar la arquitectura de software usando las abstracciones del modelo C4 antes de empezar a dibujar los diagramas".
* "Cómo documentar arquitecturas en la nube integrando el Modelo C4 con AWS y Terraform".
* "El uso de diagramas de soporte (panorama, despliegue y dinámicos) para complementar el modelo C4".

**5. Prompts sobre Herramientas Técnicas y Diagramas como Código (DaC)**
Para automatizar la documentación y elegir las mejores plataformas de dibujo arquitectónico:
* "¿Cuáles son las mejores herramientas de software para crear y compartir diagramas de arquitectura C4?".
* "Guía práctica y sintaxis para crear diagramas del modelo C4 utilizando el lenguaje de marcado Mermaid.js".
* "Cómo documentar arquitectura de software combinando el modelo C4 con PlantUML (C4-PlantUML)".
* "Generación y visualización de diagramas del modelo C4 utilizando herramientas impulsadas por Inteligencia Artificial".


## Prompts para el modelo de negocio y tecnicos

1. **"Se creara un software relacionado con ATS llamado LTI, genera una breve descripcion, valor ananido y las ventajas competitivas."**
2. **"Actúa como Product Manager Senior. Necesito un PRD del proyecto LTI."**
3. **"En tu rol analista de software experto. Enumera y describe los tres casos de uso más importantes a implementar para lograr una funcionalidad básica, usa las buenas practicas uml, los Dac realizalos en el marcado Marmaid."**
4. **"En tu rol analista de software experto. Enumera y describe los tres casos de uso principales a implementar para lograr una funcionalidad básica, usa las buenas practicas uml, los Dac realizalos en el marcado Marmaid."**
5. **"En tu rol analista de software experto. Enumera y describe los tres casos de uso más importantes cada uno con su diagragma, usa las buenas practicas uml, los Dac realizalos en el marcado Marmaid."**
6. **"En tu rol analista de software experto. Enumera y describe los tres casos de uso más importantes cada uno con su diagragma para el sistema LTI, usa las buenas practicas uml, los Dac realizalos en el marcado Marmaid."**
7. **"Actúa como un DBA y Arquitecto de Software Senior. realiza el Modelo de datos que cubra entidades, atributos (nombre y tipo) y relaciones, del proyecto LTI."**
18. **"pasemos al diseno del sistema y arquitectura de alto nivel."**
19. **"en arquitectura hexagonal?"**
20. **"Diseño del sistema a alto nivel, usando arquitectura heagonal, tanto explicado como diagrama adjunto"**
21. **"Diseño del sistema de LTI a alto nivel, usando arquitectura heagonal, tanto explicado como diagrama adjunto"**
22. **"Diagrama C4 que llegue en profundidad a uno de los componentes mas importantes del sistema, el que prefieras."**
23. **"prompts para recopilar información del dominio del problema"**
24. **"promps de fuetes para la arquitectura, casos de uso, c4, y demas detalles tecnicos"**
25. **"promps de fuetes para la arquitectura, casos de uso, modelo de datos, Diseño del sistema a alto nivel,  c4, y demas detalles tecnicos"**

## Prompts mejorados por la IA

Basado en los prompts anteriores, se le pidio a la ia que los mejorara, el resultado fue el siguiente:

26. **"Mejora los prompts antes listados"**

### 1. Prompts para Producto y Modelo de Negocio (PRD y Lean Canvas)
*En lugar de pedir solo "una breve descripción", le damos el rol de Product Manager y le exigimos un formato estructurado.*

> **Prompt Mejorado:** "Actúa como un Product Manager Senior. Estamos diseñando un Applicant Tracking System (ATS) impulsado por Inteligencia Artificial Agéntica llamado 'LTI'. Tu objetivo es crear un Documento de Requisitos del Producto (PRD) y un diagrama Lean Canvas estructurado. Detalla claramente el problema del mercado, nuestra Propuesta de Valor Única (basada en IA explicable y análisis multimodal) y nuestra ventaja competitiva. Para el Lean Canvas, presenta el resultado en una tabla clara y orientada a modelos B2B."

### 2. Prompts para Casos de Uso y UML
*Para evitar diseños genéricos, introducimos las reglas formales de UML y le indicamos a la IA cómo debe programar el diagrama para que no falle.*

> **Prompt Mejorado:** "Actúa como un Analista de Software Experto. Para el sistema ATS 'LTI', describe los 3 casos de uso principales. Utiliza estrictamente las buenas prácticas de UML: aplica relaciones de inclusión (`<<include>>`) para comportamientos obligatorios que se re-usan y relaciones de extensión (`<<extend>>`) para secuencias alternativas o excepciones. Genera el diagrama de Casos de Uso como código (Diagrams as Code) utilizando Mermaid.js. **Importante:** Utiliza identificadores de nodos cortos, alfanuméricos y sin espacios para evitar errores de renderizado (ej. usa `UC1` en lugar de textos largos en las conexiones)."

### 3. Prompts para Modelado de Bases de Datos
*Aquí aplicamos principios de ingeniería de datos para asegurar que la IA separe correctamente las entidades de los atributos y aplique las formas normales.*

> **Prompt Mejorado:** "Actúa como un Administrador de Bases de Datos (DBA) y Arquitecto Senior. Diseña el modelo de datos relacional para el proyecto LTI aplicando las reglas de normalización hasta la Tercera Forma Normal (3NF). Identifica correctamente las entidades (sustantivos con existencia propia) y atributos (adjetivos o propiedades), evitando guardar atributos derivados. Genera el código estructural en sintaxis estricta DBML con tipos de datos nativos de PostgreSQL, e incluye también el Diagrama Entidad-Relación (ERD) en Mermaid.js usando la notación Crow's Foot."

### 4. Prompts para Diseño del Sistema a Alto Nivel (C4 y Hexagonal)
*El error común es pedir arquitectura sin especificar el nivel de profundidad. Usamos el modelo C4 como herramienta de pensamiento estructural* *y definimos el patrón esperado.*

> **Prompt Mejorado:** "Actúa como Arquitecto de Software Cloud. Diseña la arquitectura del sistema LTI utilizando el Modelo C4 de Simon Brown integrado con los principios de la Arquitectura Hexagonal (Puertos y Adaptadores) para aislar la lógica de negocio. 
> 1. Explica cómo interactúan el núcleo del dominio, los puertos y los adaptadores de entrada/salida.
> 2. Genera un diagrama C4 de Nivel 2 (Contenedores) o Nivel 3 (Componentes) utilizando sintaxis Mermaid.js.
> Asegúrate de detallar el uso de persistencia políglota y una comunicación basada en eventos asíncronos (Event-Driven) para el ecosistema de IA."

---

## Prompts de requisitos Creación del Backlog de Producto LTI

### 1. Generar las User Stories

> **Prompt:** 

```text
# ROL
Actúa como un Senior Product Manager y QA Engineer experto en metodologías BDD (Behavior-Driven Development). Tu objetivo es transformar ideas de funcionalidades en User Stories profesionales listas para desarrollo.

# INSTRUCCIONES DE CALIDAD
Analiza el archivo LTI-JDLM.md y genera las User Stories correspondientes siguiendo el estándar de calidad de la industria y el ejemplo de referencia que te proporciono a continuación:

Cada User Story que generes debe cumplir estrictamente con:
1. Formato Estándar: "Como [rol], quiero [acción], para [beneficio]".
2. Criterios de Aceptación BDD: Formato Given/When/Then, cubriendo el Happy Path y al menos un Edge Case o escenario de error.
3. Especificaciones Técnicas: Incluir límites de performance (ej. ms), accesibilidad y sugerencias de stack.
4. Evaluación INVEST: Un checklist final validando por qué la historia es Small, Testable, etc.

# EJEMPLO DE REFERENCIA (ESTÁNDAR DE ORO)
[Título: Búsqueda inteligente de cursos]
[Historia: Como estudiante... quiero buscar... para encontrar rápidamente...]
[AC 1: Dado que estoy en home... cuando escribo 3 caracteres... entonces sugerencias en <500ms]
[AC 2: Escenario de error: Si no hay coincidencia, mostrar "Sin resultados" y sugerencias por categoría]

# TAREA
Basado en el estándar anterior, genera la User Story completa para la siguiente funcionalidad:
> [INSERTAR FUNCIONALIDAD AQUÍ - Ej: Registro de perfil capilar con foto]

# FORMATO DE SALIDA
### 🏷️ [Título de la Story]
**Historia de Usuario:**
> Como... Quiero... Para...

**Criterios de Aceptación (BDD):**
- **Escenario 1 (Éxito):** Given... When... Then...
- **Escenario 2 (Edge Case):** Given... When... Then...
- **Escenario 3 (Error/Límite):** Given... When... Then...

**🛠️ Notas Técnicas y No Funcionales:**
- (Performance, Accesibilidad, Seguridad, Integraciones sugeridas)

**✅ Evaluación INVEST:**
- [ ] **I**ndependent: (Breve explicación)
- [ ] **N**egociable: (...)
- [ ] **V**aluable: (...)
- [ ] **E**stimable: (...)
- [ ] **S**mall: (...)
- [ ] **T**estable: (...)
```

guarda las User Stories generadas en el archivo  /LTI-JDLM/UserStories-JDLM.md.

> **Respuesta del agente**

```text
He analizado el archivo de requerimientos y arquitectura (LTI-JDLM.md) y he generado un conjunto completo de User Stories basadas en las funcionalidades core del ecosistema ATS/CRM, utilizando el estándar BDD y los criterios de evaluación INVEST solicitados.

El archivo ha sido creado y guardado exitosamente en la siguiente ruta: /LTI-JDLM/UserStories-JDLM.md

Dentro del archivo encontrarás 5 historias de usuario clave que cubren los aspectos más importantes del sistema:

US-01: Análisis Semántico y Matching de Currículums (NLP)
US-02: Auditoría y Justificación Ética de IA (XAI)
US-03: Automatización del Cumplimiento RGPD (Borrado de Datos)
US-04: Multiposting de Vacantes (Omnicanalidad)
US-05: Evaluación Multimodal de Entrevistas Asíncronas
Cada historia incluye escenarios para el Happy Path, casos límite (Edge Cases) y situaciones de error, además de notas técnicas sobre performance, integraciones y su correspondiente checklist de validación INVEST.
```


### 2. Backlog de producto

#### Prompt sencillo

> **Prompt 1:** 
```text
Arma el Backlog de producto con las User Stories del archivo UserStories-JDLM.md, analiza que metodología de priorización que se ajuste al contexto de la app, guardalo como Backlog con promp sencillo en el archivo UserStories-JDLM.md.
```

> **Respuesta del agente**

```text
He creado el Backlog de producto basado en las User Stories previamente generadas.

Tras analizar el contexto de LTI (un ATS avanzado cuyo gran diferencial es la inteligencia artificial ética y el estricto cumplimiento normativo), he seleccionado la metodología MoSCoW (Must-have, Should-have, Could-have, Won't-have). Esta metodología es la más apropiada para delimitar claramente el Minimum Viable Product (MVP), asegurando que ninguna versión salga a producción sin cumplir la ley (RGPD) y entregando la promesa de valor central (XAI y parsing de CVs).

El resultado se ha guardado exitosamente al final del archivo /LTI-JDLM/UserStories-JDLM.md bajo la sección Backlog de Producto (Prompt Sencillo).
```

> **Analisis personal**

Parece muy generico muy pocos detalles no se ajusta a la realidad del producto.

#### Prompt estructurado definiendo metodologia RICE y buenas practicas de Backlog.

> **Prompt:** 
```text
# ROL
Actúa como un Senior Product Owner y Estratega Ágil. Tu especialidad es la gestión, refinamiento y optimización de Product Backlogs para productos de software de alta complejidad. Tu objetivo es asegurar que el backlog sea siempre DEEP (Detailed, Emergent, Estimated, Prioritized).

# CONTEXTO DEL PRODUCTO
Analiza las user stories del archivo UserStories-JDLM.md y arma el Backlog de producto, utiliza la metodologia RICE.

# MARCO ESTRATÉGICO
Para cada interacción, debes aplicar estos marcos de trabajo:
1. Modelo DEEP: Mantener el backlog detallado arriba y grueso abajo.
2. Metodología de Priorización: Aplicar RICE o MoSCoW según se solicite para justificar el orden.
3. Slicing Vertical: Asegurar que cada elemento del backlog entregue una funcionalidad completa de punta a punta.
4. Gestión de Incertidumbre: Identificar elementos con alto riesgo técnico y sugerir transformarlos en "Spikes" antes de estimarlos.

# REGLAS DE REFINAMIENTO (Grooming)
- Definición de Preparado (DoR): No permitas que una historia suba al tope del backlog si no tiene Criterios de Aceptación (BDD) claros.
- Descomposición: Si una historia es demasiado grande para un Sprint (Epic), divídela automáticamente usando patrones de división de historias.
- Valor vs. Esfuerzo: Analiza siempre si el esfuerzo técnico (Fibonacci) se justifica con el valor de negocio esperado.

# PROTOCOLO DE RESPUESTA
Cada vez que analicemos o generemos elementos para el backlog, estructura tu salida así:
1. Tabla del Backlog: [ID | Prioridad | Título | Tipo (Story/Bug/Spike) | Estimación | Estado].
2. Justificación de Prioridad: Explicación breve de por qué este elemento está en esa posición (usando MoSCoW o RICE).
3. Análisis de Riesgos: Identificación de dependencias técnicas o bloqueos potenciales.
4. Sugerencia de Refinamiento: Qué falta para que los elementos superiores pasen a estado "Ready".

# TAREA INICIAL
He comprendido mi rol como Guardián del Backlog. Estoy listo para organizar, priorizar y detallar el backlog de tu proyecto. Por favor, proporcióname la lista de ideas, épicas o funcionalidades actuales para empezar el proceso de refinamiento.

Guarda el Backlog de producto generado en el archivo UserStories-JDLM.md, con el titulo Backlog de producto con metodologia RICE con instrucciones de prompts especializados

```

> **Respuesta del agente**

```text
He añadido exitosamente el Backlog de Producto utilizando la metodología RICE al final del archivo /LTI-JDLM/UserStories-JDLM.md.

Este nuevo backlog estructurado incluye:

La Tabla del Backlog con el cálculo del RICE Score para priorizar objetivamente el valor y el esfuerzo.
La Justificación de la Prioridad, detallando por qué las normativas (US-03) y el core ético (US-02) lideran la lista sobre características complejas.
Un Análisis de Riesgos y Gestión de Incertidumbre, resaltando problemas de latencia, dependencias de APIs de terceros y alta complejidad en análisis de video.
Sugerencias de Refinamiento (Grooming), donde propongo dividir la épica de Multiposting por red social y lanzar un Spike técnico (SP-01) para resolver la incertidumbre de la evaluación multimodal (US-05).
```

> **Analisis personal**


El análisis de riesgos es sólido y refleja las preocupaciones reales de arquitectura de software. La "Incertidumbre Extrema en Rendimiento" para la US-05 es correcta, ya que el análisis de video es computacionalmente costoso y los modelos de IA para microexpresiones todavía son experimentales en cuanto a costo-beneficio en tiempo real.

#### Prompt estructurado definiendo metodologia MoSCoW y buenas practicas de Backlog.

> **Prompt:** 
```text

# ROL
Actúa como un Senior Product Owner y Estratega Ágil. Tu especialidad es la gestión, refinamiento y optimización de Product Backlogs para productos de software de alta complejidad. Tu objetivo es asegurar que el backlog sea siempre DEEP (Detailed, Emergent, Estimated, Prioritized).

# CONTEXTO DEL PRODUCTO
Analiza las user stories del archivo UserStories-JDLM.md y arma el Backlog de producto, utiliza la metodologia MoSCoW.

# MARCO ESTRATÉGICO
Para cada interacción, debes aplicar estos marcos de trabajo:
1. Modelo DEEP: Mantener el backlog detallado arriba y grueso abajo.
2. Metodología de Priorización: Aplicar RICE o MoSCoW según se solicite para justificar el orden.
3. Slicing Vertical: Asegurar que cada elemento del backlog entregue una funcionalidad completa de punta a punta.
4. Gestión de Incertidumbre: Identificar elementos con alto riesgo técnico y sugerir transformarlos en "Spikes" antes de estimarlos.

# REGLAS DE REFINAMIENTO (Grooming)
- Definición de Preparado (DoR): No permitas que una historia suba al tope del backlog si no tiene Criterios de Aceptación (BDD) claros.
- Descomposición: Si una historia es demasiado grande para un Sprint (Epic), divídela automáticamente usando patrones de división de historias.
- Valor vs. Esfuerzo: Analiza siempre si el esfuerzo técnico (Fibonacci) se justifica con el valor de negocio esperado.

# PROTOCOLO DE RESPUESTA
Cada vez que analicemos o generemos elementos para el backlog, estructura tu salida así:
1. Tabla del Backlog: [ID | Prioridad | Título | Tipo (Story/Bug/Spike) | Estimación | Estado].
2. Justificación de Prioridad: Explicación breve de por qué este elemento está en esa posición (usando MoSCoW o RICE).
3. Análisis de Riesgos: Identificación de dependencias técnicas o bloqueos potenciales.
4. Sugerencia de Refinamiento: Qué falta para que los elementos superiores pasen a estado "Ready".

# TAREA INICIAL
He comprendido mi rol como Guardián del Backlog. Estoy listo para organizar, priorizar y detallar el backlog de tu proyecto. Por favor, proporcióname la lista de ideas, épicas o funcionalidades actuales para empezar el proceso de refinamiento.

Guarda el Backlog de producto generado en el archivo UserStories-JDLM.md, con el titulo Backlog de producto con metodologia MoSCoW con instrucciones de prompts especializados

```

> **Respuesta del agente**

```text
He generado y añadido el Backlog de Producto estructurado con la metodología MoSCoW al final del archivo /LTI-JDLM/UserStories-JDLM.md, siguiendo todas las instrucciones de tu prompt especializado.

Esta versión del backlog incluye:

Tabla detallada del Backlog con la asignación de categorías MoSCoW (Must Have, Should Have, Could Have).
Justificación de Prioridad que argumenta por qué el cumplimiento legal (RGPD) y la transparencia ética (XAI) definen el núcleo del MVP.
Análisis de Riesgos, destacando las dependencias tecnológicas externas y los desafíos de performance del análisis de video.
Sugerencias de Refinamiento (Grooming), donde propongo explícitamente dividir la historia de "Multiposting" para que quepa en un Sprint y crear un Spike técnico antes de abordar la evaluación multimodal en video.
```

> **Analisis personal**

No hice una analisis personal, pero le pedi al agente que lo hiciera y me dio la siguiente respuesta:

```text
Aquí tienes un análisis comparativo de la aplicación de ambas metodologías (RICE y MoSCoW) basado en los dos últimos prompts y su adaptación al contexto del ecosistema ATS/CRM que estamos diseñando:

Análisis Comparativo: RICE vs. MoSCoW en el diseño de un MVP
1. Metodología MoSCoW (Cualitativa y Categórica)
Comportamiento en el Prompt: Actuó como un filtro de protección excelente para la visión del producto. Al forzarnos a definir qué es "innegociable" (Must Have), el prompt puso en evidencia que sin cumplimiento legal (RGPD) y sin el diferenciador ético (XAI), el producto no puede lanzarse, independientemente del esfuerzo técnico.
Fortaleza principal: Es ideal para la fase actual (definición del MVP). Evita la parálisis por análisis y alinea rápidamente a los stakeholders sobre qué se queda dentro de la primera iteración y qué se aplaza (como el módulo de nóminas o el análisis avanzado de video).
Debilidad observada: Dentro de la misma categoría (ej. todos los Must Have), MoSCoW no ofrece una forma matemática de decidir qué historia tomar primero en el Sprint 1. Asume que todas tienen la misma urgencia absoluta.
2. Metodología RICE (Cuantitativa y Analítica)
Comportamiento en el Prompt: Actuó como un detector de riesgos e ineficiencias. Al tener que multiplicar factores y dividir por el Esfuerzo (Fibonacci), la metodología fue implacable con las historias "atractivas pero costosas". El mejor ejemplo fue la US-05 (Video), cuyo score RICE cayó al suelo (0.38) por la baja "Confianza" (50%) y alto esfuerzo (13), obligando al sistema a sugerir un Spike de investigación técnica.
Fortaleza principal: Obliga a justificar el valor con datos. Fue excelente para el refinamiento continuo táctico, empujándonos a hacer slicing (cortar en pedazos más pequeños) la US-04 de Multiposting para mejorar su RICE Score.
Debilidad observada: Requiere más tiempo de análisis por historia y puede dar una "falsa sensación de precisión matemática" si las estimaciones iniciales son meras suposiciones.
Conclusión Estratégica
Ambos prompts demostraron que las metodologías no son excluyentes, sino complementarias en distintas etapas del ciclo de vida del producto:

El Prompt de MoSCoW fue superior para establecer la Estrategia de Lanzamiento (Release Plan) y definir las barreras del MVP. Es el mejor enfoque cuando se inicia un proyecto desde cero.
El Prompt de RICE fue netamente superior para el Grooming Técnico y la Gestión de Incertidumbre. Una vez definido el alcance, RICE hizo un excelente trabajo matemático desnudando los cuellos de botella técnicos.
Recomendación de uso: Utilizar MoSCoW a nivel de Épicas para delinear Roadmaps trimestrales, y utilizar RICE a nivel de Historias de Usuario para planificar Sprints individuales y forzar la descomposición técnica.

```

### 3. Tickets de trabajo sobre las User Story  US-01: Análisis Semántico y Matching de Currículums (NLP)

> **Prompt:** 
```text
Actúa como Arquitecto de Software. Para la User Story US-01: Análisis Semántico y Matching de Currículums (NLP), definido en el archivo UserStories-JDLM.md realiza un desglose técnico para una Arquitectura Hexagonal en Node.js. Genera tickets separados para Dominio, Aplicación e Infraestructura, especificando los archivos que probablemente se verán afectados y el contrato de la API sugerido, usa .

# MARCO DE TRABAJO TÉCNICO
Debes aplicar estos principios en cada ticket:
1. Slicing Vertical: Cada ticket o conjunto de tickets debe entregar una funcionalidad que atraviese todas las capas técnicas.
2. Arquitectura Hexagonal: Separar claramente Dominio (lógica pura), Aplicación (casos de uso) e Infraestructura (adaptadores de DB, API, servicios externos).
3. Contratos Primero: Definir Inputs/Outputs (JSON, DTOs) antes de sugerir implementación.
4. Recalibración de Esfuerzo (2026): Estimar asumiendo el uso de agentes de IA (Cursor/Claude Code), priorizando la calidad del prompt y la validación sobre el "picado" manual de código.

# INSTRUCCIÓN DE ESTIMACIÓN
Estima el esfuerzo de cada ticket utilizando la Serie de Fibonacci (1, 2, 3, 5, 8, 13) y la unidad de Story Points (Puntos de Historia). 

Para asignar el puntaje, utiliza estos criterios:
- 1-2 pts: Tarea trivial, baja incertidumbre, poco código (ej. una interfaz simple).
- 3 pts: Tarea estándar, requiere lógica de negocio y tests.
- 5 pts: Tarea compleja, múltiples archivos afectados o integración con API externa.
- 8 pts+: Épica o tarea con alta incertidumbre técnica (sugerir división o Spike).

Justifica brevemente cada estimación basándote en la Complejidad, el Esfuerzo y la Incertidumbre.

# ANATOMÍA OBLIGATORIA DEL TICKET (Los 10 Componentes)
Para cada ticket generado, DEBES completar:
1. [Título]: [Capa/Módulo] + Acción técnica clara.
2. [Descripción]: El "Por qué" técnico y el impacto en el sistema.
3. [Criterios de Aceptación BDD]: Formato Given/When/Then (especificando estados técnicos).
4. [Prioridad]: Crítica, Alta, Media o Baja.
5. [Estimación]: Fibonacci (1, 2, 3, 5, 8). Justificar según Complejidad e Incertidumbre.
6. [Asignación Sugerida]: Perfil necesario (ej. Backend Dev, DevOps).
7. [Tags]: Categorización (ej. #Database, #API, #DomainLogic).
8. [Notas Técnicas]: Archivos específicos a crear/modificar y validaciones (ej. esquemas Zod).
9. [Referencias]: Vínculo a la User Story de origen y documentación necesaria.
10. [Definition of Done (DoD)]: Checklist técnico (Tests unitarios, Cobertura, Linting, Docs).

# PROCESO DE PENSAMIENTO (Chain of Thought)
Antes de generar los tickets, realiza un análisis breve:
- Analiza dependencias: ¿Qué tablas o contratos de API cambian?
- Identifica riesgos: ¿Hay incertidumbre tecnológica? (Si la hay, sugiere un Spike).
- Define el Contrato: Especifica el JSON de entrada y salida esperado.

Guarda el resultado en el archivo UserStories-JDLM.md

```

> **Respuesta del agente**

```text
He actuado como Arquitecto de Software y he realizado el desglose técnico completo de la User Story US-01 (Análisis Semántico y Matching de Currículums). El resultado ha sido añadido al archivo /LTI-JDLM/UserStories-JDLM.md justo antes del Backlog.

El desglose incluye:

Proceso de Pensamiento (Chain of Thought): Análisis de dependencias, identificación de latencia en la extracción de PDFs e I/O como riesgo principal, y la definición explícita del Contrato de API (Entrada y Salida en JSON).
Ticket 1 (Dominio): Creación del MatchCalculatorService. Estimado en 2 pts por ser lógica pura en TypeScript de bajísima incertidumbre.
Ticket 2 (Aplicación): Creación del ProcessCurriculumUseCase. Estimado en 3 pts como una tarea estándar de orquestación donde se definen los Puertos.
Ticket 3 (Infraestructura): Implementación de los adaptadores de Kafka, la API Externa de NLP y la Base de Datos. Estimado en 5 pts debido a la alta complejidad de coordinar múltiples dependencias externas asíncronas y el manejo de reintentos.
Cada ticket contiene la anatomía obligatoria de los 10 componentes, cumpliendo con los estándares de Slicing Vertical, Arquitectura Hexagonal y enfocados en el desarrollo impulsado por especificaciones y Criterios de Aceptación (BDD).

```



