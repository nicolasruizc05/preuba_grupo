# MD-003 - Arquitectura del Motor Pedagógico

## 1. Objetivo

Definir la arquitectura del Motor Pedagógico de MentorOS, describiendo los componentes que lo conforman, sus responsabilidades, el flujo de información entre ellos y la forma en que colaboran para gestionar el proceso de aprendizaje del usuario.

## 2. Alcance

El presente documento describe la arquitectura conceptual del Motor Pedagógico de MentorOS. Su propósito es definir los componentes que intervienen en el proceso de aprendizaje, sus responsabilidades, la comunicación entre ellos y el flujo de decisiones que permite construir una experiencia de aprendizaje personalizada. Este documento no describe detalles de implementación, tecnologías específicas ni modelos de inteligencia artificial.

## 3. Principios de Diseño

Los principios de diseño definen las bases arquitectónicas y pedagógicas que orientan la construcción del Motor Pedagógico de MentorOS, estableciendo las reglas que deben cumplir sus componentes para garantizar un sistema organizado, adaptable y coherente con la filosofía de aprendizaje planteada.

### 3.1 Separación de responsabilidades

Cada componente del Motor Pedagógico debe tener una responsabilidad claramente definida, permitiendo mantener un mayor control sobre las funciones que desempeña dentro del sistema.
Esta separación facilita la evolución del proyecto, reduce la dependencia entre componentes y permite realizar modificaciones o mejoras sin afectar el funcionamiento general del motor.

### 3.2 Aprendizaje basado en competencias

El conocimiento dentro de MentorOS estará organizado mediante competencias, donde cada una representa una capacidad que el usuario debe desarrollar y demostrar.
Cada competencia estará relacionada con objetivos de aprendizaje, criterios de dominio, evidencias de aprendizaje y prerrequisitos necesarios para garantizar que pueda ser adquirida correctamente.
De esta manera, el sistema no seguirá únicamente una estructura lineal de temas, sino una red de conocimientos relacionados que permitirá construir rutas personalizadas de aprendizaje.

### 3.3 Adaptación continua

El Motor Pedagógico tendrá la capacidad de adaptarse al proceso de aprendizaje de cada usuario, considerando su ritmo, conocimientos previos y evidencias obtenidas durante las interacciones.
La adaptación no estará basada únicamente en respuestas correctas o incorrectas, sino en la capacidad del usuario para demostrar comprensión, aplicar conocimientos, resolver problemas y relacionar conceptos.
Esto permitirá que MentorOS evalúe el aprendizaje real del usuario y no únicamente su capacidad para responder una prueba.

### 3.4 Independencia de la IA

La inteligencia artificial no será el centro del sistema ni será responsable de definir la lógica pedagógica del aprendizaje.
Su función será actuar como un acompañante inteligente encargado de interactuar con el usuario, explicar conceptos, generar ejemplos, realizar preguntas y adaptar la comunicación según las necesidades del usuario.
Las decisiones relacionadas con qué enseñar, cuándo avanzar, qué reforzar y cómo evaluar el dominio de una competencia serán responsabilidad del Motor Pedagógico y del Modelo de Competencias.

## 4 Arquitectura General 

                         Usuario
                            |
                            ▼
                    ┌─────────────┐
                    │  Mentor IA  │
                    │ Interacción │
                    └─────────────┘
                            |
                            ▼
                ┌────────────────────┐
                │ Motor Pedagógico   │
                │ Núcleo de decisión │
                └────────────────────┘
                            |
        ┌───────────┬───────┼───────────┬───────────┐
        ▼           ▼       ▼           ▼           ▼
 Gestor de     Gestor de  Motor de   Motor de   Motor de
Competencias   Rutas     Diagnóstico Evidencias Reforzamiento

                            |
                            ▼
                ┌─────────────────────┐
                │ Perfil usuario   │
                └─────────────────────┘

                            |
                            ▼
                ┌─────────────────────┐
                │ Motor de Progreso   │
                └─────────────────────┘

