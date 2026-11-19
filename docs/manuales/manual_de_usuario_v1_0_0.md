# GUÍA DE USUARIO Y OPERACIÓN DEL SISTEMA

* **Proyecto:** Mini Juego "Piedra, Papel o Tijera" con Persistencia de Datos (`struct + fstream`)
* **Institución:** E.E.S.T. N.° 1 "Eduardo Ader" — Vicente López
* **Asignatura:** Laboratorio de Programación (LPR) — 5° Año 3° Grupos A-B
* **Docente:** Prof. Mansilla Muñoz York Elías
* **Autor / Grupo:** [Apellido y Nombre / Grupo 03]
* **Versión:** v1.0.0 | **Fecha:** 16 de octubre de 2026

---

## CONTROL DE VERSIONES

| Versión | Fecha | Descripción |
| :--- | :--- | :--- |
| **v1.0.0** | 16/10/2026 | Emisión de la guía inicial del usuario para la versión ejecutable en consola con persistencia de partidas en disco (`historial_partidas.txt`). |

---

## 1. REQUISITOS MÍNIMOS DEL SISTEMA

* **Sistema Operativo:** Windows 10 o Windows 11 (64-bit).
* **Consola de Comandos:** Windows PowerShell o Símbolo del sistema (CMD).
* **Memoria RAM:** 512 MB libres.
* **Almacenamiento:** 10 MB de espacio disponible en disco (con permisos de lectura y escritura en la carpeta del proyecto para generar `historial_partidas.txt`).

---

## 2. GUÍA PASO A PASO DE EJECUCIÓN

### Paso 1: Apertura de la Terminal
Abra la carpeta raíz del proyecto `piedrapapelotijera` en el Explorador de Archivos de Windows, presione la tecla **Shift** y haga clic derecho en un área vacía. Seleccione *"Abrir la ventana de PowerShell aquí"* (o abra la terminal integrada de Visual Studio Code con `Ctrl + ñ`).

### Paso 2: Invocación del Ejecutable
En la línea de comandos de PowerShell, ingrese la ruta del binario compilado y presione **Enter**:

```powershell
.\src\piedrapapelotijera.exe
```

### Paso 3: Navegación por el Menú Principal
Al iniciar, el sistema despliega un menú interactivo con tres opciones numeradas:

* **Opción 1 — Jugar Partida (Piedra, Papel o Tijera):** Solicita el nombre o nickname del jugador y su jugada (`1. Piedra`, `2. Papel` o `3. Tijera`). La Inteligencia Artificial genera su jugada al azar, se determina el resultado (*Victoria*, *Derrota* o *Empate*) y el registro se almacena automáticamente en disco.
* **Opción 2 — Ver Historial de Partidas Guardadas en Disco (.txt):** Lee el archivo `historial_partidas.txt` y lista en pantalla todas las partidas acumuladas, incluso si se cerró y volvió a abrir el programa.
* **Opción 3 — Salir del Sistema:** Finaliza la ejecución de manera segura confirmando que los datos quedaron resguardados en almacenamiento secundario.

### Paso 4: Interpretación de los Resultados
Una vez ejecutada una partida y consultado el historial, la consola muestra la trazabilidad de cada encuentro y la confirmación de escritura en disco (Microsoft Corporation, 2026).

#### Figura 1
*Salida en consola del menú principal, partida jugada y lectura de historial persistido*

```text
=====================================================
 LPR 2026 - ACTIVIDAD 7: PIEDRA, PAPEL O TIJERA
 Estudiante / Grupo: [Su Nombre y Apellido]
=====================================================

--- MENU PRINCIPAL DE JUEGO Y PERSISTENCIA ---
1. Jugar Partida (Piedra, Papel o Tijera)
2. Ver Historial de Partidas Guardadas en Disco (.txt)
3. Salir del Sistema
Ingrese una opcion (1-3): 1

--- NUEVA PARTIDA #1 ---
Ingrese su Nombre / Nickname: [Jugador]

Elija su jugada:
1. Piedra
2. Papel
3. Tijera
Opcion (1-3): 1

[JUGADA] [Jugador] eligio: Piedra
[JUGADA] La IA eligio: Tijera
=> RESULTADO: Victoria!
[DISCO] Partida resguardada con exito en 'historial_partidas.txt'.

--- MENU PRINCIPAL DE JUEGO Y PERSISTENCIA ---
1. Jugar Partida (Piedra, Papel o Tijera)
2. Ver Historial de Partidas Guardadas en Disco (.txt)
3. Salir del Sistema
Ingrese una opcion (1-3): 2

=====================================================
 HISTORIAL DE PARTIDAS RECUPERADO DESDE DISCO
=====================================================
Partida #1 | Jugador: [Jugador] | Piedra vs Tijera | Resultado: Victoria

[SISTEMA] Total de registros leidos desde disco: 1
=====================================================
```

> *Nota.* La salida ilustra el ciclo completo de juego contra la IA, la confirmación de persistencia en `historial_partidas.txt` y la recuperación secuencial de registros mediante la Opción 2.

---

## 3. RESOLUCIÓN DE PROBLEMAS FRECUENTES (FAQ)

1. **La ventana de la consola se abre y se cierra instantáneamente.**
   * **Causa:** El usuario ejecutó el archivo haciendo doble clic desde el Explorador de Windows sin una sesión de terminal activa, o ingresó un carácter no numérico en el menú.
   * **Solución:** Ejecute siempre el programa desde una ventana de PowerShell previamente abierta (`.\src\piedrapapelotijera.exe`) e ingrese únicamente valores numéricos entre `1` y `3`.

2. **Windows Defender o SmartScreen bloquea la ejecución.**
   * **Causa:** El archivo ejecutable `piedrapapelotijera.exe` ha sido compilado localmente con `g++` y no posee firma digital comercial.
   * **Solución:** En la ventana de advertencia de SmartScreen, haga clic en *"Más información"* y luego seleccione el botón *"Ejecutar de todas formas"*.

3. **Al seleccionar la Opción 2 aparece el mensaje `"[AVISO] Aun no existen partidas guardadas en disco."`**
   * **Causa:** Aún no se ha completado ninguna partida (el archivo `historial_partidas.txt` se crea automáticamente al finalizar la primera jugada) o el programa se ejecutó fuera de la carpeta raíz `piedrapapelotijera`.
   * **Solución:** Verifique que la terminal esté posicionada en la raíz del proyecto y juegue al menos una partida mediante la **Opción 1** antes de consultar el historial.

---

## 4. REFERENCIAS

* Microsoft Corporation. (2026). *Documentación de Windows PowerShell*. https://learn.microsoft.com/powershell/