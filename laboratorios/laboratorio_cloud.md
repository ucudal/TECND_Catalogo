# 🧪 Laboratorio 1 - Tecnologías para Negocios Digitales

## 🎯 Objetivo
Implementar un **mini portal de noticias en la nube para tu negocio digital** utilizando **Azure Blob Storage**, **Azure Function Apps** y **Azure Table Storage**.  
El portal debe mostrar titulares de **NewsAPI** y registrar cada acceso en la nube.

---

## 📝 Consigna
1. **Sitio estático en Azure Blob Storage**
   - Crear un Storage Account en Azure.
   - Habilitar la opción **Static Website**.
   - Utilizano tu GenAI de preferencia, puede crear archivos archivos para el frontend, por ejemplo, `index.html` y `script.js`. Este último para algunos scripts que agregaremos luego.
   - El sitio debe tener un botón para cargar titulares de noticias y mostrarlos en una lista.

2. **Function App – Obtener noticias**
   - Crear una **Azure Function App** (Python o C#).
   - Implementar una función `GetNews` que consulte [NewsAPI](https://newsapi.org) y devuelva un JSON con los titulares.
   - La función debe usar una **API Key** guardada en las **Application Settings**.

3. **Function App – Registrar accesos**
   - Crear otra función `LogAccess`.
   - Cada vez que el sitio cargue noticias, esta función debe guardar un registro en **Azure Table Storage** con:
     - Fecha y hora (UTC).
     - Un identificador único de la operación.

4. **Integración**
   - El `script.js` debe:
     - Llamar a la función `GetNews` para obtener noticias.
     - Mostrar los titulares en el sitio.
     - Llamar a la función `LogAccess` para registrar el acceso.

---

## ✅ Entregables
- URL pública del sitio en Azure Blob Storage.  
- Captura de pantalla mostrando las noticias cargadas.  
- Captura de la tabla `AccessLog` con al menos un registro.  
- Breve documento explicando:
  - Qué servicios de Azure usaron.
  - Cómo se comunican entre sí.

## 💡 IMPORTANTE
- NewsAPI entrega un máximo de 100 requests por día con la versión gratuita.  
- Usar la **Application Settings** en Azure Function App para almacenar credenciales (no incluirlas en el código).  
- El acceso al portal es público, pero las funciones deben manejar la API Key de forma segura.  

---