## 5. Componentes del Motor Pedagogico 

### 5.1 Mentor IA (Interacción)

- ¿Cuál es su propósito?
El propósito de este componente es servir como interfaz conversacional entre el usuario y el Motor Pedagógico, permitiendo una comunicación natural durante el proceso de aprendizaje.

- ¿Qué recibe?
Recibe las interacciones del usuario, como solicitudes de aprendizaje, preguntas, respuestas y solicitudes de explicación.
Ejemplo:
"Quiero aprender React"

- ¿Qué entrega?
Entrega al Motor Pedagógico la intención del usuario y posteriormente comunica las acciones definidas por este, adaptando la explicación según las necesidades del usuario.

### 5.2 Gestor de Competencias

- ¿Cuál es su propósito?
Administrar el conocimiento estructurado de MentorOS mediante competencias de aprendizaje, incluyendo sus objetivos, prerrequisitos, relaciones y criterios de dominio.

- ¿Qué recibe?
Solicitudes del Motor Pedagógico relacionadas con una competencia específica.
Ejemplo:
"Obtener información de la competencia React"

- ¿Qué entrega?
Entrega la información asociada a la competencia:
- descripción;
- objetivos;
- prerrequisitos;
- criterios de dominio;
- evidencias esperadas.

### 5.3 Gestor de Rutas de Aprendizaje

- ¿Cuál es su propósito?
Construir y administrar la secuencia de aprendizaje que debe seguir el usuario para alcanzar una competencia determinada.

- ¿Qué recibe?
Recibe una competencia objetivo y la información del perfil del usuario.

- ¿Qué entrega?
Entrega una ruta personalizada de aprendizaje indicando:
- competencias previas requeridas;
- orden recomendado;
- competencias pendientes;
- siguiente objetivo de aprendizaje.

### 5.4 Motor de Diagnóstico

- ¿Cuál es su propósito?
Evaluar el nivel de comprensión y dominio del usuario frente a una competencia, identificando fortalezas, dificultades y oportunidades de mejora.

- ¿Qué recibe?
Recibe las respuestas del usuario, ejercicios realizados, explicaciones proporcionadas y evidencias generadas durante el proceso de aprendizaje.

- ¿Qué entrega?
Entrega un análisis del nivel de dominio de la competencia, identificando los conocimientos adquiridos, los aspectos que requieren refuerzo y recomendaciones para continuar con la ruta de aprendizaje.

### 5.5 Motor de Evidencias

- ¿Cuál es su propósito?
Registrar, organizar y analizar las evidencias generadas durante el proceso de aprendizaje para demostrar el desarrollo de una competencia.

- ¿Qué recibe?
Recibe resultados del diagnóstico, ejercicios realizados, explicaciones del usuario, soluciones prácticas y actividades completadas.

- ¿Qué entrega?
Entrega información sobre las evidencias acumuladas del usuario, permitiendo determinar el nivel de dominio alcanzado en una competencia.

### 5.6 Motor de Reforzamiento

- ¿Cuál es su propósito?
Identificar dificultades en el aprendizaje y generar estrategias para fortalecer las competencias que presentan debilidades.

- ¿Qué recibe?
Recibe información del diagnóstico, evidencias del usuario y competencias con dominio insuficiente.

- ¿Qué entrega?
Entrega recomendaciones de refuerzo, actividades adicionales, explicaciones alternativas y ejercicios personalizados.

## 6. Flujo del Motor Pedagógico

El flujo del Motor Pedagógico describe el proceso mediante el cual MentorOS interpreta la intención del usuario, determina la ruta adecuada de aprendizaje, acompaña el desarrollo de competencias y analiza las evidencias obtenidas durante el proceso.

### 6.1 Solicitud inicial del usuario
El usuario realiza una solicitud de aprendizaje mediante el Mentor IA.
Ejemplo:
"Quiero aprender React"
---

