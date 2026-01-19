# 🏠 Alertas Visuales para Home Assistant

## 📋 Descripción

Este proyecto contiene 6 blueprints (plantillas) para Home Assistant diseñados específicamente para **personas sordas o con problemas de audición**. Cada blueprint convierte eventos del hogar en **alertas visuales mediante luces de colores** y notificaciones móviles.

**Características principales:**
- ✅ Configuración simple sin conocimientos técnicos
- ✅ Alertas visuales claras con colores distintivos
- ✅ Notificaciones móviles como respaldo
- ✅ Compatible con cualquier luz inteligente de Home Assistant

---

## 🎨 Blueprints Incluidos

### 1. 🚪 **Timbre (doorbell.yaml)**
**Qué hace:** Cuando alguien toca el timbre, las luces parpadean en blanco cálido durante 30 segundos.
- **Color:** Blanco cálido parpadeante (30 segundos)
- **Notificación:** Inmediata al móvil

### 2. 📞 **Telefonillo (intercom.yaml)**
**Qué hace:** Cuando alguien llama al telefonillo, las luces parpadean en blanco frío durante 30 segundos.
- **Color:** Blanco frío parpadeante (30 segundos)
- **Notificación:** Inmediata al móvil
- **Diferencia con timbre:** Color más frío para distinguirlos fácilmente

### 3. 🚨 **Puerta Abierta (open_door.yaml)**
**Qué hace:** Si una puerta permanece abierta más de 5 minutos, las luces parpadean en rojo.
- **Color:** Rojo parpadeante (30 segundos)
- **Tiempo de espera:** 5 minutos
- **Notificación:** Inmediata al móvil

### 4. 💧 **Fuga de Agua (water_leak.yaml)**
**Qué hace:** Detecta fugas de agua y activa alertas visuales azules.
- **Color:** Azul parpadeante (30 segundos)
- **Notificación:** Inmediata al móvil
- **Urgencia:** Alta - requiere atención inmediata

### 5. 🍽️ **Lavavajillas (dishwasher.yaml)**
**Qué hace:** Detecta cuándo el lavavajillas termina su ciclo y muestra luz verde.
- **Detección inicio:** Consumo > 25W durante 30 segundos
- **Detección fin:** Consumo < 6W durante 12 minutos
- **Color:** Verde fijo (5 minutos)
- **Notificación:** Al finalizar el ciclo
- **Tiempo máximo:** 8 horas (después se cancela)

### 6. 👕 **Lavadora (washing_machine.yaml)**
**Qué hace:** Detecta cuándo la lavadora termina su ciclo y muestra luz verde.
- **Detección inicio:** Consumo > 12W durante 20 segundos
- **Detección fin:** Consumo < 4W durante 4 minutos
- **Color:** Verde fijo (5 minutos)
- **Notificación:** Al finalizar el ciclo
- **Tiempo máximo:** 6 horas (después se cancela)

---

## 🎯 Código de Colores (Guía Rápida)

| Color | Significado | Patrón |
|-------|-------------|--------|
| 🟢 **Verde** | Electrodoméstico terminado | Fijo 5 minutos |
| ⚪ **Blanco cálido** | Timbre | Parpadeo 30 segundos |
| ⚪ **Blanco frío** | Telefonillo | Parpadeo 30 segundos |
| 🔴 **Rojo** | Puerta abierta mucho tiempo | Parpadeo 30 segundos |
| 🔵 **Azul** | Fuga de agua | Parpadeo 30 segundos |

---

## 📦 Requisitos Previos

### Hardware necesario:
1. **Home Assistant Green** (o cualquier instalación de Home Assistant)
2. **Luces inteligentes** compatibles con Home Assistant (Philips Hue, IKEA, etc.)
3. **Sensores** según los blueprints que quieras usar:
   - Sensor de potencia (enchufe inteligente) para lavadora/lavavajillas
   - Sensor de puerta/ventana para puerta abierta
   - Sensor de fuga de agua
   - Sensor de timbre
   - Sensor de telefonillo

### Software necesario:
- Home Assistant instalado y funcionando
- Aplicación móvil de Home Assistant en tu teléfono

---

## 🚀 Instalación

### Paso 1: Importar Blueprints

Hay dos formas de importar los blueprints:

#### Opción A: Importación Manual (Recomendada)
1. Abre Home Assistant
2. Ve a **Configuración** → **Automatizaciones y Escenas** → **Blueprints**
3. Haz clic en **"Importar Blueprint"** (botón azul abajo a la derecha)
4. En "URL del Blueprint", pega la ruta del archivo o sube el archivo `.yaml`
5. Repite para cada uno de los 6 blueprints

#### Opción B: Copia Directa
1. Accede a tu Home Assistant por SSH o File Editor
2. Navega a la carpeta: `/config/blueprints/automation/`
3. Crea una carpeta llamada `alertas_visuales`
4. Copia todos los archivos `.yaml` en esa carpeta
5. Reinicia Home Assistant

