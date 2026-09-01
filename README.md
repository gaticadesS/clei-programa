# Programa de la 52ª CLEI 2026 — ITAM

Página web del programa del congreso, pensada para consultarse desde el celular
mediante un código QR. Un solo archivo, sin dependencias externas.

- **Sede:** Instituto Tecnológico Autónomo de México, Ciudad de México
- **Fechas:** 7 al 11 de septiembre de 2026
- **Sitio oficial:** https://conferencia2026.clei.org/es-cl/inicio/

---

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La página completa. Es lo único que se publica. |
| `README.md` | Este documento. |

`index.html` contiene tres cosas: el diseño (CSS), el programa (un bloque de datos)
y la lógica (JavaScript). **Para cambiar el programa solo se toca el bloque de datos.**

---

## Cómo cambiar el programa

1. En GitHub, abre `index.html` y haz clic en el lápiz (**Edit this file**).
2. Busca la línea que empieza con `<script type="application/json" id="datos">`.
   Todo el programa está ahí, en una sola línea larga.
3. Haz el cambio que necesites (ver ejemplos abajo).
4. Baja hasta el final y haz clic en **Commit changes**.
5. La página se actualiza sola en uno o dos minutos. El código QR no cambia.

### Ejemplos

**Cambiar la sala de una sesión:** busca el código de la sesión, por ejemplo `"cod":"IA-7"`,
y edita el valor de `"sala"` que está junto a él.

**Cambiar un horario:** edita `"ini"` (hora de inicio) y `"fin"` (hora de término).
Siempre en formato de 24 horas con dos dígitos: `"16:30"`.

**Agregar los autores de una ponencia:** dentro de la ponencia, junto a `"n"` y `"t"`,
se agrega `"a":["Nombre Apellido","Otro Nombre"]`. La página los abrevia sola.

**Llenar una sesión que está por confirmar:** cambia `"estado":"por-confirmar"`
por `"estado":"ok"` y sustituye `"pon":[]` por la lista de ponencias:

```
"pon":[{"n":101,"t":"Título de la primera ponencia"},
       {"n":102,"t":"Título de la segunda ponencia"}]
```

**Cancelar una sesión:** lo más claro para el asistente es dejarla visible.
Cambia el `"tipo"` a `"Sesión cancelada"` y vacía `"pon":[]`.

### Reglas para no romper el archivo

- Las comillas siempre son dobles rectas `"`, nunca comillas curvas.
- Cada dato va separado por coma, pero **el último de una lista no lleva coma**.
- Si un título trae comillas dobles, cámbialas por comillas simples `'`.
- Si algo sale mal, GitHub guarda el historial: entra a **History**, abre la versión
  anterior y usa **Revert** para volver atrás.

---

## Cómo cambiar los colores

La paleta completa está al inicio de la hoja de estilos, dentro de `:root{ }`, con un
comentario que explica para qué sirve cada color. Se cambian ahí y afectan a toda la página.

Los colores de los tracks (verde para Sistemas Inteligentes, rosa para el LAWCC, amarillo
para el TLISC, etc.) **no están en esa paleta**: viven en el bloque de datos, porque son
los mismos colores del programa impreso y deben coincidir con la señalización del evento.

Debajo de `:root{ }` hay un bloque `@media (prefers-color-scheme: dark)` con la versión
para modo oscuro. Si cambias un color de la paleta clara, revisa su equivalente ahí.

Todos los colores actuales cumplen el contraste mínimo AA (4.5 a 1) tanto en modo claro
como en modo oscuro. Si los cambias, conviene volver a verificarlo.

---

## Decisiones de diseño

Se dejan anotadas porque son las primeras que se olvidan y las primeras que se preguntan.

- **La página abre en el día actual solo si la fecha coincide exactamente** con un día del
  congreso. Fuera de esas fechas abre en lunes y no marca nada como "en curso". Se descartó
  la opción de identificar el día por día de la semana para no mostrar información engañosa
  antes del evento.
