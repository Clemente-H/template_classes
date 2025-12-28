# Modelos Generativos de Audio y Video
## Diplomado CENIA - [Tu nombre]

---

## 1. Introducción: ¿Por qué unir audio y video?

Hasta ahora vieron audio y video como mundos separados. Pero en la realidad, nunca los percibimos así.

**El problema fundamental:** Los humanos esperamos coherencia audiovisual. Un video sin audio coherente se siente incompleto, y un audio desincronizado es inmediatamente perturbador.

**El desafío técnico:** Dos modalidades con características muy distintas:
- Audio: señal 1D, alta densidad temporal (24kHz = 24,000 samples/seg)
- Video: señal 3D (alto × ancho × tiempo), menor frecuencia temporal (24-60 fps)

¿Cómo los alineamos? ¿Cómo los generamos juntos?

---

## 2. Recap Express: Lo que ya saben

### Audio (lo esencial)
- **Señal cruda:** amplitud, frecuencia, fase
- **Espectrogramas:** representación tiempo-frecuencia que permite tratar audio "como imagen"
- **El problema de la dimensionalidad:** 1 segundo = 24,000 valores
- **Soluciones modernas:** neural codecs (EnCodec), tokenización para LLMs

### Video (lo esencial)
- **Secuencia de frames:** el video es un tensor 4D (batch × tiempo × alto × ancho × canales)
- **Consistencia temporal:** el gran desafío — mantener coherencia entre frames
- **Representaciones latentes:** VQ-VAE, codebooks para discretizar video

### La conexión
En ambos casos, la comunidad convergió hacia:
1. **Comprimir** a un espacio latente (encoders)
2. **Modelar** en ese espacio comprimido (transformers, difusión)
3. **Decodificar** de vuelta a la señal original

---

## 3. Deepfakes: El elefante en la habitación

### ¿Qué son realmente?
Los deepfakes fueron el primer caso masivo de generación audio-video condicionada. Recordemos "Synthesizing Obama" que vieron en la clase de video.

### La evolución
- **Primera generación:** Audio → movimiento de labios (lip sync)
- **Segunda generación:** Face swapping + voice cloning separados
- **Generación actual:** Sistemas end-to-end que generan persona completa

### El problema ético (ya lo discutieron, pero vale reforzar)
- Desinformación política
- Fraude por suplantación
- Contenido no consensuado
- La carrera armamentista: generación vs detección

---

## 4. El Problema de la Condicionalidad

Esta es la pregunta central de la clase: **¿Cómo unimos audio y video?**

### Estrategias de condicionamiento

#### 4.1 Video → Audio (V2A)
Dado un video, generar el audio correspondiente.

**Aplicaciones:**
- Foley automático (efectos de sonido)
- Sonorización de películas mudas
- Accesibilidad

**Desafíos:**
- Sincronización temporal precisa
- Entender qué objetos producen qué sonidos
- Ambiente vs acciones puntuales

**Modelos relevantes:**
- V2A de DeepMind (https://deepmind.google/blog/generating-audio-for-video/)
- Sistemas de Foley automático

#### 4.2 Audio → Video (A2V)
Dado un audio, generar video coherente.

**Aplicaciones:**
- Talking heads / avatares virtuales
- Visualización de música
- Asistentes virtuales

**Desafíos:**
- El audio tiene menos información que el video (problema ill-posed)
- Múltiples videos válidos para un mismo audio
- Consistencia de identidad

**Modelos relevantes:**
- Sistemas de lip-sync
- Generación de avatares

#### 4.3 Texto → Audio + Video (T2AV)
Generación conjunta desde descripción textual.

**El santo grial actual.** Es lo que hacen Sora, Veo3, etc.

**Desafíos:**
- Mantener coherencia cross-modal
- El texto es ambiguo respecto al timing
- Calidad en ambas modalidades simultáneamente

---

## 5. Arquitecturas Modernas: Cómo resuelven estos problemas

### 5.1 Open-Sora (HPC-AI Tech)
Paper: https://arxiv.org/pdf/2412.20404

**¿Por qué es relevante?**
- Es open-source (pueden experimentar)
- Documenta las decisiones arquitectónicas que los sistemas cerrados no revelan

**Componentes clave:**
- Diffusion Transformer (DiT) para video
- Integración de condicionamiento temporal
- Estrategias de entrenamiento multi-escala

**Lo que resuelve de los problemas clásicos:**
- Consistencia temporal larga (attention sobre secuencias)
- Escalabilidad (entrenamiento progresivo)
- Eficiencia (latent diffusion)

### 5.2 Sistemas Propietarios: Sora, Veo3, Kling

**Lo que sabemos (y lo que no):**
- Probablemente DiT-based
- Entrenamiento en datasets masivos propietarios
- Generación de audio nativa (no post-procesado)

**La brecha open vs closed:**
- Calidad de datos de entrenamiento
- Compute disponible
- Técnicas de fine-tuning no publicadas

### 5.3 Modelos Especializados

#### Mirelo (https://www.mirelo.ai)
[Investigar y completar - revisar qué hace específicamente]

---

## 6. Problemas Abiertos y Fronteras

### Problemas técnicos no resueltos
1. **Sincronización fina:** Los labios aún se desincronizan en casos complejos
2. **Física del sonido:** Los modelos no entienden acústica real (reverberación, distancia)
3. **Consistencia de identidad:** En videos largos, los personajes "derivan"
4. **Edición coherente:** Modificar una modalidad sin romper la otra

### Direcciones de investigación
1. **World models audiovisuales:** Entender física, no solo estadísticas
2. **Representaciones unificadas:** Un solo espacio latente para audio y video
3. **Generación interactiva:** Sistemas que respondan en tiempo real

### El futuro cercano
- Avatares virtuales indistinguibles
- Doblaje automático con lip-sync perfecto
- Creación de contenido "completo" desde texto

---

## 7. Discusión: Implicancias

### Técnicas
- ¿Llegamos al límite de escalar transformers?
- ¿Los modelos entienden o solo memorizan?

### Éticas
- ¿Cómo manejamos la autenticidad del contenido?
- ¿Quién es responsable del mal uso?
- ¿Deberíamos watermarkear todo contenido generado?

### Sociales
- El futuro del trabajo creativo
- Acceso democratizado vs concentración de poder en labs

---

## 8. Recursos y Referencias

### Papers fundamentales
- Open-Sora: https://arxiv.org/pdf/2412.20404
- V2A DeepMind: https://deepmind.google/blog/generating-audio-for-video/

### Repos para experimentar
- Open-Sora: https://huggingface.co/hpcai-tech/Open-Sora
- [Agregar más recursos prácticos]

### Para profundizar
- [Agregar lecturas adicionales]

---

## Notas para el lab práctico (próxima sesión)
[Pendiente - lo definimos después]

---

*Nota: Este documento es un índice de trabajo. Expandir secciones según el tiempo disponible para la clase.*
