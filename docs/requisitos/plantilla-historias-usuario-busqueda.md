# Historias de usuario de búsqueda

| Campo | Valor |
| --- | --- |
| Proyecto | Proyecto Simbiosis |
| Fecha | 29/10/2026 |
| Versión | 0.1 |
| Estado | Borrador |

## Fuentes comunes

- [Acta de UC-21 Buscar recetas](../captura/acta-acuerdos-uc-21-buscar-recetas.md), v1.1, Vigente.
- [Catálogo de requisitos](catalogo-requisitos.md), UR-08 y FR pertinentes.
- [Modelo de casos de uso](../modelos/modelo-casos-de-uso.md), UC-21.

## Épica de búsqueda

Como usuario registrado, quiero encontrar recetas combinando un texto de búsqueda, los ingredientes que quiero usar y los ingredientes que quiero evitar, para decidir qué cocinar sin revisar todo el catálogo.

**Estado:** descompuesta en US-01, US-02 y US-03. Conserva la necesidad conjunta.

## Justificación de la división

La épica se divide en tres historias porque cada una ofrece un resultado útil por sí sola y se puede entregar y probar de forma independiente sobre el mismo catálogo de recetas:

- **US-01** permite llegar a una receta concreta a partir de una palabra o frase, por ejemplo cuando la persona recuerda el nombre del plato o parte de él.
- **US-02** permite encontrar recetas que aprovechan los ingredientes que la persona tiene o quiere usar.
- **US-03** permite descartar las recetas que llevan ingredientes que la persona no quiere, mediante una exclusión que ella elige de forma expresa.

Las tres comparten la infraestructura de búsqueda y se pueden combinar en una misma consulta, pero ninguna necesita a las otras para ser útil.

## US-01

**Título:** Buscar recetas por palabra o frase

Como usuario registrado, quiero buscar recetas escribiendo una palabra o frase, para encontrar rápidamente un plato por su nombre o por lo que recuerdo de él.

**Fuentes:** UR-08; UC-21; FR-085 a FR-096 (concretar el FR principal en el catálogo); FR-119; acta de UC-21, v1.1.

### Criterios de aceptación

- **CA-01.** Dado que tengo una sesión iniciada y escribo una palabra o frase en la búsqueda, cuando la lanzo, entonces el sistema muestra las recetas que coinciden con el texto, con su vista previa.
- **CA-02.** Dado que escribo un texto que no coincide con ninguna receta, cuando lanzo la búsqueda, entonces el sistema informa de que no hay resultados y me permite modificar la búsqueda.
- **CA-03.** Dado que el sistema muestra resultados, cuando selecciono uno, entonces accedo al detalle de esa receta y puedo volver a la lista de resultados.

## US-02

**Título:** Buscar recetas por ingredientes incluidos

Como usuario registrado, quiero indicar los ingredientes que quiero que lleve una receta, para encontrar recetas que aprovechen lo que tengo o lo que me apetece cocinar.

**Fuentes:** UR-08; UC-21; FR-085 a FR-096 (concretar el FR principal en el catálogo); FR-119; acta de UC-21, v1.1.

### Criterios de aceptación

- **CA-01.** Dado que tengo una sesión iniciada e indico uno o varios ingredientes a incluir, cuando lanzo la búsqueda, entonces solo aparecen recetas que incluyen los ingredientes indicados.
- **CA-02.** Dado que indico un texto de búsqueda y ingredientes a incluir, cuando lanzo la búsqueda, entonces los resultados cumplen ambos criterios a la vez.
- **CA-03.** Dado que ninguna receta incluye los ingredientes indicados, cuando lanzo la búsqueda, entonces el sistema informa de que no hay resultados y me permite cambiar los ingredientes.

## US-03

**Título:** Excluir ingredientes de la búsqueda

Como usuario registrado, quiero excluir ingredientes de mi búsqueda, para no ver recetas que llevan ingredientes que no quiero consumir.

