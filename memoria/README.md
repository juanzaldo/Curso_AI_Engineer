# Memorias del Bootcamp AI Engineer

Este índice reúne las guías para repetir el curso con otros alumnos y compañeros de trabajo. Cada memoria explica qué se quería lograr, por qué se eligió una solución, cómo se realizó y qué se comprobó.

**Inicio del registro:** 6–7 de octubre de 2026.  
**Proyecto:** Agente Operador — Código Facilito, segunda generación.  
**Repositorio del alumno:** [Curso_AI_Engineer](https://github.com/juanzaldo/Curso_AI_Engineer).  
**Primera entrega:** [practica/clase-1](https://github.com/juanzaldo/Curso_AI_Engineer/tree/practica/clase-1).

## Índice de documentos disponibles

| N.º | Memoria | Conceptos y herramientas | Estado |
|---|---|---|---|
| 00 | [Instalación y preparación del entorno](00_memoria_de_Instalacion.md) | PowerShell, uv, Python, Git, VS Code, Ollama, Gemini, Groq y publicación de la primera rama | Redactada; incluye evidencia y pendientes explícitos |

Solo se enlazan archivos existentes. Al completar una clase se agrega su documento y una fila a esta tabla.

## Cómo crecerá la documentación

- `00_` queda reservado para la preparación del entorno.
- Las siguientes memorias usarán el número de clase y un título concreto: por ejemplo, `01_cliente_llm_y_proveedores.md`. Ese archivo todavía no se ha creado.
- Si una clase necesita varios documentos, se usarán sufijos: `01_01_conceptos.md`, `01_02_practica.md`.
- Una herramienta que se use en varias clases podrá tener su propia guía en `herramientas/`, enlazada desde las memorias correspondientes. Esa carpeta se creará cuando haga falta.
- Las imágenes o ejemplos auxiliares irán en `recursos/NN/`, sin credenciales ni datos confidenciales.
- Una clase nueva enlazará sus requisitos previos, en vez de copiar toda la instalación.
- Los cambios de versiones o configuración se documentarán con fecha y motivo. No se reescribirá una prueba histórica como si se hubiera ejecutado de nuevo.

## Método de trabajo: especificar, practicar y documentar

Aplicamos una versión sencilla de Spec Driven Development. La especificación expresa la intención antes de programar; la memoria recoge el resultado después de comprobarlo.

1. **Especificación:** objetivo, alcance, entradas, salidas y criterios de aceptación.
2. **Plan:** conceptos necesarios, archivos que se tocarán y pasos previstos.
3. **Implementación:** el alumno realiza los cambios con explicaciones paso a paso.
4. **Validación:** pruebas, comandos y evidencias que demuestren el comportamiento.
5. **Memoria y entrega:** decisiones, errores, pendientes, commit y enlace a la rama.

Durante las prácticas, el asistente guía y explica. Solo modifica código cuando el alumno lo pide explícitamente. La redacción de una memoria también se realiza después de que el alumno la autorice.

## Estructura para las siguientes clases

Esta es la plantilla de contenido, no un archivo de práctica ya terminado:

1. **Ficha:** número, tema, fecha, rama, commit de referencia y estado.
2. **Objetivo y alcance:** qué se construirá y qué queda fuera.
3. **Criterios de aceptación:** comportamientos observables que deben cumplirse.
4. **Requisitos:** memorias previas, herramientas, cuentas y datos de ejemplo.
5. **Conceptos:** explicación breve con ejemplos del proyecto.
6. **Plan y decisiones:** archivos afectados y razones de cada elección.
7. **Práctica:** pasos con objetivo → motivo → acción → resultado esperado → verificación.
8. **Validación:** resultados reales, separados de los ejemplos y de las pruebas pendientes.
9. **Problemas resueltos:** síntoma, causa identificada y solución.
10. **Entrega:** revisión del diff, commit, rama y enlace.
11. **Aprendizajes y pendientes:** qué practicar después.
12. **Referencias y cambios:** fuentes oficiales y registro de actualizaciones.

## Reglas para que otro alumno pueda repetirlo

- Los comandos de esta primera memoria están escritos para **PowerShell en Windows**.
- Cada alumno adapta `$carpetaCurso`, el usuario de GitHub y el nombre de su repositorio.
- Las versiones registradas son evidencia de esta sesión; las descargas futuras pueden ofrecer otras versiones.
- Los resultados de APIs pueden variar. Una respuesta distinta no implica necesariamente un fallo.
- No se copian claves reales a documentos, capturas o commits. El archivo `.env` se configura de manera privada.
- Los archivos Markdown se leen en GitHub o con la vista previa de VS Code: **Ctrl + Shift + V**.

## Cómo guardar y publicar una memoria

Desde la raíz del repositorio, después de revisar el contenido:

```powershell
git status
git add memoria/README.md memoria/00_memoria_de_Instalacion.md
git diff --cached
git commit -m "Documenta instalacion y preparacion del entorno"
git push
```

Estos comandos corresponden a la primera memoria. En las siguientes clases se sustituyen los nombres por los archivos que realmente se hayan creado o actualizado.

La creación local de un Markdown no lo publica automáticamente. Se necesita un commit y un push. El contenido de estas memorias está dentro de `bootcamp` para que pueda versionarse junto con el curso.