- **Al empezar a escribir en el buscador se limpia el filtro de tema**, pero si ya hay texto
  escrito se puede aplicar un filtro y se combina. Surgió de las pruebas con usuarios: varias
  personas buscaban con un filtro activo sin darse cuenta y no encontraban nada.
- **Sin tipografías ni imágenes externas.** La página no pide nada a otros servidores, para
  que cargue rápido con el wifi saturado del congreso y siga funcionando sin conexión.
- **Los recesos y comidas se muestran como líneas delgadas**, no como tarjetas, para que el
  programa del día quepa en menos pantallas.
- **La hora "en curso" usa el reloj del dispositivo de cada persona**, no un reloj del servidor.
- **Sin logotipos institucionales**, por decisión de la organización.
- **Los autores se muestran abreviados**: inicial del nombre de pila y el resto del nombre
  completo (`M. Fernanda Papa`), para no perder apellidos compuestos. Se muestran hasta
  cuatro por ponencia y el resto se resume como "y N más". Si se busca por un autor que
  quedó oculto, la lista se despliega completa en ese resultado.
- **El buscador cubre título, autor, sala, código y tipo de sesión**, en los cinco días.
- **No se guardan correos ni afiliaciones**, solo el nombre de cada autor.
- **Ante cualquier diferencia entre el PDF de artículos y las imágenes del programa,
  gana el PDF.** Indicación de la organización.
- **Las presentaciones virtuales se marcan con la etiqueta VIRTUAL y van al final de su
  sesión.** Se declaran en la lista `VIRTUALES` del generador; en `index.html` aparecen
  con `"v":1` dentro de la ponencia.

---

## Pendientes de contenido

Aparecen en la página como **programa por confirmar**, con su horario y sala visibles
(ocho bloques en total):

- Los cuatro bloques del TLISC en Bib3 (miércoles y jueves).
- Las cuatro Conferencias Magistrales. El sitio oficial ya publica cuatro ponentes con sus
  títulos, pero no indica qué día le toca a cada uno, así que falta esa asignación.

Otros puntos abiertos:

- Qué artículo es el virtual en cada una de las nueve sesiones con presentación virtual
  (IA-1, IA-8, IA-14, IA-16, SOFT-3, EDU-3, PRACT-7, TEC-3 y LAWCC-5).
- El tipo de sesión de LAWCC-3 y LAWCC-7, las dos sesiones nuevas en Bib2.
- La sala de las Conferencias Magistrales: el sitio oficial dice auditorio del ITAM.
- La LANC (Conferencia Latinoamericana de Redes) aparece como evento asociado en el sitio
  oficial pero no está en los horarios recibidos.
- **Los nombres de las salas (`Bib1`, `Bib2`, `Bib3`) son provisionales** y se definirán más
  cerca del evento, en función del número de personas registradas.

---

## Historial de cambios en el programa

- **1 de septiembre de 2026.** Se agregaron los autores de las 169 ponencias numeradas a
  partir de la tabla `authors_accepted_clei2026.xlsx`, y el buscador ahora también busca
  por autor.

- **31 de agosto de 2026.** Se retiró #331 de TEC-3; #234 salió de TEC-2 y entró #78, que
  venía de TEC-5; se corrigió el número de la ponencia de IA-6 (#201 a #210) y el título de
  la #211 en EDU-3; PRACT-7 cambió de orden y ahora empieza a las 9:00; LAWCC-8 incluye la
  premiación. Se agregó el soporte para marcar presentaciones virtuales.

- **26 de agosto de 2026.** El LAWCC pasó de seis a ocho sesiones y cambió su numeración.
  Se agregaron dos sesiones nuevas en Bib2 (miércoles y jueves, 14:00-15:00) y se cargaron
  las ponencias de las ocho. Las imágenes del programa impreso todavía no reflejan este cambio.

---

## Publicación

La página se publica con GitHub Pages desde la rama `main`, carpeta raíz (`/`).
Se configura en **Settings → Pages**.

Después de cada cambio, GitHub tarda entre uno y dos minutos en actualizar el sitio.
Si no ves el cambio, recarga forzando la actualización del caché
(en el celular: cierra la pestaña y vuelve a abrirla).
