# Programa del CLEI 2026 — ITAM

Página web del programa del congreso, pensada para consultarse desde el celular
mediante un código QR. Un solo archivo, sin dependencias externas.

- **Sede:** Instituto Tecnológico Autónomo de México, Ciudad de México
- **Fechas:** 7 al 11 de septiembre de 2026

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

## Publicación

La página se publica con GitHub Pages desde la rama `main`, carpeta raíz (`/`).
Se configura en **Settings → Pages**.

Después de cada cambio, GitHub tarda entre uno y dos minutos en actualizar el sitio.
Si no ves el cambio, recarga forzando la actualización del caché
(en el celular: cierra la pestaña y vuelve a escanear el QR).

---

## Pendientes de contenido

Al momento de publicar, faltan por confirmar:

- Los títulos de las seis sesiones del LAWCC (miércoles y jueves, EPIC Lab).
- Los ponentes y títulos de las Conferencias Magistrales (los cinco días, 15:00–16:00).
- El contenido de los cuatro bloques TLISC en Bib3 (miércoles y jueves).
- Los nombres de autores y ponentes de todas las ponencias.

Estos bloques aparecen en la página como **programa por confirmar**, con su horario
y sala visibles.
