# Simulador del Generador de ⁹⁹Mo → ⁹⁹ᵐTc

Simulador interactivo del **equilibrio transitorio** en un generador de ⁹⁹Mo/⁹⁹ᵐTc, desarrollado como material de apoyo docente en el Departamento de Tecnología Médica, Universidad de Chile.

La pregunta que responde es concreta: si el ⁹⁹ᵐTc decae con una semivida de apenas 6 h, ¿cómo puede su actividad llegar a casi igualar la del ⁹⁹Mo, que decae en 66 h? El simulador lo muestra hora a hora, tratando cada emisión horaria del padre como una **cohorte** independiente que se desvanece sin desaparecer antes de que nazca la siguiente.

> ⚠️ **Versión de demostración.** Material didáctico: los valores son ilustrativos y no sustituyen los cálculos, protocolos ni registros de una unidad de radiofarmacia.

## Acceso en línea

👉 **https://lucianotejadac.github.io/simulador-generador-mo99-tc99m/**

No requiere instalación: funciona en el navegador.

## Contexto académico

Radiofarmacia · cinética de generadores. Está pensado para acompañar la explicación del equilibrio transitorio, un contenido que suele presentarse solo como fórmula de Bateman y que aquí se descompone en un mecanismo visible: nacimiento, decaimiento y acumulación de cohortes sucesivas.

## Qué muestra

- **Activímetro del hijo**: lectura de la actividad total de ⁹⁹ᵐTc disponible en cada instante, en mCi y GBq.
- **Panel de tarjetas**: actividad del ⁹⁹Mo, tiempo transcurrido, número de cohortes emitidas, razón hijo/padre y contenido de la última jeringa.
- **Narración dinámica**: en cada paso explica cuánto aporta la cohorte nueva, cuánto conservan las anteriores y en qué porcentaje del padre va la suma. Avisa cuando se alcanza el equilibrio transitorio.
- **Línea de tiempo de cohortes**: una fila por cohorte horaria; el trazo se atenúa a medida que decae, dejando ver que las cohortes viejas siguen aportando cuando nacen las nuevas.
- **Gráfico de actividad**: curvas de ⁹⁹ᵐTc, ⁹⁹Mo y de la fracción del padre que alimenta al hijo (87.6 %).
- **Elución**: retira de la columna la fracción seleccionada del ⁹⁹ᵐTc acumulado, marca el momento en la línea de tiempo y deja al ⁹⁹Mo intacto para que la pila vuelva a reconstruirse.

## Modelo físico

| Parámetro | Valor |
|---|---|
| Actividad de calibración del ⁹⁹Mo | 1 000 mCi (37 GBq) |
| Semivida del padre ⁹⁹Mo | 66 h |
| Semivida del hijo ⁹⁹ᵐTc | 6.01 h |
| Ramificación hacia el estado metaestable | 87.6 % |
| Paso temporal | 1 h |
| Horizonte de simulación | 36 h |
| Eficiencia de elución | 75 % · 85 % · 95 % · 100 % (85 % por defecto) |
| Razón hijo/padre en equilibrio | ≈ 96 % |

Cada hora el padre entrega una cohorte de actividad A₀ = 0.876 × A_padre × (1 − e^(−λ_hijo·1h)), y toda cohorte previa se multiplica por e^(−λ_hijo·1h). La suma de esta serie geométrica reproduce exactamente la solución de Bateman. El techo del 96 % surge de multiplicar la ramificación (87.6 %) por el exceso λ_hijo/(λ_hijo − λ_padre) ≈ 1.10.

## Uso

| Control | Acción |
|---|---|
| Avanzar 1 hora | Emite una cohorte y decae todas las anteriores |
| Avanzar 6 h / 12 h | Repite el paso horario 6 o 12 veces |
| Eluir | Retira de la columna la fracción seleccionada de ⁹⁹ᵐTc |
| Eficiencia | Elige el rendimiento de la elución (75–100 %) |
| Reiniciar | Vuelve al generador recién calibrado |

## Stack técnico

- HTML, CSS y JavaScript sin framework.
- **Chart.js 4.4.1** (vía CDN) para el gráfico de actividad.
- **Canvas 2D** dibujado a mano para la línea de tiempo de cohortes.
- Tipografías Space Grotesk e IBM Plex (Sans y Mono) desde Google Fonts.
- Diseño responsivo y regiones `aria-live` para lectores de pantalla.

Requiere conexión a internet en la primera carga para obtener Chart.js y las tipografías.

## Limitaciones conocidas

- El tiempo avanza en pasos discretos de 1 h; no hay animación continua ni tiempos intermedios.
- La elución retira la misma fracción de todas las cohortes y deja el ⁹⁹Mo intacto: no modela rotura de columna, arrastre de ⁹⁹Mo ni pureza radionucleídica.
- No representa volumen de elución ni concentración radiactiva (mCi/mL).
- La actividad de calibración, las semividas y el horizonte de 36 h están fijos en el código.
- Depende de recursos externos (CDN y Google Fonts): sin conexión, el gráfico no se dibuja.

## Roadmap

- [ ] Actividad de calibración, semividas y horizonte configurables
- [ ] Volumen de elución y concentración radiactiva
- [ ] Exportación de la serie a CSV
- [ ] Versión sin conexión con Chart.js y tipografías embebidas
- [ ] Comparación con un generador en equilibrio secular (⁶⁸Ge/⁶⁸Ga)

## Cómo citar

Tejada Castro, L. (2026). *Simulador del generador de ⁹⁹Mo/⁹⁹ᵐTc* [software educativo]. Departamento de Tecnología Médica, Facultad de Medicina, Universidad de Chile. https://lucianotejadac.github.io/simulador-generador-mo99-tc99m/

## Autor

**Luciano Tejada Castro**
Departamento de Tecnología Médica · Facultad de Medicina · Universidad de Chile
lucianotejada@uchile.cl

## Licencia

© 2026 Luciano Tejada Castro. Todos los derechos reservados. Obra protegida por la Ley N° 17.336 sobre Propiedad Intelectual de Chile. Cualquier reproducción, adaptación o comunicación pública distinta del uso personal requiere autorización escrita del autor.

Este proyecto utiliza Chart.js 4.4.1, © Chart.js Contributors, distribuido bajo licencia MIT. Ese componente se rige por su propia licencia y no queda comprendido en la reserva de derechos anterior.
