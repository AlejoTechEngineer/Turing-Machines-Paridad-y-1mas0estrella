<h1 align="center">🤖 Máquinas de Turing — Paridad y 1⁺0*</h1>

> Fundación Universitaria Internacional de La Rioja · 2026

---

## 📋 Descripción

Este repositorio contiene el diseño formal, diagramas de estados e implementación en **JFLAP** de dos Máquinas de Turing de una sola cinta, construidas como parte del Laboratorio No. 2 de la asignatura Informática Teórica.

Cada máquina fue diseñada para reconocer un lenguaje formal específico sobre el alfabeto Σ = {0, 1}, con alfabeto de cinta Γ = {0, 1, □}.

---

## 🧠 Ejercicios Implementados

### Ejercicio 1 — Paridad de Unos
**Lenguaje reconocido:**
```
L = { w ∈ {0,1}* | el número de símbolos "1" en w es par }
```

| Estado | Rol |
|--------|-----|
| `q0` | Estado inicial y de paridad par |
| `q1` | Paridad impar |
| `q_accept` | Estado de aceptación final |
| `q_reject` | Estado de rechazo |

**Estrategia:** Alternancia de estados cada vez que se lee un `1`. Los ceros no modifican la paridad. Al encontrar el blanco `□`, se acepta si se está en `q0` y se rechaza si se está en `q1`.

---

### Ejercicio 2 — Cadenas de la forma 1⁺0*
**Lenguaje reconocido:**
```
L = { 1ⁿ0ᵐ | n ≥ 1, m ≥ 0 }
```

| Estado | Rol |
|--------|-----|
| `q0` | Estado inicial — verifica que la cadena empiece con al menos un `1` |
| `q1` | Fase de lectura del bloque de unos |
| `q2` | Fase de lectura del bloque de ceros (aceptación posible) |
| `q_accept` | Estado de aceptación final |
| `q_reject` | Estado sumidero de rechazo |

**Estrategia:** Un único recorrido izquierda→derecha dividido en tres fases: verificación del primer `1`, procesamiento de los unos consecutivos, y procesamiento del bloque de ceros. Cualquier violación del patrón conduce directamente a `q_reject`.

---

## 📁 Estructura del Repositorio

```
Turing-Machines-Paridad-y-1mas0estrella/
│
├── 📄 README.md
│
├── 📂 informe/
│   └── Desarrollo_Proyecto_Alejandro_De_Mendoza.pdf
│
└── 📂 jflap/
    ├── MT_paridad_unos.jff        ← Máquina de Turing Ejercicio 1
    └── MT_1plus_0star.jff         ← Máquina de Turing Ejercicio 2
```

---

## 🔬 Tablas de Transición

### MT 1 — Paridad de Unos

| Estado actual | Símbolo leído | Símbolo escrito | Movimiento | Estado siguiente |
|:---:|:---:|:---:|:---:|:---:|
| q0 | 0 | 0 | R | q0 |
| q0 | 1 | 1 | R | q1 |
| q0 | □ | □ | S | **q_accept** |
| q1 | 0 | 0 | R | q1 |
| q1 | 1 | 1 | R | q0 |
| q1 | □ | □ | S | **q_reject** |

### MT 2 — Cadenas 1⁺0*

| Estado actual | Símbolo leído | Símbolo escrito | Movimiento | Estado siguiente |
|:---:|:---:|:---:|:---:|:---:|
| q0 | 1 | 1 | R | q1 |
| q0 | 0 | 0 | S | **q_reject** |
| q0 | □ | □ | S | **q_reject** |
| q1 | 1 | 1 | R | q1 |
| q1 | 0 | 0 | R | q2 |
| q1 | □ | □ | S | **q_accept** |
| q2 | 0 | 0 | R | q2 |
| q2 | □ | □ | S | **q_accept** |
| q2 | 1 | 1 | S | **q_reject** |

---

## ✅ Casos de Prueba Validados

### MT 1 — Paridad
| Cadena | Resultado | Razón |
|--------|-----------|-------|
| `""` (vacía) | ✅ ACEPTA | 0 unos → par |
| `110` | ✅ ACEPTA | 2 unos → par |
| `1010` | ✅ ACEPTA | 2 unos → par |
| `1` | ❌ RECHAZA | 1 uno → impar |
| `111` | ❌ RECHAZA | 3 unos → impar |

### MT 2 — Cadenas 1⁺0*
| Cadena | Resultado | Razón |
|--------|-----------|-------|
| `1` | ✅ ACEPTA | 1 uno, 0 ceros |
| `110` | ✅ ACEPTA | 2 unos, 1 cero |
| `1100` | ✅ ACEPTA | 2 unos, 2 ceros |
| `""` (vacía) | ❌ RECHAZA | n = 0 → excluida |
| `0` | ❌ RECHAZA | No empieza con `1` |
| `101` | ❌ RECHAZA | `1` después de `0` |
| `01` | ❌ RECHAZA | Empieza con `0` |

---

## 🛠️ Herramientas Utilizadas

- **JFLAP** — Java Formal Languages and Automata Package  
  Rodger, S. H. & Finley, T. W. (2006). Duke University. [jflap.org](http://www.jflap.org)

---

## 📚 Referencias Bibliográficas

- Hopcroft, J. E., Motwani, R., & Ullman, J. D. (2008). *Introduction to Automata Theory, Languages, and Computation* (3rd ed.). Pearson.
- Sipser, M. (2013). *Introduction to the Theory of Computation* (3rd ed.). Cengage Learning.
- Turing, A. M. (1936). On computable numbers, with an application to the Entscheidungsproblem. *Proceedings of the London Mathematical Society*, 42(2), 230–265.

---

## 👨‍💻 Autor

**Alejandro De Mendoza**  
Ingeniería Informática 
Fundación Universitaria Internacional de La Rioja  
Bogotá D.C., Colombia · 2026

---

> *"A Turing machine is an idealized computing device."*  
> — Alan M. Turing
