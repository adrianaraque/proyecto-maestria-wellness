# proyecto-maestria-wellness
Plataforma Inteligente de Gestión Wellness basada en IA

Estos requisitos definen qué debe hacer el sistema. Los hemos dividido por módulos lógicos para facilitar la futura creación de microservicios.
Módulo 1: Gestión de Usuarios y Perfiles
•	RF-01: El sistema debe permitir a los usuarios registrarse e iniciar sesión utilizando correo electrónico/contraseña o autenticación de terceros (ej. Google OAuth).
•	RF-02: El sistema debe recopilar y almacenar los datos antropométricos iniciales del usuario (peso corporal, altura, edad, género).
•	RF-03: El sistema debe permitir al usuario definir sus objetivos principales (ej. hipertrofia, ganancia de fuerza, pérdida de grasa, mantenimiento).
Módulo 2: Gestión de Rutinas y Entrenamientos (Core Fitness)
•	RF-04: El sistema debe permitir al usuario registrar los detalles de cada sesión de entrenamiento, incluyendo: tipo de ejercicio, series, repeticiones ejecutadas y peso levantado.
•	RF-05: El sistema debe contar con una base de datos estandarizada de ejercicios de fuerza y musculación (clasificados por grupo muscular y equipamiento).
•	RF-06: El sistema debe calcular métricas de sesión automáticamente, como el volumen de carga total (Series x Repeticiones x Peso).
Módulo 3: Inteligencia Artificial (Wellness Coach Agent)
•	RF-07: El agente de IA debe generar un plan de entrenamiento semanal estructurado basado en el objetivo del usuario, su nivel de experiencia y los días disponibles para entrenar.
•	RF-08: El agente de IA debe analizar el historial de cargas del usuario y sugerir ajustes para garantizar la sobrecarga progresiva (ej. "Te sugiero aumentar 2kg en Sentadilla esta semana").
•	RF-09: El sistema debe incluir una interfaz de "Chat Asistente Wellness" donde el usuario pueda consultar dudas sobre ejecución de ejercicios o pedir adaptaciones en tiempo real (ej. "La máquina de poleas está ocupada, ¿qué otro ejercicio puedo hacer?").
•	RF-10: El agente debe detectar patrones de estancamiento o disminución del rendimiento y enviar alertas proactivas o mensajes motivacionales para prevenir el abandono.
Módulo 4: Analítica y Progreso
•	RF-11: El sistema debe mostrar un panel interactivo (Dashboard) con la proyección de progreso físico y de cargas en el tiempo estimado.
________________________________________
 Requisitos No Funcionales (RNF) - Evaluación ISO 25010
Estos requisitos definen cómo el sistema debe comportarse, alineados directamente con el estándar de calidad ISO 25010 solicitado por la profesora.
•	RNF-01: Adecuación Funcional: Las sugerencias de rutinas generadas por la IA deben basarse en principios comprobados de hipertrofia y fuerza, asegurando que los ejercicios recomendados sean biomecánicamente coherentes.
•	RNF-02: Eficiencia de Desempeño:
o	El tiempo de respuesta de la API Gateway para consultas CRUD básicas (ej. guardar un peso) no debe superar los 500 ms.
o	El tiempo de respuesta del Agente IA para generar una nueva rutina completa no debe superar los 5 segundos.
•	RNF-03: Compatibilidad: La arquitectura debe ser MCP-ready, permitiendo que el Agente IA consulte las bases de datos (Firestore/BigQuery) mediante protocolos estandarizados sin interferir con otros microservicios.
•	RNF-04: Usabilidad: La interfaz (PWA o Web Responsive) debe permitir el registro de pesos y repeticiones con un máximo de 3 toques/clics por serie, ya que el usuario estará interactuando en el gimnasio.
•	RNF-05: Fiabilidad (Cloud-Native): El sistema debe garantizar una disponibilidad del 99.9% mediante el despliegue en contenedores (ej. Docker en GCP/AWS) y balanceo de carga.
•	RNF-06: Seguridad:
o	Todas las contraseñas deben estar hasheadas (ej. bcrypt).
o	La comunicación entre el cliente y el servidor, y entre microservicios, debe estar cifrada (HTTPS/TLS).
•	RNF-07: Mantenibilidad: El código debe estar versionado en GitHub, utilizando convenciones de Clean Code y separado estrictamente en microservicios independientes (Auth, Workout-Core, IA-Agent).
•	RNF-08: Portabilidad: El sistema debe poder ejecutarse y desplegarse en cualquier entorno compatible con contenedores Docker, sin depender exclusivamente de una sola nube.

 Épica 1: Onboarding y Configuración de Perfil
