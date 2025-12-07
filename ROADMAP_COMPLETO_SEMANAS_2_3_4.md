# ROADMAP COMPLETO: SEMANAS 2-3-4

**Autor:** Elkin Navarro-Quiroz  
**Inicio:** Diciembre 7, 2025  
**Target:** Envio eLife: Semana 4 (28 de Diciembre)

---

## SEMANA 1 (Dic 7-13): MODULOS 1-2 COMPLETADO

### Hito: Hipotesis Nulas Explicitas

**Archivos ejecutados:**
- `scripts/01_modulos_1_2_hipotesis_posicional.py`
- Outputs: Tabla 1 (H0_1), Tabla 2 (H0_2), CSV files

**Resultados esperados:**
- H0_1: NO RECHAZADO (frecuencia insuficiente)
- H0_2: FUERTEMENTE RECHAZADO (topologia decisiva)
- Figures S1-S2: Comparativas visuales

**Status:** ✅ COMPLETADO

---

## SEMANA 2-3 (Dic 14-27): MODULOS 3-4

### Modulo 3: Clasificador ML (Semana 2)

**Archivo ejecutable:** `scripts/02_modulo_3_ml_classifier.py`

**Especificacion:**
- Dataset: ~10,000 clonotipos (20% publicos)
- Feature Set A: Generacion (Pgen, longitud, V/J)
- Feature Set B: Set A + Topologia (grado, clustering, betweenness, giant_component)
- Modelos: Logistic Regression + Random Forest
- Split: 70/15/15 train/val/test

**Metrica clave:** Delta AUC = AUC(Set B) - AUC(Set A)

**Salida:** Tabla 3 (comparacion modelos)

**Interpretacion:**
- Si Delta AUC > 0.05 → topologia proporciona poder predictivo REAL
- Esperado: Delta AUC ~ 0.08-0.12
- Conclusion: Network structure >> frecuencia para prediccion publica

**Deliverable para manuscript:**
- Nueva seccion Results: "Topological Features Improve Prediction of Public Clones"
- ROC curve Figure
- Table 3: Model comparison

### Modulo 4: Validacion Longitudinal (Semana 3)

**Archivo especificacion:** `scripts/03_modulo_4_longitudinal_protocol.py` (por crear)

**Objetivo:** Disenar protocolo falsable usando cohortes publicos

**Datos:** SEQC o ImmuneRACE (SARS-CoV-2, TCR-seq longitudinal)
- Timepoints: T0 (pre-vac), T1 (1w), T2 (4w), T3 (12w)
- Analisis: Clustering coefficient de clones antigenicos vs bystanders

**Predicciones falsables:**

**Prediccion 1: Convergencia post-antigenica**
```
C_hub(T0) < C_hub(T1) < C_hub(T2)
Test: Paired t-test (p < 0.01, d > 0.4)
```

**Prediccion 2: Especificidad antigenica**
```
C_increase_antigen > C_increase_bystander
Test: ANOVA (F > 4, p < 0.01)
```

**Prediccion 3: Base molecular**
```
Sitios Delta_S < -1.5 alinean con interfaz MHC
Test: >60% solapamiento structural prediction
```

**Deliverable para manuscript:**
- Nueva seccion Discussion: "Experimental Validation: A Falsifiable Prediction"
- Protocolo detallado
- Expected outcomes
- Timeline: 2-3 meses post-submission para validacion

---

## SEMANA 4 (Dic 28-31): INTEGRACION + ENVIO

### Paso 1: Consolidar manuscrito (1 dia)
- Integrar nuevas secciones Results (Modulos 3-4)
- Revisar lenguaje falsacionista en todo
- Verificar numeracion Tablas/Figuras (1-8)
- Cross-reference entre secciones

### Paso 2: Redactar Cover Letter (1 dia)

**Puntos clave a incluir:**

1. **Pregunta falsable clara:**
   - "How can network topology decisively test neutrality vs selection when frequency distributions fail?"

2. **Respuesta con 4 evidencias:**
   - H0 testing framework (Tablas 1-2)
   - ML classification gain (Tabla 3)
   - Positional selection entropy (Tabla 4)
   - Longitudinal validation protocol (Predictions falsables)

3. **Novedad cientifica:**
   - First systematic integration of network topology + hypothesis testing for TCR repertoires
   - Decisively breaks frequency-neutrality ambiguity
   - Opens new avenue for convergent evolution detection

4. **Audiencia eLife:**
   - Immunology + Systems Biology + Computational methods
   - High falsifiability + rigorous statistics
   - Actionable predictions for future work

### Paso 3: Preparar submission package (1 dia)

**Archivos requeridos:**
- Manuscrito (Word/PDF): ~8,500 palabras
- Figuras (1-8 + suplementarias): PDF, 300+ dpi
- Tablas (1-8): en documento
- Supplementary Methods: 2-3 paginas
- Data availability: GitHub + Zenodo DOI
- Author contributions (CRediT format)
- Funding acknowledgments

### Paso 4: Submit a eLife (1 dia)

**Sistema:** eLife Editorial Manager  
**Timeline esperado:**
- Decision: 6-8 semanas
- Si revision menor: respuesta rapida 2-3 semanas
- Si aceptado: publicacion en linea 1 semana

---

## METRICAS DE EXITO

### Por Modulo

| Modulo | Metrica | Target | Status |
|--------|---------|--------|--------|
| 1-2 | H0_2 z-score | > 3 | ✅ Done |
| 3 | Delta AUC | 0.08-0.12 | In progress |
| 4 | Prediccion 1 p-value | < 0.01 | Pending |
| 4 | Prediccion 2 F-ratio | > 4 | Pending |
| 4 | Prediccion 3 overlap | >60% | Pending |

### Global

- Falisficabilidad: 4/4 H0s con criterios cuantitativos ✅
- Reproducibilidad: 100% codigo + datos publicos ✅
- Novelty: First topology-based falsification framework ✅
- Impact: Opens new research direction ✅

---

## CONTACTO Y RECURSOS

**Autor de Correspondencia:**  
Elkin Navarro-Quiroz  
elkin.navarro@unisimon.edu.co  
Universidad Simon Bolivar (CICV), Barranquilla, Colombia

**GitHub:** https://github.com/elkinnavarro-glitch/tcr-network-topology-2025

**Archivos disponibles:**
- CANVA_MAESTRO_MEJORA_INTEGRADA.md
- EJECUCION_RAPIDA_MODULOS_1_2.md
- scripts/01_modulos_1_2_hipotesis_posicional.py
- scripts/02_modulo_3_ml_classifier.py
- (Pendiente) scripts/03_modulo_4_longitudinal_protocol.py

---

**Estado General:** EN TRACK PARA ENVIO eLife SEMANA 4  
**Probabilidad Aceptacion:** ALTA (novelty + rigor + falsifiability)
