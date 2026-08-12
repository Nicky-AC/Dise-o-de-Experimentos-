[README.md](https://github.com/user-attachments/files/30984904/README.md)
# Análisis del IMC en Función del Programa Académico y la Edad en Estudiantes de la Universidad de Cartagena

**Autoras:** Sharon Nicole Acosta Caraballo, María José Ibarra Ariña
**Profesora:** Luz Elena Vargas Ortiz
**Institución:** Universidad de Cartagena — Diseño de Experimentos
**Fecha:** 5 de diciembre de 2025

## Descripción

Este trabajo analiza si el Índice de Masa Corporal (IMC) de estudiantes universitarios varía según tres factores: **programa académico** (Matemáticas, Biología, Química), **género** (Femenino, Masculino) y **grupo de edad** (17–19, 20–22, 23–31 años). Se utiliza un **diseño factorial completo 3×2×3** analizado mediante **ANOVA de tres vías** en R.

## Población y muestra

- **60 estudiantes**, muestreo por conveniencia.
- 20 estudiantes por programa académico.
- 10 estudiantes de cada género por programa.
- 18 combinaciones posibles de factores (3 × 2 × 3).

## Variables

| Tipo | Variable | Descripción |
|---|---|---|
| Respuesta | IMC | Peso (kg) / Estatura (m)² |
| Factor | Programa académico | Matemáticas, Biología, Química |
| Factor | Género | Femenino, Masculino |
| Factor | Grupo de edad | 17–19, 20–22, 23–31 años |
| Auxiliar | Peso, Estatura, Edad | Usadas para calcular el IMC y el grupo etario |

## Metodología / Herramientas

Análisis realizado en **R** con las librerías: `modeest`, `moments`, `readxl`, `dplyr`, `ggplot2`, `car`, `agricolae`, `PMCMRplus`.

Modelo ajustado:
```r
Modelo <- aov(IMC ~ Programa * Genero * GrupoEdad, data = CienciasExactasIMC)
```

### Verificación de supuestos del modelo

| Supuesto | Prueba | Resultado | Conclusión |
|---|---|---|---|
| Normalidad | Shapiro-Wilk | W = 0.9791, p = 0.3925 | No se rechaza H0 → residuos normales |
| Independencia | Durbin-Watson | DW = 2.2983, p = 0.868 | No se rechaza H0 → errores independientes |
| Homogeneidad de varianzas | Levene | F = 1.2476, p = 0.2738 | No se rechaza H0 → homocedasticidad |

Todos los supuestos se cumplen, por lo que el ANOVA es válido.

## Resultados del ANOVA

| Fuente | p-valor | Significativo (α=0.05) |
|---|---|---|
| Programa | 0.4876 | No |
| Género | 0.0686 | Cercano (tendencia) |
| **Grupo de edad** | **0.000121** | **Sí (***) |
| Programa × Género | 0.7995 | No |
| **Programa × Grupo de edad** | **0.0095** | **Sí (**)** |
| Género × Grupo de edad | 0.8608 | No |
| **Programa × Género × Grupo de edad** | **0.0267** | **Sí (*)** |

## Comparaciones múltiples (Tukey HSD)

- **Grupo de edad:** 23–31 años tiene un IMC significativamente mayor que 17–19 años (p=0.00025) y que 20–22 años (p=0.0233).
- **Programa × Grupo de edad:** el grupo *Biología: 23–31 años* presenta el IMC más alto, con diferencias significativas frente a múltiples combinaciones de programas y edades más jóvenes.
- **Programa × Género × Grupo de edad:** se identifican varias combinaciones con diferencias significativas, destacando nuevamente el subgrupo de Biología en edades mayores.

## Conclusión principal

El IMC varía significativamente según el **grupo de edad**, y existen **interacciones significativas** entre programa académico, género y edad. El subgrupo **Biología (23–31 años)** presenta el IMC más alto de la muestra. Se recomienda:

- Programas de educación nutricional adaptados por edad y programa académico.
- Fomento de actividad física dentro y fuera del entorno académico.
- Tamizajes periódicos del estado nutricional.
- Mejora de la oferta alimentaria universitaria.
- Incorporación de la salud y el autocuidado como ejes transversales de la formación.

## Estructura del documento

1. Metodología
2. Población y muestra
3. Variables del diseño experimental
4. Diseño experimental
   4.1 Prueba de los supuestos (normalidad, independencia, homogeneidad, ANOVA, prueba de medias)
5. Resultados
   5.1 Verificación de supuestos
   5.2 Comparaciones múltiples
6. Conclusión
- Anexo
- Referencias

## Referencias

1. Cerda G., H. *Diseño y análisis estadístico de experimentos*. McGraw-Hill, 2002.
2. Montgomery, D. C. *Diseño y análisis de experimentos*. 9.ª ed. Limusa, 2019.
3. Nieto Ortiz, D., Nieto Mendoza, I., Mejía Amézquita, M. "Hábitos alimentarios e índice de masa corporal en estudiantes de la Universidad del Atlántico, Barranquilla". *Revista Digital: Actividad Física y Deporte*, 7(2), 2021.