### Paso 2: Crear Automatizaciones

Para cada blueprint que quieras usar:

1. Ve a **Configuración** → **Automatizaciones y Escenas**
2. Haz clic en **"Crear Automatización"**
3. Selecciona **"Usar Blueprint"**
4. Elige el blueprint que quieres configurar (ej: "Timbre")
5. Completa los 3 campos requeridos:

   **Campo 1: Sensor**
   - Selecciona el sensor correspondiente (ej: sensor del timbre)
   
   **Campo 2: Luces afectadas**
   - Selecciona las luces que quieres que se activen
   - Puedes elegir una o múltiples luces
   - Recomendación: usa luces en zonas comunes donde las veas frecuentemente
   
   **Campo 3: Notificación al móvil**
   - Selecciona `notify.mobile_app_tu_telefono`
   - Si no aparece, instala primero la app de Home Assistant en tu móvil

6. Haz clic en **"Guardar"**
7. Dale un nombre descriptivo (ej: "Alerta Visual - Timbre")

### Paso 3: Probar las Automatizaciones

Para cada automatización creada:

1. Ve a **Configuración** → **Automatizaciones y Escenas**
2. Encuentra tu automatización
3. Haz clic en los **tres puntos** (⋮) → **"Ejecutar"**
4. Verifica que:
   - Las luces se encienden con el color correcto
   - Recibes la notificación en el móvil
   - Las luces se apagan después del tiempo indicado

---

## ⚙️ Configuración Avanzada (Opcional)

### Ajustar Umbrales de Potencia

Si los electrodomésticos no se detectan correctamente, puedes ajustar los valores:

**Para Lavavajillas:**
```yaml
# En dishwasher.yaml, líneas 27-28
above: 25  # Cambiar si tu lavavajillas usa más/menos potencia
for:
  seconds: 30
```

**Para Lavadora:**
```yaml
# En washing_machine.yaml, líneas 27-28
above: 12  # Cambiar si tu lavadora usa más/menos potencia
for:
  seconds: 20
```

### Cambiar Duración de Alertas

Para modificar cuánto tiempo parpadean las luces:

```yaml
# En cualquier blueprint con parpadeo
- repeat:
    count: 30  # Cambiar este número (30 = 30 segundos)
```

### Cambiar Colores

Si quieres personalizar los colores:

```yaml
# Para RGB (rojo, verde, azul):
rgb_color: [255, 0, 0]  # Rojo
rgb_color: [0, 255, 0]  # Verde
rgb_color: [0, 80, 255] # Azul

# Para temperatura de color:
kelvin: 2700  # Blanco cálido
kelvin: 6500  # Blanco frío
```

---

## 🔧 Solución de Problemas

### Las luces no se encienden
- ✅ Verifica que las luces están encendidas y conectadas
- ✅ Comprueba que has seleccionado las luces correctas en el blueprint
- ✅ Prueba manualmente encendiendo las luces desde Home Assistant

### No recibo notificaciones
- ✅ Instala la app de Home Assistant en tu móvil
- ✅ Activa las notificaciones en los ajustes del teléfono
- ✅ Verifica que has seleccionado el servicio correcto (`notify.mobile_app_...`)

### La lavadora/lavavajillas no se detecta
- ✅ Revisa que el sensor de potencia funciona correctamente
- ✅ Observa el consumo real del electrodoméstico en Home Assistant
- ✅ Ajusta los umbrales de potencia si es necesario

### Las alertas se activan demasiado pronto/tarde
- ✅ Revisa los tiempos de espera en cada blueprint
- ✅ Ajusta los valores según tu caso particular

### Las luces quedan encendidas
- ✅ Esto es normal: después de la alerta, las luces se encienden brevemente (1 segundo) antes de apagarse
- ✅ Es para confirmar que la automatización ha terminado correctamente

---

## 📝 Notas Técnicas

### Timeouts
Los electrodomésticos tienen timeouts de seguridad:
- **Lavavajillas:** 8 horas máximo
- **Lavadora:** 6 horas máximo
- Si no terminan en ese tiempo, la automatización se cancela silenciosamente

### Reset de Luces
Al final de cada alerta, las luces:
1. Se encienden brevemente en blanco cálido (2700K)
2. Se apagan después de 1 segundo
3. Esto confirma que la automatización ha terminado

---

## 📄 Licencia

Este proyecto es de código abierto. Siéntete libre de modificar y compartir los blueprints según tus necesidades.

---

## ✨ Créditos

Blueprints diseñados para facilitar la vida de personas sordas mediante alertas visuales claras y efectivas en Home Assistant.

**Versión:** 1.0  
**Última actualización:** Enero 2026  
**Compatible con:** Home Assistant 2024.1 y superior

---

**¡Disfruta de tu hogar inteligente más accesible! 🏠✨**
