# Sistema de Gestión de Turnos Automáticos para Farmacia Independiente

## ✅ Descripción General del Sistema
Este proyecto corresponde al modelado completo de un **Sistema de Gestión de Turnos Automáticos**, diseñado para optimizar la atención al cliente en una **farmacia independiente**, garantizando fluidez, trazabilidad y eficiencia en el proceso de asignación y atención de turnos.

El sistema busca resolver los cuellos de botella típicos en farmacias de atención presencial mediante:
- Asignación automática de turnos según prioridad y tipo de atención.
- Visualización en tiempo real del estado de la fila.
- Llamado automatizado mediante pantallas y notificaciones.
- Gestión centralizada de los módulos de atención y sus operadores.
- Accesos diferenciados para operadores, supervisores y administradores.

---

## 🔍 Objetivos del Modelado
- Realizar una transición completa desde los requerimientos funcionales hasta el despliegue físico del sistema.
- Aplicar patrones de diseño para robustecer la arquitectura y su escalabilidad.
- Desarrollar un sistema modular, mantenible y alineado con las buenas prácticas de diseño orientado a objetos.

---

## 🔹 1. Diagrama de Casos de Uso UML
![imagen](https://github.com/user-attachments/assets/8e0c00b8-1a2b-4415-a6e1-1bc5e92afa84)


### Descripción general
El análisis funcional permitió identificar los actores clave y los flujos de atención prioritarios. Se aplicaron correctamente las relaciones **<<include>>** y **<<extend>>** para representar flujos obligatorios y opcionales.

#### Actores identificados:
- **Cliente**: Solicita turno según el tipo de atención (receta, OTC, consulta).
- **Operador de Módulo**: Atiende turnos asignados y los marca como completados.
- **Administrador de Farmacia**: Gestiona usuarios, módulos y configuración del sistema.
- **Supervisor**: Monitorea en tiempo real el estado de las filas y genera reportes.
- **Pantalla de Llamado**: Actor externo que refleja el turno llamado.

#### Casos de uso destacados:
- **Solicitud de Turno Automático**
  - `<<extend>>` **Asignación Prioritaria según Perfil del Cliente** (ej.: embarazadas, tercera edad).
- **Atención de Turno en Módulo**
  - `<<include>>` **Registro de Atención Realizada**.
  - `<<extend>>` **Escalamiento a Supervisor** en caso de incidentes.
- **Llamado de Turno a Pantalla**
  - Comunicación obligatoria con el actor externo **Pantalla de Llamado**.
- **Consulta del Estado de la Fila**
  - `<<extend>>` **Generación de Reporte Diario de Atenciones**.
- **Configuración de Parámetros del Sistema**
  - Gestión de tiempos máximos de espera, número de módulos y tipos de atención.

#### Justificación de relaciones:
- `<<include>>` se utilizó para flujos obligatorios como el registro posterior a una atención.
- `<<extend>>` se empleó en funciones condicionales como llamados prioritarios o generación de reportes.

---

## 🔹 2. Diagrama de Clases UML con Patrones Aplicados
![imagen](https://github.com/user-attachments/assets/4813591a-c6d9-4dc5-be5d-f12d54d38df2)


## 🧩 Justificación Arquitectónica y Patrones Aplicados

### 1. Singleton (ConfiguracionTurnos)
**Justificación:**  
Permite la **gestión centralizada de parámetros críticos del sistema**, como tiempos de espera máximos, tipos de atención y alertas por demora.

**Intención:**  
- Garantizar una única fuente de verdad para la configuración.  
- Facilitar acceso global y seguro a dichos parámetros.  
- Prevenir inconsistencias operativas en los módulos de atención.

---

### 2. Prototype (PlantillaTurno)
**Justificación:**  
En horarios punta o campañas de salud se generan múltiples turnos similares. Prototype permite **clonar plantillas de turnos predefinidos**, agilizando el proceso.

**Intención:**  
- Optimizar la creación de turnos frecuentes.  
- Adaptar fácilmente la estructura de turnos a eventos especiales.  
- Reducir tiempos de espera en la atención.

---

### 3. Adapter (AdaptadorPantalla)
**Justificación:**  
La pantalla de llamado puede variar en hardware o software. Adapter permite **adaptar el sistema a distintas interfaces de visualización** (web, LED, TV smart).

**Intención:**  
- Desacoplar el núcleo del sistema de los dispositivos externos.  
- Facilitar integraciones con distintas marcas/modelos.  
- Permitir actualizaciones sin modificar la lógica interna.

---

## 🔹 3. Diagrama de Implementación UML
![imagen](https://github.com/user-attachments/assets/7b3050da-23ae-4212-b949-4c53ab70fe0c)


# Explicación del Diagrama de Implementación UML

## 🗂️ Paquetes (Nodos Físicos)

El sistema ha sido organizado en cuatro nodos principales, que representan los distintos módulos físicos y lógicos dentro de la arquitectura:

- **Servidor Principal:**  
  Núcleo del sistema donde reside la lógica de negocio y la configuración global.

- **Pantalla de Llamado:**  
  Dispositivo dedicado a mostrar los turnos vigentes al público.

- **Módulo Operador:**  
  Terminal utilizada por los trabajadores de la farmacia para llamar y gestionar turnos.

- **Admin/Supervisor PC:**  
  Equipo usado para configurar el sistema, generar reportes y gestionar la operación.

## 🧩 Componentes

Cada nodo contiene uno o más componentes software representados en el diagrama:

- **Servidor Principal:**
  - *Lógica de Turnos:* Maneja la asignación, llamado y control de turnos. Es el corazón del sistema.
  - *Control de Configuración:* Encargado de los parámetros del sistema, como horarios, prioridades y reglas.
  - *Base de Datos Turnos y Configuración:* Almacena la información operativa y de configuración en un único repositorio.

- **Pantalla de Llamado:**
  - *Visualizador de Turnos:* Renderiza la información actual de llamados y muestra al cliente qué número debe pasar.

- **Módulo Operador:**
  - *Interfaz de Atención:* Herramienta que usa el personal de farmacia para atender pacientes, llamar turnos y marcarlos como finalizados.

- **Admin/Supervisor PC:**
  - *Panel de Configuración y Reportes:* Permite al administrador ajustar parámetros, consultar métricas y generar reportes operacionales.

## 🔄 Relaciones

Las flechas en el diagrama muestran las relaciones funcionales entre módulos:

- Visualizador de Turnos se comunica con la Lógica de Turnos para recibir actualizaciones en tiempo real y mostrar los llamados.
- Interfaz de Atención (operador) interactúa directamente con la Lógica de Turnos para gestionar el flujo de pacientes.
- Panel de Configuración y Reportes se conecta al Control de Configuración para cambiar parámetros del sistema.
- Tanto la Lógica de Turnos como el Control de Configuración acceden directamente a la base de datos para lectura y escritura.

---

## 🧩 Reflexiones Finales del Modelado
Este sistema representa una solución para farmacias independientes que quieran **Digitalizar su atención al cliente**. La aplicación de patrones fue incorporada para mantener una mejor reutilización y escalabilidad a la hora de manejar el sistema.