HU-01: Registro de perfil y objetivos iniciales
•	Historia: Como usuario nuevo, quiero registrar mis datos físicos (peso, altura, edad) y mi objetivo principal (ej. ganar músculo, perder grasa) para que el sistema pueda generar recomendaciones personalizadas.
•	Criterios de Aceptación:
o	El sistema debe validar que los campos de datos físicos sean numéricos y estén dentro de rangos lógicos.
o	El usuario debe poder seleccionar su objetivo de una lista predefinida.
o	Los datos deben guardarse correctamente en la base de datos (ej. Firestore) vinculados al ID del usuario.

 Épica 2: Registro del Entrenamiento (Core Wellness)
HU-02: Registro de series en tiempo real
•	Historia: Como usuario en el gimnasio, quiero anotar rápidamente el peso y las repeticiones de cada serie que realizo para llevar un control exacto de mi sobrecarga progresiva sin perder tiempo.
•	Criterios de Aceptación:
o	La interfaz debe permitir ingresar los datos con un teclado numérico optimizado para móviles.
o	El sistema debe auto-completar los campos con el peso y repeticiones de la sesión anterior para ese mismo ejercicio a modo de sugerencia.
o	Debe existir un botón visible para marcar la serie como "Completada".
HU-03: Visualización del historial de un ejercicio
•	Historia: Como usuario, quiero ver el gráfico o la lista de mis levantamientos anteriores en un ejercicio específico (ej. Press de Banca) para saber si estoy mejorando mi fuerza.
•	Criterios de Aceptación:
o	Al seleccionar un ejercicio, se debe mostrar el peso máximo levantado (1RM estimado) y el historial de las últimas 4 semanas.

 Épica 3: Interacción con el Wellness Coach Agent (IA)
HU-04: Generación de rutina semanal automatizada
•	Historia: Como usuario, quiero solicitar al Agente IA que me arme una rutina para los próximos 4 días basada en mis objetivos y mi nivel, para no tener que planificarla manualmente.
•	Criterios de Aceptación:
o	El Agente IA debe procesar el historial del usuario y devolver un plan estructurado (días, ejercicios, series y repeticiones objetivo).
o	El plan generado debe guardarse en la base de datos y reflejarse inmediatamente en el calendario del usuario.
HU-05: Asistencia en tiempo real (Chatbot Wellness)
•	Historia: Como usuario en medio de una rutina, quiero pedirle al chat de IA una alternativa a un ejercicio (ej. "la máquina de sentadillas está ocupada") para no interrumpir mi flujo de entrenamiento.
•	Criterios de Aceptación:
o	El chat debe integrarse en la misma pantalla de la rutina activa.
o	El Agente IA debe recomendar un ejercicio que trabaje el mismo grupo muscular basándose en la base de datos de ejercicios disponible.
HU-06: Detección proactiva de estancamiento (Push AI)
•	Historia: Como usuario, quiero que la IA me avise si llevo varias semanas levantando el mismo peso o saltándome entrenamientos, y me sugiera qué cambiar para recuperar el ritmo y no abandonar.
•	Criterios de Aceptación:
o	El sistema (Analytics Agent) debe evaluar semanalmente el volumen de carga y la frecuencia de asistencia.
o	Si detecta estancamiento o riesgo de abandono, debe generar un mensaje motivacional o sugerir una semana de descarga (deload) a través de una notificación.

 Épica 4: Administración de la Plataforma
HU-07: Dashboard de métricas globales
•	Historia: Como administrador del sistema, quiero visualizar un panel de control con métricas generales de los usuarios (usuarios activos, rutinas más generadas, tasa de abandono) para evaluar el rendimiento de la plataforma.
•	Criterios de Aceptación:
o	El dashboard debe consumir datos agregados (preferiblemente desde BigQuery).
o	Debe mostrar gráficos de retención mensual y uso de la IA.

 Catálogo de los 10 Casos de Uso
