# Clase 2: Entrenamiento de LLMs - Infraestructura y Tips

## Descripción
Clase teórica de 1.5 horas sobre infraestructura, recursos computacionales y técnicas de optimización para entrenar y deployar LLMs. **Basada en mi_plan.md** con enfoque en ejemplos concretos y flujo narrativo.

## Estructura de Archivos

```
clase2/
├── train_and_infra_llms.tex          # Archivo principal que importa secciones
├── referencias_entrenamiento.bib     # Referencias bibliográficas con datos reales
├── sections/                          # Secciones individuales (9 archivos)
│   ├── 01_intro_motivacional.tex     # Costos reales de entrenamiento (10 min)
│   ├── 02_training_vs_inference.tex  # Distinción crucial (5 min)
│   ├── 03_hardware.tex               # GPUs, VRAM, calculadora (20 min)
│   ├── 04_software_librerias.tex     # Frameworks brevemente (5 min)
│   ├── 05_ciclo_entrenamiento.tex    # Base → Instruction → Preference (10 min)
│   ├── 06_tecnicas_optimizacion.tex  # LoRA, Quantization, QLoRA (30 min)
│   ├── 07_evaluaciones.tex           # MMLU, MT-Bench, leaderboards (5 min)
│   ├── 08_deployment_recursos.tex    # vLLM, herramientas (10 min)
│   └── 09_cierre.tex                 # Resumen, próximo lab (5 min)
└── drafts_and_context/
    ├── mi_plan.md                    # Plan original del usuario
    ├── guia_clase_teorica.md         # Guía anterior (referencia)
    └── NOTA_IMAGENES.md              # Instrucciones para imágenes

## Contenido de la Clase (1.5 horas) - Basado en mi_plan.md

### 1. Introducción Motivacional (10 min)
**Objetivo:** Mostrar ejemplos concretos de costos de entrenamiento

#### Modelos Grandes (Como referencia):
- **GPT-3 (175B):** $1.1M - $4.6M, 355 GPU-years V100
- **Llama 3.3 70B:** 7.0M GPU-hours H100
- **OLMo 3 32B:** $2.75M, 1.05M GPU-hours H100

#### Modelos Eficientes (No es la verdad absoluta):
- **DeepSeek-V3 (671B MoE):** $5.5M, 2.788M GPU-hours (11× más eficiente que Llama)
- **Mixtral 8x7B:** MoE, eficiencia de 12.9B con 45B params

#### Modelos Pequeños (Más accesibles):
- **Qwen 2.5 1.5B:** Pre-entrenado en 18T tokens
- **Falcon3 7B:** 14T tokens, 1,024 H100

**Todas las referencias están en referencias_entrenamiento.bib con links a fuentes**

### 2. Training ≠ Inference (5 min)
**ANTES de hablar de hardware**

- Distinción crucial: Forward vs Forward+Backward+Optimization
- Training requiere 3-4× más memoria
- Componentes: Weights, Gradients, Optimizer States, Activations
- KV Cache (inference) vs Activations (training)

### 3. Hardware (20 min)

#### GPUs y VRAM:
- VRAM = cuello de botella
- Fórmula de cálculo: `Memoria = (Params × Bytes) / 10^9 × 1.2`
- Calculadora interactiva: https://vram.asmirnov.xyz

#### Visualizaciones:
- Memory profiler durante training (diapo5.png → memory_profiler_training.png)
- Escalamiento con batch size (diapo6.png → memory_scaling_batch.png)

#### Comunicación:
- Tensor Parallelism brevemente
- Inter-GPU e intra-GPU
- "Es un culo" (costosa)

### 4. Software y Librerías (5 min)
**Solo mencionar, no profundizar**

- PyTorch, Accelerate, DeepSpeed, NeMo, SageMaker
- Trade-offs: control vs facilidad
- Nos aprovechamos de estas librerías

### 5. Ciclo de Entrenamiento Común (10 min)
**Usar imagen del paper OLMo del flujo**

#### Tres Fases:
1. **Base Pre-training:** 6-15T tokens, millones $, inaccesible
2. **Instruction Tuning (SFT):** Miles ejemplos, accesible
3. **Preference Alignment (DPO/RLHF):** Comparaciones, accesible

#### Tabla comparativa:
- Datos necesarios
- GPU hours
- Costo
- Accesibilidad

**Mensaje:** Pre-training = solo grandes labs, Fine-tuning = muy accesible

### 6. Técnicas de Optimización (30 min)
**La sección más importante**

#### LoRA (Low-Rank Adaptation):
- Reduce parámetros entrenables 100×
- Matemática: W = W_original + B × A
- Ejemplo: 4096×4096 → 16×8192 = 128× reducción
- Imagen: GenIA/lora.png

#### Quantization:
- FP32 → FP16 → INT8 → INT4
- INT8 = sweet spot
- Ejemplo: Llama 8B (19.2GB → 9.6GB → 4.8GB)
- Imagen: GenIA/quantization.png

#### QLoRA:
- Combinación perfecta: INT4 + LoRA
- Fine-tune Llama 70B en 48GB GPU
- Democratización: $10k+ → $100-200
- Imagen: GenIA/qlora.jpg
- Innovaciones: NF4, double quantization, paged optimizers

### 7. Evaluaciones (5 min)
**Breve, no profundizar**

- MMLU, MT-Bench, HumanEval
- Leaderboards: Hugging Face, Chatbot Arena
- Placeholder para screenshot de leaderboard (usuario lo proporcionará)
- Mensaje: Usar benchmarks como referencia, evaluar en tu caso de uso

### 8. Deployment y Recursos (10 min)

#### vLLM:
- Estándar de facto
- PagedAttention, Continuous Batching
- 24× mejor throughput

#### Otras herramientas:
- TGI, TensorRT-LLM, Ollama
- Hugging Face Hub, Axolotl, Unsloth

### 9. Cierre (5 min)
- Resumen de todo
- Mensajes clave
- Lo que NO hablamos
- Próximo: Lab Práctico

## Datos Reales y Referencias

### Archivo referencias_entrenamiento.bib
Contiene TODOS los datos con fuentes verificadas:

**Modelos con costos documentados:**
- GPT-3: $1.1M - $4.6M \[gpt3_cost_epoch, gpt3_cost_lambda\]
- Llama 3.3: 7M GPU-hours \[llama33_training\]
- OLMo 3: $2.75M, 1.05M GPU-hours \[olmo3_cost\]
- DeepSeek-V3: $5.5M, 2.788M GPU-hours \[deepseek_v3_technical\]

**Modelos sin costos públicos:**
- Mixtral 8x7B: Arquitectura documentada, costo no público
- Qwen 2.5 1.5B: Dataset (18T tokens) documentado, costo no público
- Falcon3 7B: 14T tokens, 1,024 H100, costo no público

**TODOS los links están en el .bib - NO hay valores inventados**

## Imágenes Necesarias

### Ya deberían existir en images/GenIA/:
- lora.png (arquitectura LoRA)
- quantization.png (visualización niveles)
- qlora.jpg (arquitectura QLoRA)
- Vram_estimator.png (screenshot calculadora)

### Debes copiar/crear:
1. **diapo1.png → GenIA/training_3_steps.png**
   - Diagrama Forward/Backward/Optimization
   - Usado en: 02_training_vs_inference.tex

2. **diapo5.png → GenIA/memory_profiler_training.png**
   - Memory profiler PyTorch de Llama 1B
   - Usado en: 03_hardware.tex

3. **diapo6.png → GenIA/memory_scaling_batch.png**
   - Escalamiento memoria con batch size
   - Usado en: 03_hardware.tex

### Usuario proporcionará:
4. **Imagen del ciclo OLMo** (base → instruction → preference)
   - Placeholder en: 05_ciclo_entrenamiento.tex
   - Guardar como: GenIA/olmo_training_cycle.png

5. **Screenshot de leaderboard**
   - Placeholder en: 07_evaluaciones.tex
   - Guardar como: GenIA/llm_leaderboard.png

### Imágenes con logos (opcionales):
- Logos de OpenAI, Meta, AI2 para tabla comparativa
- Logos de Alibaba, TII para modelos pequeños

## Cómo Compilar

```bash
cd "/Users/clemente/Documents/Work/Latex Presentaciones/template_classes"
pdflatex main.tex
bibtex main  # Para incluir referencias
pdflatex main.tex
pdflatex main.tex
```

O con latexmk:
```bash
latexmk -pdf main.tex
```

## Diferencias con la Versión Anterior

### Nuevo enfoque (basado en mi_plan.md):
✅ **Más visual:** Empieza con tabla comparativa de costos reales
✅ **Mejor flujo:** Training ≠ Inference ANTES de hardware
✅ **Más completo:** Incluye ciclo completo (base → instruction → preference)
✅ **Más práctico:** Enfoque en "qué queremos hacer"
✅ **Incluye evaluaciones:** MMLU, MT-Bench, leaderboards
✅ **Datos reales:** Todas las referencias verificadas y documentadas

### Qué se mantuvo:
- Técnicas de optimización (LoRA, Quantization, QLoRA) - bien explicadas
- Deployment con vLLM - sigue siendo relevante
- Imágenes de arquitecturas (lora.png, qlora.jpg, quantization.png)

## Próximos Pasos

- [ ] Copiar las 3 imágenes de diapos (ver arriba)
- [ ] Buscar y agregar imagen del ciclo OLMo
- [ ] Buscar y agregar screenshot de leaderboard
- [ ] Opcional: Agregar logos de compañías
- [ ] Compilar y verificar que todas las referencias funcionen
- [ ] Revisar timing (debería ser ~90 min)
- [ ] Preparar lab práctico (fine-tuning con QLoRA)

## Notas Pedagógicas

- **Enfoque:** Ejemplos concretos primero, luego teoría
- **Progresión:** Grande → eficiente → pequeño (para modelos)
- **Mensaje central:** Fine-tuning es ACCESIBLE con técnicas modernas
- **Trade-offs:** Siempre mostrar costos y beneficios
- **Prohibido:** Inventar datos - todas las cifras están referenciadas

## Referencias en el .bib

El archivo `referencias_entrenamiento.bib` contiene 17 referencias con:
- Costos de entrenamiento documentados
- GPU hours de modelos específicos
- Links a fuentes originales (papers, blogs oficiales, technical reports)
- Notas con datos específicos extraídos

**Formato de cita en slides:** `\cite{clave_referencia}`
