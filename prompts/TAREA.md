# Tarea: Mi prompt avanzado

## Tarea elegida

Generar casos de prueba para un formulario de registro de usuarios con nombre, correo y contraseña.

## Versión 1: prompt básico

```text
Dame casos de prueba para un registro de usuarios.
```

- Técnica: prompt básico, sin técnicas avanzadas.
- Resultado: generó 25 casos, pero asumió confirmación de contraseña y aceptación de términos.
- Mejora necesaria: definir los campos, las reglas y el formato.

## Versión 2

```text
Actúa como analista de pruebas de aplicaciones web.
Genera 6 casos de prueba para un registro con nombre, correo y contraseña.
Todos los campos son obligatorios. El correo debe contener @ y no estar registrado. La contraseña debe tener al menos 8 caracteres; no se exige mayúscula, número ni símbolo.
Presenta una tabla con ID, escenario, datos de entrada y resultado esperado.
No agregues otros campos ni requisitos.
```

- Técnica agregada: role prompting, con reglas y formato definidos.
- Motivo: enfocar la respuesta en el formulario solicitado.
- Mejora observada: produjo 6 casos concretos, aunque CP-06 combinó dos errores.

## Versión 3: prompt final

```text
<rol>
Actúa como analista de pruebas de aplicaciones web.
</rol>

<contexto>
Registro con nombre, correo y contraseña.
Todos los campos son obligatorios.
El correo debe contener @ y no estar registrado.
La contraseña debe tener al menos 8 caracteres.
No se exige mayúscula, número ni símbolo.
</contexto>

<tarea>
Genera exactamente 8 casos: registro válido, nombre vacío,
correo vacío, contraseña vacía, correo sin @, correo duplicado,
contraseña de 7 caracteres y contraseña de 8 caracteres.
Cada caso negativo debe probar un solo error, con los demás
datos válidos. Usa correos no registrados salvo en el caso
de correo duplicado. Cada prueba es independiente.
</tarea>

<formato>
Tabla con ID, escenario, datos de entrada y resultado esperado.
Usa datos concretos y una frase breve por resultado.
</formato>

<autocritica>
Antes de entregar, revisa que estén los 8 casos, que las
contraseñas tengan la longitud indicada y que no combines
errores ni agregues requisitos. Corrige lo necesario.
Después de la tabla, indica brevemente si corregiste algo.
</autocritica>
```

- Técnicas agregadas: prompt estructurado y autocrítica; se conserva el rol.
- Motivo: organizar las instrucciones y revisar el resultado antes de entregarlo.
- Mejora observada: separó los errores e incluyó pruebas del límite de 8 caracteres.

## Técnicas usadas en el prompt final

| Técnica             | Parte del prompt                                              |
| ------------------- | ------------------------------------------------------------- |
| Role prompting      | Rol de analista de pruebas de aplicaciones web.               |
| Prompt estructurado | Etiquetas de rol, contexto, tarea y formato.                  |
| Autocrítica         | Revisión de cantidad, longitudes y errores antes de entregar. |

## Evaluación del resultado

| Criterio                                   | Cumple (Sí/No) |
| ------------------------------------------ | -------------- |
| Presenta exactamente 8 casos.              | Sí             |
| Usa las 4 columnas solicitadas.            | Sí             |
| Cada caso negativo prueba un solo error.   | Sí             |
| Incluye contraseñas de 7 y 8 caracteres.   | Sí             |
| Respeta los campos y requisitos definidos. | Sí             |

## Por qué elegí estas técnicas

Elegí el rol para orientar las pruebas, la estructura para separar las instrucciones y la autocrítica para revisar el resultado. No usé few-shot porque el formato ya estaba definido, ni descomposición porque la tarea era breve.