**Fuentes:** UR-08; UC-21; FR-085 a FR-096 (concretar el FR principal en el catálogo); FR-119; acta de UC-21, v1.1.

### Criterios de aceptación

- **CA-01.** Dado que tengo una sesión iniciada e indico uno o varios ingredientes a excluir, cuando lanzo la búsqueda, entonces ninguna receta de los resultados incluye esos ingredientes.
- **CA-02.** Dado que hay otros criterios activos (texto o ingredientes incluidos), cuando añado una exclusión, entonces los resultados cumplen todos los criterios a la vez.
- **CA-03.** Dado que no he indicado ninguna exclusión, cuando lanzo la búsqueda, entonces el sistema no excluye recetas por las alergias de mi perfil, porque la búsqueda no las aplica automáticamente.

## Revisión INVEST

La revisión abarca US-01, US-02 y US-03. «Aplicado» indica si se ha realizado la comprobación. «Cumple» indica si todas las historias cumplen el criterio. Si alguna no lo cumple, indicar «No» e identificar la historia y el motivo en la justificación. Si no se ha realizado la comprobación o faltan datos, indicar «Pendiente» en «Cumple».

| Criterio | Pregunta de revisión | Aplicado | Cumple | Justificación |
| --- | --- | --- | --- | --- |
| Independiente | ¿Puede implementarse cada historia y ofrecer un resultado útil sin implementar antes las otras historias del conjunto? Puede compartir infraestructura con ellas. | Sí | Sí | US-01, US-02 y US-03 se apoyan en el mismo catálogo y la misma infraestructura de búsqueda, pero cada una da un resultado útil sin las otras. US-03 funciona sola sobre el catálogo completo y su combinación con otros criterios se recoge como un criterio de aceptación, no como una dependencia. |
| Negociable | ¿Cada historia explica qué necesita la persona y deja margen para discutir los detalles de la solución, respetando los acuerdos confirmados? | Sí | Sí | Las historias describen la necesidad y no fijan la interfaz ni la técnica de búsqueda. Quedan abiertos, por ejemplo, el modo de introducir ingredientes o el tratamiento de variantes del mismo ingrediente. Se respeta el acuerdo de no aplicar automáticamente las alergias del perfil. |
| Valiosa | ¿La parte «para…» de cada historia explica el beneficio que obtiene la persona al usar esa capacidad? | Sí | Sí | Cada «para…» expresa un beneficio distinto: encontrar un plato por su nombre (US-01), aprovechar ingredientes disponibles (US-02) y evitar ingredientes no deseados (US-03). |
| Estimable | ¿Están claros el alcance y los datos necesarios para estimar el trabajo de cada historia? | Sí | Pendiente | El alcance es claro y los datos son los de las recetas. Falta confirmar en el acta cómo se comparan los ingredientes (variantes, plurales) y si varios ingredientes incluidos se combinan todos a la vez. Afecta a US-02 y US-03. |
| Pequeña | ¿Se centra cada historia en una única capacidad de alcance manejable? | Sí | Sí | Cada historia cubre una única capacidad de búsqueda. La ordenación, los filtros adicionales y el detalle de la receta quedan fuera de estas tres historias. |
| Comprobable | ¿Los criterios de aceptación de cada historia describen acciones y resultados observables que permiten distinguir un comportamiento correcto de uno incorrecto? | Sí | Sí | Cada criterio define una situación, una acción y un resultado que se puede comprobar con datos de prueba: recetas mostradas, ausencia de recetas con el ingrediente excluido o mensaje de «sin resultados». |

## Dudas pendientes

- Identificar en el catálogo los FR principales de US-01, US-02 y US-03 y el apartado pertinente del acta de UC-21 para completar las fuentes.
- Confirmar en el acta si varios ingredientes incluidos se combinan todos a la vez y cómo se comparan los ingredientes (variantes y plurales).
- La correspondencia entre las alergias del perfil y los ingredientes sigue abierta en el modelo. Por ahora US-03 solo cubre exclusiones que la persona indica en la búsqueda.