### 6.2 Identificación de la competencia
El Mentor IA recibe la solicitud y comunica la intención del usuario al Motor Pedagógico.
El Motor Pedagógico consulta el Gestor de Competencias para identificar la competencia asociada al objetivo del usuario.
Ejemplo:
Usuario:
"Quiero aprender React"
Resultado:
Competencia objetivo:
Desarrollo de interfaces con React.
---

### 6.3 Análisis de prerrequisitos
El Motor Pedagógico consulta las competencias necesarias para alcanzar la competencia seleccionada.
Ejemplo:
React requiere:
- JavaScript básico.
- Funciones.
- Objetos.
- Manejo del DOM.
---

### 6.4 Construcción de la ruta de aprendizaje
El Gestor de Rutas de Aprendizaje analiza la información obtenida y construye una ruta personalizada teniendo en cuenta:
- Competencias previas.
- Perfil del estudiante.
- Evidencias existentes.
- Nivel de dominio actual.
---

### 6.5 Asignación de misiones de aprendizaje
El Motor Pedagógico genera las misiones correspondientes para desarrollar la competencia.
Cada misión puede contener:
- Explicaciones.
- Ejercicios prácticos.
- Retos.
- Actividades de reflexión.
- Evidencias esperadas.
El Mentor IA comunica las misiones al usuario.
---

### 6.6 Desarrollo y recopilación de evidencias
El usuario desarrolla las actividades propuestas y genera evidencias de aprendizaje mediante:
- Respuestas.
- Soluciones prácticas.
- Explicaciones propias.
- Resolución de problemas.
---

### 6.7 Análisis del aprendizaje
El Motor Pedagógico analiza las evidencias obtenidas mediante el Motor de Diagnóstico.
El sistema determina:
- Nivel de dominio alcanzado.
- Fortalezas.
- Aspectos por reforzar.
---

### 6.8 Reforzamiento o avance
Si se identifican dificultades, el Motor de Reforzamiento genera actividades adicionales para fortalecer los conocimientos necesarios.
Si el usuario demuestra dominio suficiente, el sistema permite continuar hacia nuevas competencias dentro de la ruta de aprendizaje.

Usuario
  |
Mentor IA
  |
Motor Pedagógico
  |
  ├── Gestor de Competencias
  |
  ├── Gestor de Rutas
  |
  ├── Motor Diagnóstico
  |
  ├── Motor Evidencias
  |
  └── Motor Reforzamiento
          |
     Nueva misión

# 7. Responsabilidades de cada componente

Cada componente del Motor Pedagógico posee una responsabilidad específica dentro del proceso de aprendizaje. Esta separación permite mantener una arquitectura organizada, escalable y alineada con la filosofía de MentorOS.

## 7.1 Mentor IA
### Responsabilidad principal
Actuar como la interfaz conversacional entre el usuario y el sistema, facilitando la comunicación durante el proceso de aprendizaje.

### Responsabilidades:
- Interpretar las solicitudes del usuario.
- Comunicar la intención del usuario al Motor Pedagógico.
- Explicar conceptos utilizando un lenguaje adaptado al estudiante.
- Generar ejemplos y analogías para facilitar la comprensión.
- Formular preguntas siguiendo las estrategias definidas por el Motor Pedagógico.
- Comunicar avances, recomendaciones y retroalimentación al usuario.

### No es responsabilidad del Mentor IA:
- Definir qué competencia debe aprender el usuario.
- Decidir cuándo el usuario puede avanzar.
- Evaluar por sí solo el dominio de una competencia.
---

## 7.2 Gestor de Competencias

### Responsabilidad principal
Administrar el conocimiento estructurado que utiliza MentorOS para representar las habilidades y conocimientos que el estudiante debe desarrollar.

### Responsabilidades:
- Almacenar las competencias disponibles.
- Definir relaciones entre competencias.
- Administrar prerrequisitos.
- Mantener objetivos de aprendizaje.
- Gestionar criterios de dominio.
- Proporcionar información requerida por el Motor Pedagógico.

