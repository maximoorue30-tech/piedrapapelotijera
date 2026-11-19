# MANUAL TÉCNICO DEL PROGRAMADOR Y ARQUITECTURA DE CÓDIGO

* **Proyecto:** Mini Juego "Piedra, Papel o Tijera" con Persistencia de Datos (Actividad 7)
* **Institución:** E.E.S.T. N.° 1 "Eduardo Ader" — Vicente López
* **Asignatura:** Laboratorio de Programación (LPR) — 5° Año 3° Grupos A-B
* **Docente:** Prof. Mansilla Muñoz York Elías
* **Autor / Grupo:** [Apellido y Nombre / Grupo 03]
* **Fecha:** 16 de octubre de 2026 | **Versión:** v1.0.0

---

## CONTROL DE VERSIONES Y CHANGELOG

| Versión | Fecha | Autor | Descripción de Cambios |
| :--- | :--- | :--- | :--- |
| **v1.0.0** | 16/10/2026 | [Autor / Grupo 03] | Versión inicial del juego modular en C++ con estructuras de datos (`struct Partida`), persistencia en disco (`fstream`) y sincronización Dual-Remote. |

---

## 1. ARQUITECTURA DEL SISTEMA Y ENTORNO DE DESARROLLO

### Requisitos del Entorno
* **Compilador:** `g++` (MinGW-w64 GCC v8.1.0 o superior) con estándar `-std=c++11` habilitado.
* **Librerías Estándar Utilizadas:** `<iostream>`, `<fstream>`, `<string>`, `<cstdlib>` y `<ctime>`.
* **IDE recomendado:** Visual Studio Code con extensión *C/C++ Extension Pack*.
* **Shell y Control de Versiones:** Windows PowerShell 5.1+ y Git configurado en modo Dual-Remote (GitHub + GitLab).

### Estructura de Directorios del Repositorio

```text
/piedrapapelotijera/
├── .gitattributes          <-- Normalización de finales de línea
├── .gitignore              <-- Exclusiones (.exe, *.out, .vscode/)
├── LICENSE                 <-- Licencia MIT escolar
├── README.md               <-- Portada del proyecto con integrantes
├── CHANGELOG.md            <-- Historial de versiones del software
├── docs/                   <-- Entregables y documentación
│   ├── InformeEEST1_LPR2026_ACT07_G03_[ApellidoNombre]_Informe_v1.0.0.pdf
│   └── manuales/
│       ├── manual_programador_v1.0.0.pdf
│       ├── manual_programador_v1.0.0.md
│       ├── manual_usuario_v1.0.0.pdf
│       └── manual_usuario_v1.0.0.md
├── src/                    <-- Código fuente compilable
│   └── main.cpp            <-- Programa principal del juego en C++
├── data/                   <-- Para archivos persistentes
│   └── historial_partidas.txt <-- Archivo de persistencia generado
└── capturas/               <-- Evidencias de ejecución (.png)
    ├── jugada_consola.png  <-- Captura del menú y partida jugada
    └── archivo_disco.png   <-- Captura del archivo .txt abierto
```

---

## 2. DOCUMENTACIÓN DE ESTRUCTURAS, MÓDULOS Y FUNCIONES (`src/main.cpp`)

### Estructura de Datos: `struct Partida`
* **Propósito:** Agrupar cinco variables heterogéneas en una única entidad lógica en memoria RAM (Stroustrup, 2013) antes de serializarlas hacia el disco.
* **Campos:**
  * `int idPartida`: Identificador secuencial de la jugada.
  * `string jugador`: Nombre o nickname del usuario.
  * `string eleccionJugador`: Selección del usuario (`Piedra`, `Papel` o `Tijera`).
  * `string eleccionIA`: Selección aleatoria de la consola.
  * `string resultado`: Desenlace de la partida (`Victoria`, `Derrota` o `Empate`).

