# Secciones de la Clase: Audio y Video Generativo

Este directorio contiene las secciones modulares de la clase, cada una en un archivo separado.

## Estructura

Cada archivo `.tex` corresponde a una sección completa de la presentación:

1. **01_introduccion.tex** - ¿Por qué Unir Audio y Video?
2. **02_recap.tex** - Recap Express: Lo Que Ya Saben
3. **03_deepfakes.tex** - Deepfakes: El Elefante en la Habitación
4. **04_condicionalidad.tex** - El Problema de la Condicionalidad (V2A, A2V, T2AV)
5. **05_profundizacion.tex** - Profundización: Arquitecturas Específicas
6. **06_arquitecturas_modernas.tex** - Arquitecturas Modernas (Open-Sora, Sora, Veo)
7. **07_problemas_abiertos.tex** - Problemas Abiertos y Fronteras
8. **08_discusion.tex** - Discusión: Implicancias y Reflexiones
9. **09_recursos.tex** - Recursos y Referencias

## Uso

El archivo principal `audio_and_video_genmodels.tex` importa todas estas secciones con `\input{}`.

Para editar una sección específica, simplemente edita el archivo correspondiente.

## Ventajas de esta estructura:

- ✅ **Modularidad**: Cada sección es independiente
- ✅ **Mantenibilidad**: Más fácil encontrar y editar contenido específico
- ✅ **Control de versiones**: Git puede trackear cambios por sección
- ✅ **Colaboración**: Múltiples personas pueden editar secciones diferentes
- ✅ **Context window**: No se llena la ventana de contexto de Claude