### No es responsabilidad del Gestor de Competencias:
- Evaluar al estudiante.
- Crear rutas personalizadas.
- Decidir el siguiente paso del aprendizaje.
---

## 7.3 Gestor de Rutas de Aprendizaje

### Responsabilidad principal
Construir y administrar la ruta personalizada que seguirá el estudiante para alcanzar una competencia.

### Responsabilidades:
- Analizar las competencias requeridas.
- Identificar prerrequisitos necesarios.
- Organizar el orden recomendado de aprendizaje.
- Adaptar la ruta según el perfil del estudiante.
- Determinar las próximas misiones de aprendizaje.

### No es responsabilidad del Gestor de Rutas:
- Explicar los contenidos.
- Evaluar evidencias.
- Interactuar directamente con el usuario.
---

## 7.4 Motor de Diagnóstico

### Responsabilidad principal
Analizar el nivel de dominio del estudiante frente a una competencia.

### Responsabilidades:
- Analizar respuestas del usuario.
- Evaluar ejercicios realizados.
- Identificar fortalezas y dificultades.
- Determinar niveles de dominio.
- Generar recomendaciones de aprendizaje.

### No es responsabilidad del Motor de Diagnóstico:
- Bloquear el avance del estudiante.
- Crear contenido educativo.
- Reemplazar al Mentor IA.
---

## 7.5 Motor de Evidencias

### Responsabilidad principal
Registrar y organizar las evidencias generadas durante el proceso de aprendizaje.

### Responsabilidades:
- Almacenar evidencias del estudiante.
- Asociar evidencias con competencias.
- Mantener historial de aprendizaje.
- Proporcionar información para el diagnóstico.
- Permitir seguimiento del progreso.

### No es responsabilidad del Motor de Evidencias:
- Evaluar directamente al estudiante.
- Crear rutas de aprendizaje.
- Generar explicaciones.
---

## 7.6 Motor de Reforzamiento

### Responsabilidad principal
Fortalecer las competencias donde el estudiante presenta dificultades.

### Responsabilidades:
- Analizar debilidades identificadas.
- Generar estrategias de refuerzo.
- Recomendar actividades adicionales.
- Proponer ejercicios complementarios.
- Integrar conocimientos previos cuando sean necesarios.

### No es responsabilidad del Motor de Reforzamiento:
- Reemplazar la ruta principal.
- Evaluar nuevamente sin criterios definidos.
- Decidir la arquitectura del aprendizaje.
---

## 7.7 Gestor del Perfil del Estudiante

### Responsabilidad principal
Administrar la información relacionada con el proceso individual de aprendizaje del usuario.

### Responsabilidades:
- Registrar conocimientos adquiridos.
- Mantener historial de aprendizaje.
- Gestionar preferencias del usuario.
- Almacenar niveles de dominio.
- Proporcionar contexto personalizado al Motor Pedagógico.
---

## 7.8 Motor de Progreso

### Responsabilidad principal
Representar la evolución del estudiante dentro de su proceso de aprendizaje.

### Responsabilidades:
- Calcular avance dentro de una ruta.
- Mostrar competencias desarrolladas.
- Identificar competencias pendientes.
- Generar indicadores de progreso.
- Facilitar seguimiento del aprendizaje.

# 8. Interacción entre componentes
La interacción entre los componentes del Motor Pedagógico permite que MentorOS gestione el proceso de aprendizaje de forma personalizada, utilizando la información del estudiante, las competencias disponibles y las evidencias generadas durante el proceso.
Cada componente participa dentro de un flujo coordinado donde el Motor Pedagógico actúa como núcleo de decisión, integrando la información necesaria para definir la ruta de aprendizaje y las acciones que debe realizar el sistema.
---