Actor Principal: Usuario (Atleta)
1.	CU-01: Registrar Cuenta y Perfil Físico: El usuario ingresa sus credenciales, datos corporales (peso, altura) y meta de fitness (hipertrofia, fuerza) para iniciar el sistema.
2.	CU-02: Registrar Entrenamiento en Tiempo Real: El usuario introduce el peso y las repeticiones ejecutadas en cada serie de un ejercicio mientras está en el gimnasio.
3.	CU-03: Visualizar Historial y Progreso: El usuario revisa sus gráficos de rendimiento mensual y 1RM (Repetición Máxima) estimados.
4.	CU-04: Solicitar Rutina Personalizada: El usuario pide al sistema la generación de su próxima rutina semanal.
5.	CU-05: Consultar Chatbot IA por Alternativas: El usuario pregunta al chatbot (en tiempo real) por qué ejercicio sustituir uno que no puede hacer (ej. máquina ocupada).


Actor Principal: Agentes de Inteligencia Artificial 
6. CU-06: Generar Plan de Entrenamiento (Wellness Coach Agent): La IA procesa la solicitud del usuario, consulta BigQuery/Firestore y construye una rutina aplicando principios de sobrecarga progresiva. (Extiende de CU-04) 7. CU-07: Evaluar Estancamiento y Progreso (Analytics Agent): El agente analiza en segundo plano el historial de cargas para calcular si el usuario está mejorando o se ha estancado. 
8. CU-08: Detectar Inactividad y Enviar Motivación (Motivation Agent): El agente detecta (mediante eventos temporales) que el usuario no ha registrado rutinas en 4 días y le envía un mensaje personalizado para evitar el abandono.
Actor Principal: Administrador 
9. CU-09: Gestionar Catálogo Maestro de Ejercicios: El administrador añade, edita o elimina ejercicios de la base de datos central (agregando músculos implicados y videos). 
10. CU-10: Monitorear Métricas Globales: El administrador visualiza un dashboard con el número total de usuarios activos, rutinas generadas por la IA y tasa de retención.

flowchart LR
    %% Definición de Actores
    U([👤 Usuario Atleta])
    Admin([🛠️ Administrador])
    IA_WC([🤖 Wellness Coach Agent])
    IA_AN([📊 Analytics Agent])
    IA_MO([🔥 Motivation Agent])

    %% Límite del Sistema
    subgraph Plataforma Inteligente Wellness
        direction TB
        CU1((CU-01: Registrar \nCuenta y Perfil))
        CU2((CU-02: Registrar \nEntrenamiento))
        CU3((CU-03: Visualizar \nProgreso))
        CU4((CU-04: Solicitar \nRutina IA))
        CU5((CU-05: Consultar \nChatbot Alternativas))
        
        CU6((CU-06: Generar Plan \nde Entrenamiento))
        CU7((CU-07: Evaluar Progreso \ny Estancamiento))
        CU8((CU-08: Detectar Abandono \ny Motivar))
        
        CU9((CU-09: Gestionar Catálogo \nde Ejercicios))
        CU10((CU-10: Monitorear \nMétricas Globales))
    end

    %% Relaciones Usuario
    U --> CU1
    U --> CU2
    U --> CU3
    U --> CU4
    U --> CU5

    %% Relaciones y dependencias IA (Includes / Extends lógicos)
    CU4 -. "<<include>>" .-> CU6
    IA_WC --> CU6
    IA_WC --> CU5
    
    CU2 -. "<<trigger>>" .-> CU7
    IA_AN --> CU7
    
    CU7 -. "<<informa a>>" .-> IA_MO
    IA_MO --> CU8

    %% Relaciones Administrador
    Admin --> CU9
    Admin --> CU10

    %% Estilos (Opcional para que se vea elegante en GitHub)
    classDef actorStyle fill:#f9f9f9,stroke:#333,stroke-width:2px;
    classDef usecaseStyle fill:#e1f5fe,stroke:#0288d1,stroke-width:2px;
    classDef iaStyle fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#000;
    
    class U,Admin actorStyle;
    class CU1,CU2,CU3,CU4,CU5,CU9,CU10 usecaseStyle;
    class CU6,CU7,CU8 iaStyle;
    class IA_WC,IA_AN,IA_MO actorStyle;
