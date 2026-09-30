# Bitácora de técnicas avanzadas

Laboratorio 07: Técnicas Avanzadas de Prompting.
Herramienta de IA usada: ChatGPT mediante chats temporales.

## Ejercicio 2: Zero-shot, one-shot y few-shot

| Tipo      | Aciertos (de 5) | Formato de la respuesta                                                   | Todas con el mismo formato (Sí/No) |
| --------- | --------------- | ------------------------------------------------------------------------- | ---------------------------------- |
| Zero-shot | 5               | Tabla con comentario y clasificación; incluye un resumen.                 | Sí                                 |
| One-shot  | 5               | Lista numerada, sin comillas y con etiquetas en negrita.                  | Sí                                 |
| Few-shot  | 5               | Comentarios entre comillas, seguidos de -> y la etiqueta, sin numeración. | Sí                                 |

Las tres respuestas clasificaron correctamente los comentarios y mantuvieron un formato uniforme dentro de cada respuesta. Sin embargo, few-shot reprodujo el formato de los ejemplos con mayor fidelidad.

## Ejercicio 3: Chain of Thought

| Pedido      | Respuesta de la IA                                                        | Muestra los pasos (Sí/No) | Correcta (Sí/No) |
| ----------- | ------------------------------------------------------------------------- | ------------------------- | ---------------- |
| Directo     | 318.60                                                                    | No                        | Sí               |
| Paso a paso | S/ 318.60, con los cálculos del descuento, IGV y total por tres unidades. | Sí                        | Sí               |

Mostrar los cálculos permite verificar que primero se aplicó el descuento y después el IGV.
Aunque la respuesta directa fue correcta, los pasos permiten identificar dónde habría un error.

## Ejercicio 4: Role prompting

| Versión        | Vocabulario (sencillo/técnico)                                                     | Usa ejemplos o código                                                      | A quién le sirve más                                                             |
| -------------- | ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| A. Sin rol     | Sencillo, con una mención al espacio de memoria.                                   | Comparación con una caja y ejemplos breves en Python.                      | Personas que necesitan una explicación general y breve.                          |
| B. Rol docente | Sencillo y detallado; explica nombre, valor y asignación.                          | Comparación con una caja y ejemplos en Python sobre edad, nombre y puntos. | Estudiantes que nunca han programado.                                            |
| C. Rol senior  | Combina lenguaje sencillo con términos como tipo de dato, identificador y dominio. | Código Java y ejemplos sobre impuestos y nombres descriptivos.             | Personas con conocimientos básicos de Java que buscan escribir código más claro. |

El rol docente produjo una explicación más guiada para principiantes. El rol senior orientó los ejemplos hacia Java y la calidad del código, aunque mantuvo un lenguaje accesible.

## Ejercicio 5: Descomposición

- Paso 1: La IA presentó cinco requisitos principales para un sistema de inventario de una tienda pequeña en Java.
- Paso 2: Diseñó seis clases con sus atributos y tipos de datos, además del enum TipoMovimiento.
- Paso 3: Generó la clase Producto con atributos privados, constructor y métodos get y set. Utilizó BigDecimal para el precio y una referencia a Categoria.
- Paso 4: Propuso validar los datos, evitar cambios en los identificadores y agregar métodos para controlar el stock.

Comparación: El pedido por pasos permitió revisar por separado los requisitos, el diseño, el código y las mejoras, manteniendo el contexto entre las respuestas.

## Ejercicio 6: Prompt estructurado y autocrítica

El prompt básico generó 25 casos generales. El prompt estructurado produjo los 6 casos solicitados, enfocados en las credenciales y el bloqueo después de tres intentos fallidos. La autocrítica agregó seis casos sobre campos vacíos, correo inválido y espacios.

| Qué revisar                                      | Cumple (Sí/No) |
| ------------------------------------------------ | -------------- |
| ¿Tiene las 4 columnas pedidas?                   | Sí             |
| ¿Incluye el bloqueo después de 3 intentos?       | Sí             |
| ¿Incluye casos con campos vacíos?                | Sí             |
| ¿Indica qué casos agregó en la autocrítica?      | Sí             |
| ¿Hay algún caso repetido o que no tenga sentido? | No             |

Observación: Los datos de CP-11 y CP-12 no muestran claramente los espacios que se desean probar. Además, el reinicio del contador en CP-06 y el tratamiento de errores de validación requieren confirmar las reglas del sistema.

### Prompt estructurado

```text
<rol>Actua como analista de pruebas de software.</rol>
<contexto>Login web con correo y contrasena. La cuenta se bloquea
despues de 3 intentos fallidos.</contexto>
<tarea>Piensa paso a paso que puede fallar y escribe 6 casos de prueba.</tarea>
<formato>Tabla con las columnas: ID, escenario, datos de entrada,
resultado esperado.</formato>
```

### Mensaje de autocrítica

```text
Revisa tu tabla: faltan casos limite como campos vacios, correo sin @
o contrasena con espacios? Agrega los que falten e indica cuales agregaste.
```
