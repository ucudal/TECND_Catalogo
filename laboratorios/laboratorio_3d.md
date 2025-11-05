# 🧠 Laboratorio: “Reloj Digital Mecánico” — Manufactura Aditiva y Diseño Colaborativo

---

## 🎯 Descripción general

El objetivo de este proyecto es **diseñar colaborativamente un reloj mecánico digital** que indique:

> Año — Día — Hora — Minuto — Segundo — Décima de segundo

Cada equipo será responsable de **modelar una etapa del sistema** (un conjunto de engranajes) y luego integrar su diseño en una **simulación digital completa** del reloj.

El trabajo no requiere impresión física, sino un enfoque de **manufactura aditiva conceptual**, diseño CAD y simulación digital del movimiento.

---

## 🧩 Asignación de equipos

| Equipo | Módulo del reloj | Unidad de tiempo representada |
|:------|:------------------|:------------------------------|
| 1 | Engranaje base | Décima de segundo |
| 2 | Reducción 1 | Segundo |
| 3 | Reducción 2 | Minuto |
| 4 | Reducción 3 | Hora |
| 5 | Reducción 4 | Día |
| 6 | Reducción 5 | Año |

Cada equipo diseña un **módulo de engranajes** que reduzca la velocidad adecuadamente para que el movimiento del eje principal (décimas de segundo) se traduzca en la unidad de tiempo correspondiente.

---

## ⚙️ Requisitos técnicos

- **Software recomendado:**  
  - Tinkercad. 
  - Cada modelo debe poder exportarse como `.STL` o `.STEP`.  
- **Sin impresión física** — todo el trabajo será digital y conceptual.  
- **Compatibilidad de diseño:**  
  - Cada módulo debe incluir un **eje de salida estandarizado** (diámetro 5 mm) para conectar con el siguiente módulo.  
  - Las relaciones de reducción deben permitir que, al acoplar los módulos, se mantenga la secuencia temporal del reloj.

---

## 🧮 Guía conceptual para los engranajes

1. **Décima de segundo → Segundo:**  
   Relación 1:10  
2. **Segundo → Minuto:**  
   Relación 1:60  
3. **Minuto → Hora:**  
   Relación 1:60  
4. **Hora → Día:**  
   Relación 1:24  
5. **Día → Año:**  
   Relación 1:365  

Cada grupo debe calcular cuántos dientes deben tener sus engranajes para obtener esa relación, considerando:

$$
\text{Relación} = \frac{Z_{\text{conducido}}}{Z_{\text{conductor}}}
$$

Donde:
- Z<sub>conductor</sub>: dientes del engranaje que impulsa  
- Z<sub>conducido</sub>: dientes del engranaje arrastrado

---

## 🧠 Objetivos de aprendizaje

- Aplicar conceptos de **manufactura aditiva digital** en un proyecto integrado.  
- Comprender **relaciones de transmisión y reducción** en mecanismos.  
- Trabajar en equipos interdependientes con interfaces definidas.  
- Usar herramientas CAD para **modelar y simular sistemas mecánicos**.  
- Integrar y validar diseños mediante simulación digital.

---

## 🧩 Entregable final (integración)

Una vez que todos los grupos completen su modelo:

- Pueden importar modelos pre existentes y ajustar la relación.
- Los equipos integrarán sus modelos en un único archivo conjunto (No está permitido modificar los modelos de otros equipos).
- Ajustarán los ejes y las orientaciones para lograr la **transmisión continua desde la décima de segundo hasta el año**.  

*(El objetivo no es lograr precisión absoluta, sino mostrar la coherencia del diseño y la comprensión de los principios)*

