# 📘 Manual Técnico del Programador y Arquitectura de Código

**Proyecto:** Sistema de Modelado de Datos con Estructuras y Punteros (Actividad 5)  
**Institución:** E.E.S.T. N° 1 "Eduardo Ader" — Vicente López  
**Asignatura:** Laboratorio de Programación (LPR) — 5° Año  
**Docente:** Mansilla Muñoz York Elías  
**Autor / Grupo:** Gabriel Zacarías, Sofía Mojica, Leonel De Armas, Mateo Roberts (Grupo N.º 3)  
**Fecha:** 12 de Octubre de 2026 | **Versión:** v1.0.0  

---

## 📋 Control de Versiones y Changelog

| Versión | Fecha | Autor | Descripción de Cambios |
| :--- | :--- | :--- | :--- |
| **v1.0.0** | 12/10/2026 | Grupo 3 | Versión inicial del modelo estructurado del componente de hardware (`struct`) mediante pasaje por referencia indirecta (`->`). |

---

## 🏗️ 1. Arquitectura del Sistema y Entorno de Desarrollo

### Requisitos del Entorno
* **Compilador:** `g++` (MinGW-w64 GCC v16.2.0 o superior). Estándar C++11 o superior habilitado.
* **IDE recomendado:** Visual Studio Code con extensión *C/C++ Extension Pack* y *Code Runner*.
* **Shell:** Windows PowerShell 5.1 o PowerShell Core 7+.

### Estructura de Directorios del Repositorio

```text
sistemaproyecto/
├── .gitignore                      <-- Exclusiones de Git (.exe, .vscode/)
├── LICENSE                         <-- Licencia MIT de uso escolar
├── README.md                       <-- Portada técnica del proyecto
├── docs/                           <-- Documentación y manuales técnicos
│   ├── InformeEEST1_LPR2026_ACT05_G03_v1.0.0.pdf  <-- Informe Formal (APA v7)
│   └── manuales/
│       ├── manual_programador_v1.0.0.pdf          <-- Este documento en PDF
│       └── manual_programador_v1.0.0.md           <-- Este documento en Markdown
├── src/                            <-- Código fuente compilable
│   ├── main.cpp                    <-- Código fuente C++ unificado
│   └── sistemaproyecto.exe         <-- Ejecutable local (ignorado por Git)
└── capturas/                       <-- Evidencias de ejecución (.png)
    └── ejecucion_struct.png        <-- Captura de pantalla de la terminal
```

---

## 🧩 2. Documentación de Módulos y Funciones (`src/main.cpp`)

### 📦 Definición de la Entidad de Datos
```cpp
struct EntidadProyecto {
    int id;
    char nombre[50];
    float metrica; 
};
```
* **Propósito:** Encapsular los atributos heterogéneos de un componente de hardware o sensor (identificador, etiqueta de texto y lectura analógica) en un único bloque de almacenamiento continuo dentro de la memoria RAM.

### ⚙️ Módulo 1: `void cargarDatos(EntidadProyecto* ptr)`
* **Propósito:** Realizar la carga estructurada de datos ingresados por el usuario directamente sobre la celda de memoria original mediante pasaje por dirección.
* **Firma:** `void cargarDatos(EntidadProyecto* ptr)`
* **Mecánica e Implementación:**
  1. `cin >> ptr->id;` → Utiliza el **operador flecha (`->`)** para acceder de forma indirecta al miembro entero e inyectar el valor en la RAM sin copias redundantes.
  2. `cin.ignore();` → Vacía el salto de línea (`\n`) huérfano remanente en el buffer de entrada del teclado para prevenir fallas de lectura en la instrucción inmediata posterior.
  3. `cin.getline(ptr->nombre, 50);` → Captura de forma segura cadenas de caracteres con espacios sin desbordar el array de destino asignado.
  4. `cin >> ptr->metrica;` → Asignación del valor en punto flotante de la lectura del dispositivo.

---

## 🚀 3. Instrucciones de Compilación y Depuración

### Compilación desde PowerShell
Ubicándose en la raíz del proyecto (`sistemaproyecto/`), ejecute los comandos oficiales:

```powershell
# Compilación del fuente hacia la carpeta src
g++ src/main.cpp -o src/sistemaproyecto.exe

# Ejecución del binario resultante
.\src\sistemaproyecto.exe
```

### Diagnóstico de Errores Frecuentes
1. **Error:** `'g++' no se reconoce como un comando interno o externo...`
   * *Causa:* Las variables de entorno de Windows (`PATH`) no incluyen el directorio binario del compilador.
   * *Solución:* Agregar la ruta `C:\msys64\ucrt64\bin` al PATH del sistema y reiniciar el entorno de VS Code de forma completa.
2. **Error:** `error: expected '}' at end of input`
   * *Causa:* Falta de simetría de llaves analíticas; el bloque de la función de carga (`cargarDatos`) quedó abierto.
   * *Solución:* Incorporar el token de cierre `}` al final exacto del archivo fuente.
3. **Anomalía:** *La terminal "se salta" la solicitud del nombre del dispositivo.*
   * *Causa:* Saturación por el carácter nulo acumulado en el buffer de lectura de hardware.
   * *Solución:* Asegurar la presencia de la función de control `cin.ignore();` inmediatamente posterior a la primera lectura por consola (`cin >>`).

---

## 📚 4. Referencias
* Kernighan, B. W., & Ritchie, D. M. (1988). *El lenguaje de programación C* (2.ª ed.). Prentice Hall.
* Stroustrup, B. (2013). *The C++ programming language* (4th ed.). Addison-Wesley.