### Módulo 1: `void jugarPartida(int& contadorID)`
* **Propósito:** Gestionar la interacción de una ronda contra la IA y disparar el guardado inmediato en disco.
* **Firma:** `void jugarPartida(int& contadorID)` (recibe el contador por referencia para auto-incrementar el ID de partida).
* **Lógica y Manejo de Búfer:** Invoca `cin.ignore()` para descartar el carácter de salto de línea (`\n`) residual en el búfer de entrada antes de leer `p.jugador` con `getline(cin, p.jugador)`. Genera la jugada de la IA mediante `(rand() % 3) + 1`, evalúa las reglas del juego y delega la persistencia a `guardarEnDisco(p)`.

### Módulo 2: `void guardarEnDisco(const Partida& p)`
* **Propósito:** Persistir de forma no volátil los campos de la estructura `Partida` en un archivo de texto plano delimitado por comas (Kernighan & Ritchie, 1988).
* **Firma:** `void guardarEnDisco(const Partida& p)` (paso por referencia constante para evitar copias innecesarias en memoria).
* **Mecánica de Flujo (`ofstream`):** Abre el flujo en modo anexar (`ios::app`) para escribir al final del archivo sin sobrescribir el historial previo, valida `archivo.is_open()`, serializa los cinco atributos separados por `,` y cierra el descriptor con `archivo.close()`.

### Módulo 3: `void leerHistorialDisco()`
* **Propósito:** Recuperar y desplegar en consola todas las partidas almacenadas en almacenamiento secundario.
* **Firma:** `void leerHistorialDisco()`
* **Mecánica de Lectura (`ifstream`):** Abre el flujo de entrada, verifica su existencia y utiliza un bucle `while` con llamadas encadenadas a `getline(archivo, campo, ',')` para parsear cada registro CSV línea por línea, contabilizando el total de registros recuperados.

---

## 3. INSTRUCCIONES DE COMPILACIÓN, DEPURACIÓN Y SINCRONIZACIÓN GIT

### Compilación y Ejecución desde PowerShell
Ubicándose en la raíz del repositorio `piedrapapelotijera`, ejecute:

```powershell
# 1. Compilación limpia habilitando estándar C++11
g++ -std=c++11 src/main.cpp -o src/piedrapapelotijera.exe

# 2. Ejecución directa del binario resultante
.\src\piedrapapelotijera.exe
```

### Sincronización Dual-Remote (GitHub + GitLab)

```bash
git add .
git commit -m "feat(act07): implementa juego piedra papel o tijera con persistencia fstream v1.0.0"
git push origin main
git push gitlab main
```

### Diagnóstico de Errores Frecuentes

1. **Error: `'g++' no se reconoce como un comando interno o externo...`**
   * **Causa:** Las variables de entorno de Windows (`PATH`) no incluyen el directorio `bin` de MinGW-w64.
   * **Solución:** Agregar `C:\mingw64\bin` al `PATH` del sistema, reiniciar VS Code / PowerShell y reintentar la compilación.

2. **El programa saltea la lectura de `Nombre / Nickname`.**
   * **Causa:** Falta la llamada a `cin.ignore()` luego de leer la opción numérica del menú con `cin >> opcion`.
   * **Solución:** Mantener `cin.ignore();` inmediatamente antes de `getline(cin, p.jugador);` en `jugarPartida()`.

3. **Discrepancia de ruta entre `data/historial_partidas.txt` y `src/historial_partidas.txt`.**
   * **Causa:** El código base de referencia abre `src/historial_partidas.txt`, mientras que la arquitectura de repositorio organiza los datos persistentes en `data/historial_partidas.txt`.
   * **Solución:** Asegurar que la ruta pasada a los constructores de `ofstream` e `ifstream` coincida con la ubicación elegida (`data/historial_partidas.txt`) y verificar que la carpeta exista antes de ejecutar.

---

## 4. REFERENCIAS

* Kernighan, B. W., & Ritchie, D. M. (1988). *El lenguaje de programación C* (2.ª ed.). Prentice Hall.
* Stroustrup, B. (2013). *The C++ programming language* (4th ed.). Addison-Wesley.