## 8.1 Flujo de interacción inicial
Cuando un usuario expresa una intención de aprendizaje, el flujo inicia mediante el Mentor IA.
Ejemplo:
Usuario:
"Quiero aprender React"
El proceso es el siguiente:
1. El Mentor IA recibe la solicitud del usuario y transmite la intención al Motor Pedagógico.
2. El Motor Pedagógico consulta el Gestor de Competencias para identificar la competencia asociada al objetivo del usuario.
3. El Gestor de Competencias proporciona la información relacionada:
- Descripción de la competencia.
- Objetivos de aprendizaje.
- Prerrequisitos.
- Criterios de dominio.
- Competencias relacionadas.
4. El Motor Pedagógico solicita al Gestor del Perfil del Estudiante la información actual del usuario:
- Competencias adquiridas.
- Nivel de dominio.
- Historial de aprendizaje.
- Evidencias anteriores.
5. El Gestor de Rutas de Aprendizaje analiza la información obtenida y construye una ruta personalizada.
6. El Mentor IA comunica al usuario la ruta y las primeras misiones asignadas.
---

## 8.2 Flujo durante el aprendizaje
Durante el desarrollo de una misión, el estudiante genera información que será utilizada por los componentes del motor.
El flujo es:
1. El usuario desarrolla actividades propuestas.
2. Las respuestas, ejercicios y resultados obtenidos son almacenados mediante el Motor de Evidencias.
3. El Motor de Diagnóstico analiza las evidencias generadas para determinar el nivel de dominio alcanzado.
4. El Motor Pedagógico recibe los resultados del diagnóstico y decide la siguiente acción:
- Continuar con la ruta establecida.
- Recomendar refuerzo.
- Ajustar la ruta de aprendizaje.
5. El Mentor IA comunica la decisión al estudiante utilizando una explicación adaptada.
---

## 8.3 Interacción durante el reforzamiento
Cuando el sistema identifica dificultades en una competencia:
1. El Motor de Diagnóstico informa las áreas donde existe dificultad.
2. El Motor de Reforzamiento analiza las necesidades del estudiante.
3. Se generan actividades adicionales, explicaciones alternativas o ejercicios prácticos.
4. Las nuevas evidencias obtenidas son registradas nuevamente para evaluar la evolución del estudiante.
---

## 8.4 Principio de comunicación entre componentes
La comunicación entre componentes seguirá el principio de separación de responsabilidades:
- El Modelo de Competencias proporciona el conocimiento.
- El Perfil del Estudiante proporciona el contexto individual.
- El Motor de Evidencias proporciona información del progreso real.
- El Motor Pedagógico toma las decisiones de aprendizaje.
- El Mentor IA comunica y acompaña al usuario.

De esta forma, MentorOS mantiene una arquitectura donde la inteligencia artificial funciona como un facilitador del aprendizaje y no como el único responsable de la toma de decisiones.

# 9. Resultado esperado
La arquitectura definida para el Motor Pedagógico de MentorOS permitirá construir un sistema de aprendizaje personalizado, capaz de analizar las necesidades del estudiante, adaptar las rutas de aprendizaje y acompañar su desarrollo de competencias.
Mediante la integración de sus componentes, el sistema podrá:

- Identificar los objetivos de aprendizaje del usuario.
- Relacionar los temas solicitados con competencias específicas.
- Analizar los conocimientos previos del estudiante.
- Construir rutas de aprendizaje adaptadas a sus necesidades.
- Asignar misiones orientadas al desarrollo de competencias.
- Evaluar el progreso mediante evidencias de aprendizaje.
- Detectar dificultades y generar estrategias de reforzamiento.
- Permitir un avance progresivo sin generar bloqueos estrictos.
- Utilizar la inteligencia artificial como un acompañante educativo que facilita la comprensión y comunicación del conocimiento.

El resultado esperado es un sistema donde el aprendizaje no esté basado únicamente en completar contenidos o aprobar evaluaciones, sino en desarrollar, demostrar y fortalecer competencias de manera progresiva.
De esta forma, MentorOS busca convertirse en un entorno de aprendizaje adaptativo donde cada estudiante pueda avanzar según su propio proceso, manteniendo una guía estructurada proporcionada por el Motor Pedagógico.