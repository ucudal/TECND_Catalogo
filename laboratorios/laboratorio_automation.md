# 🧪 Laboratorio 3 - Tecnologías para Negocios Digitales

## 🎯 Objetivo
Identificar como se puede usar **Power Automate** para **automatizar tareas repetitivas** relacionadas con tu carrera en la UCU.  

---

## 📝 Consigna
A continuación veremos 3 procesos asociados a tu evolución en la carrera, te proponemos implementarlos con **Azure Power Automate**.

---


## ⚙️ Procesos a automatizar

### 1. Confirmación de inscripción a un curso
- **Trigger:**  
  - *Cuando llegue un correo a Outlook que indique que te haz inscripto a un curso*.  
- **Acciones:**  
  - Extraer información (nombre del curso y fecha).  
  - Registrar automáticamente en una hoja de **Excel Online** con columnas:  
    `Fecha | Tipo de evento | Curso | Califiación`.  
  - Enviar una notificación al estudiante en **Teams** o **Outlook** confirmando que se registró.  

---

### 2. Resultados de un curso
- **Trigger:**  
  - *Cuando llegue un correo a Outlook que indique la aprobación del curso*.  
- **Acciones:**  
  - Leer el nombre del curso y la calificación.  
  - Guardar en la misma planilla de **Excel** en una nueva fila:  
    `Fecha | Tipo de evento | Curso | Calificación`.  
  - Si la calificación es **aprobado**, enviar un emoji 🎉 en la notificación al estudiante.  

---

### 3. Recordatorio de tareas pendientes
- **Trigger:**  
  - *Flujo programado (Scheduled)* que se ejecuta cada lunes a las 9:00 AM.  
- **Acciones:**  
  - Leer la planilla de **Excel** y listar cursos inscritos que aún no tienen resultado registrado.  
  - Generar un correo automático al estudiante con el asunto:  
    > “Recordatorio: tienes cursos pendientes de resultados”  
  - Adjuntar listado de cursos pendientes en el cuerpo del mail.  

---

## 🔗 Conectores utilizados
- **Outlook 365** → Para recibir correos.  
- **Excel Online (Business)** → Para guardar datos en la planilla.  
- **Teams/Outlook** → Para enviar notificaciones.  

---

## ✅ Entregables
- Captura de pantalla mostrando los flujos creados.
- Captura de la planilla **Excel** con al menos un registro completo.  
- Breve documento explicando:
  - Qué servicios de Azure usaron.
  - Cómo podrían utilizar esta herramienta en un proceso de negocio.
