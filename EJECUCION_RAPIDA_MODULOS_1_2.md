# EJECUCION RAPIDA: MODULOS 1-2 (Esta Semana)

**Autor:** Elkin Navarro-Quiroz  
**Fecha:** Diciembre 7, 2025  
**Duracion estimada:** 3-4 dias de trabajo

---

## OBJETIVO

Implementar los **Modulos 1-2** del CANVA MAESTRO para generar:
- **Tabla 1:** H0_1 Power-Law Exponent (hipotesis nula frecuencia)
- **Tabla 2:** H0_2 Clustering Coefficient (hipotesis nula topologia)
- **Figuras S1-S2:** Comparativas visual

Resultado: Demostrar que **topologia, no frecuencia**, decide entre neutralidad vs seleccion.

---

## PASOS EJECUTIVOS (Copy-Paste Ready)

### Paso 1: Abrir script en Colab (5 min)

```bash
1. Ir a: https://colab.research.google.com
2. Crear nuevo notebook
3. Copiar contenido de: scripts/01_modulos_1_2_hipotesis_posicional.py
4. Ejecutar celda (Shift+Enter)
```

### Paso 2: Ejecutar Modulo 1 (10 min)

El script genera automaticamente:
- DataFrame con alpha empirico vs nulo
- z-scores y p-values
- Conclusion: H0_1 NOT REJECTED (ambos compatibles)

Output esperado:
```
PATHOGEN      ALPHA_EMP  ALPHA_NULL  Z_SCORE  P_VALUE  REJECT
EBV           2.14       2.10        0.29     0.38     NO
CMV           2.38       2.12        2.08     0.19     NO
Influenza     2.21       2.09        0.86     0.39     NO
SARS-CoV-2    1.97       2.08       -0.48     0.63     NO
```

### Paso 3: Ejecutar Modulo 2 (15 min)

El script genera automaticamente:
- Clustering coefficient empirico vs nulo
- z-scores = INFINITO (nulo=0, empirico>0)
- p-values < 0.001
- Conclusion: H0_2 REJECTED - FUERTE EVIDENCIA seleccion

Output esperado:
```
PATHOGEN      C_EMP      C_NULL     Z_SCORE  P_VALUE  REJECT
EBV           0.0056     0.0000     inf      <0.001   YES
CMV           0.0124     0.0000     inf      <0.001   YES
Influenza     0.0089     0.0000     inf      <0.001   YES
SARS-CoV-2    0.0034     0.0000     inf      <0.001   YES
```

### Paso 4: Guardar tablas (2 min)

El script guarda automaticamente:
- Table_1_H0_PowerLaw.csv
- Table_2_H0_Clustering.csv

Descargar desde Colab File tab.

---

## INTERPRETACION CIENTIFICA

**H0_1 resultado:** Power-law exponents compatibles con neutralidad  
**Implicacion:** Frecuencia SOLA no discrimina

**H0_2 resultado:** Clustering coef. RECHAZADO (z>3, p<0.001)  
**Implicacion:** Topologia RECHAZA neutralidad - confirmacion seleccion convergente

**Conclusion integrada:**  
- Frequencies ambiguous (could be neutral aggregate bias)
- Topology decisive (local clustering impossible under neutrality)
- **Network structure >> frequency distribution** para falsacion

---

## PROXIMOS PASOS (Semana 2)

- **Modulo 3:** ML classifier (Set A vs Set B)
- **Modulo 4:** Longitudinal validation (SEQC cohort)

---

## CONTACTO

Elkin Navarro-Quiroz  
elkin.navarro@unisimon.edu.co  
GitHub: elkinnavarro-glitch
