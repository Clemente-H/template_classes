# Clase 2: Entrenamiento de LLMs - Infraestructura y Tips

## Descripción
Clase teórica de 1.5 horas sobre infraestructura y técnicas de optimización para entrenar y deployar LLMs.

## Estructura de Archivos

```
clase2/
├── train_and_infra_llms.tex          # Archivo principal que importa todas las secciones
├── sections/                          # Secciones individuales de la clase
│   ├── 01_introduccion.tex           # Hardware vs Software, motivación (101 líneas)
│   ├── 02_hardware_recursos.tex      # GPUs, VRAM, cálculos de memoria (319 líneas)
│   ├── 03_tecnicas_optimizacion.tex  # Quantization, LoRA, QLoRA (341 líneas)
│   ├── 04_deployment.tex             # vLLM, TGI, conceptos de serving (316 líneas)
│   └── 05_recapitulacion.tex         # Resumen y mensajes clave (130 líneas)
└── drafts_and_context/               # Material de referencia
    ├── guia_clase_teorica.md         # Guía detallada de la clase con timings
    ├── NOTA_IMAGENES.md              # Instrucciones para copiar imágenes
    ├── 3-Efficiency&DeploymentGENAI (1).tex  # Material de referencia original
    ├── diapo1.png - diapo6.png       # Imágenes adicionales de referencia
    └── resumen_transcripcion_colega.txt

## Contenido de la Clase (1.5 horas)

### 1. Introducción (5-7 min)
- Diferenciación Hardware vs Software
- Los 3 pasos del entrenamiento (Forward, Backward, Optimization)
- Motivación: GPT-3 costó $4.6M pero hoy es más accesible

### 2. Hardware y Recursos Computacionales (25-30 min)

#### 2.1 Fundamentos de GPUs
- Por qué GPUs y no CPUs
- Tipos de GPUs (consumer vs datacenter)
- VRAM como cuello de botella

#### 2.2 Calculando Recursos Necesarios
- Fórmula fundamental: `Memoria (GB) = (Parámetros × Bytes) / 10^9 × 1.2`
- Ejemplos con Llama 3.1 8B y 70B
- Calculadora interactiva: https://vram.asmirnov.xyz
- Componentes de memoria (weights, KV cache, activations, overhead)

#### 2.3 Training vs Inference
- Training requiere 3-4× más memoria
- Componentes: pesos, gradientes, optimizer states, activations
- Batch size y su impacto
- Visualización con memory profiler

#### 2.4 Referencias de Entrenamiento Real
- GPT-3: ~$4.6M, 355 GPU-years
- Llama 2 70B: ~1.7M GPU-hours
- Mensaje: Pre-training inaccesible, fine-tuning muy accesible

### 3. Técnicas de Optimización (35-40 min)

#### 3.1 Quantization (12-15 min)
- Concepto y niveles (FP32 → FP16 → INT8 → INT4)
- Post-Training Quantization (GPTQ, AWQ, SmoothQuant)
- Quantization-Aware Training
- Ejemplo práctico: Llama 8B en diferentes precisiones
- INT8 = "sweet spot"

#### 3.2 LoRA (12-15 min)
- Low-Rank Adaptation: aproximar matrices grandes con pequeñas
- Matemática: W = W_original + B × A
- Reducción 128× en parámetros entrenables
- Beneficios y limitaciones
- Cuándo usar LoRA

#### 3.3 QLoRA (8-10 min)
- Combinación de INT4 quantization + LoRA
- Innovaciones: NF4, double quantization, paged optimizers
- Fine-tune Llama 70B en 48GB GPU
- Democratización del fine-tuning

#### 3.4 Otras Técnicas (3-5 min)
- Pruning: estructurado vs no estructurado
- Tabla comparativa de todas las técnicas

### 4. Deployment en Producción (15-20 min)

#### 4.1 El Problema del Deployment
- Desafíos: concurrencia, memoria, batching, observabilidad
- Métricas críticas: TTFT, throughput, requests concurrentes, costo/token

#### 4.2 Bibliotecas de Serving
- **vLLM:** Líder en throughput, PagedAttention, 24× mejor que HF Transformers
- **TGI:** Integración HuggingFace, telemetría robusta
- **TensorRT-LLM:** Máximo rendimiento NVIDIA, ultra-baja latencia
- **Ollama:** Desarrollo local, muy simple

#### 4.3 Conceptos Clave
- Continuous Batching: reducción 5-10× en latencia
- PagedAttention: 2-4× más requests concurrentes
- Tensor Parallelism: dividir modelos entre GPUs

### 5. Recapitulación (5 min)
- Flujo completo: Hardware → Optimización → Deployment
- Mensajes clave
- Lo que hicimos posible (democratización)
- Recursos útiles

## Imágenes Necesarias

### Ya deberían existir en `images/GenIA/`:
- alpaca.png
- Vram_estimator.png
- lora.png
- quantization.png
- qlora.jpg

### Debes copiar desde drafts_and_context/:
1. diapo1.png → GenIA/training_3_steps.png
2. diapo5.png → GenIA/memory_profiler_training.png
3. diapo6.png → GenIA/memory_scaling_batch.png

Ver `drafts_and_context/NOTA_IMAGENES.md` para comandos de copia.

## Cómo Compilar

Desde el directorio raíz del proyecto:

```bash
cd "/Users/clemente/Documents/Work/Latex Presentaciones/template_classes"
pdflatex main.tex
```

O si usas latexmk:

```bash
latexmk -pdf main.tex
```

## Recursos Mencionados en la Clase

- VRAM Calculator: https://vram.asmirnov.xyz
- vLLM: https://github.com/vllm-project/vllm
- Hugging Face TGI: https://github.com/huggingface/text-generation-inference
- Ollama: https://ollama.ai

## Papers de Referencia

Las referencias bibliográficas están en el archivo de bibliografía del proyecto:
- LoRA (Hu et al., 2021)
- QLoRA (Dettmers et al., 2023)
- DPO (Rafailov et al., 2024)
- Constitutional AI (Anthropic)

## Notas Pedagógicas

- **Enfoque:** Bottom-up (problema → solución → matemática → ejemplo)
- **Ejemplos consistentes:** Usar Llama 3.1 8B/70B como caso recurrente
- **Trade-offs:** Siempre mostrar costos y beneficios
- **Democratización:** Enfatizar lo que ES POSIBLE con hardware limitado

## Próximos Pasos

- [ ] Copiar las 3 imágenes faltantes (ver NOTA_IMAGENES.md)
- [ ] Verificar que todas las imágenes del .tex original estén disponibles
- [ ] Compilar y revisar el PDF
- [ ] Ajustar timings según necesidad
- [ ] Preparar la sesión práctica (1.5 horas de práctica separada)
