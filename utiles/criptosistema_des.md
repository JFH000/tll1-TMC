# Funcionamiento del Criptosistema DES

## 1. Descripción General

El **Data Encryption Standard (DES)** es un criptosistema de cifrado simétrico por bloques. Fue adoptado como estándar en 1977 por el **National Institute of Standards and Technology (NIST)** (anteriormente NBS).

- Tamaño de bloque: **64 bits**
- Tamaño de clave: **64 bits** (56 bits efectivos + 8 bits de paridad)
- Número de rondas: **16**
- Estructura: **Red de Feistel**

---

## 2. Esquema General

DES cifra un bloque de 64 bits mediante 16 rondas de transformación basadas en subclaves derivadas de la clave principal.

### Paso 1: Permutación Inicial (IP)

Dado un bloque de texto plano:

\[
M \in \{0,1\}^{64}
\]

Se aplica una permutación fija:

\[
IP(M) = L_0 \parallel R_0
\]

donde:

- \(L_0\): primeros 32 bits
- \(R_0\): últimos 32 bits

---

## 3. Estructura de Feistel

Para cada ronda \(i = 1, 2, \dots, 16\):

\[
L*i = R*{i-1}
\]

\[
R*i = L*{i-1} \oplus F(R\_{i-1}, K_i)
\]

donde:

- \(K_i\): subclave de la ronda \(i\)
- \(F\): función de ronda
- \(\oplus\): operación XOR

---

## 4. Función de Ronda \(F\)

La función \(F\) es el núcleo de seguridad del sistema.

\[
F(R, K) = P(S(E(R) \oplus K))
\]

Se compone de cuatro etapas:

### 4.1 Expansión \(E\)

Expande \(R\) de 32 bits a 48 bits:

\[
E: \{0,1\}^{32} \rightarrow \{0,1\}^{48}
\]

Esto introduce redundancia para mezclar con la subclave.

---

### 4.2 Mezcla con la Subclave

\[
B = E(R) \oplus K
\]

---

### 4.3 Sustitución (S-Boxes)

El bloque de 48 bits se divide en 8 bloques de 6 bits:

\[
B = B_1 \parallel B_2 \parallel \dots \parallel B_8
\]

Cada bloque pasa por una S-Box:

\[
S_i: \{0,1\}^6 \rightarrow \{0,1\}^4
\]

Produciendo:

\[
S(B) = S_1(B_1) \parallel \dots \parallel S_8(B_8)
\]

Resultado: 32 bits.

---

### 4.4 Permutación \(P\)

Se aplica una permutación fija:

\[
P: \{0,1\}^{32} \rightarrow \{0,1\}^{32}
\]

Esto difunde los bits para la siguiente ronda.

---

## 5. Generación de Subclaves

La clave original \(K\) (64 bits) se reduce a 56 bits eliminando los bits de paridad.

Se divide en:

\[
C_0, D_0 \in \{0,1\}^{28}
\]

Para cada ronda:

1. Se realiza un desplazamiento circular a la izquierda:
   \[
   C*i = LS(C*{i-1})
   \]
   \[
   D*i = LS(D*{i-1})
   \]

2. Se aplica una permutación (PC-2):

\[
K_i = PC2(C_i \parallel D_i)
\]

donde:

\[
K_i \in \{0,1\}^{48}
\]

---

## 6. Paso Final

Después de 16 rondas se obtiene:

\[
L*{16} \parallel R*{16}
\]

Se intercambian:

\[
R*{16} \parallel L*{16}
\]

Luego se aplica la permutación final \(FP\) (inversa de IP):

\[
C = FP(R*{16} \parallel L*{16})
\]

donde \(C\) es el texto cifrado.

---

## 7. Descifrado

El descifrado usa el mismo algoritmo, pero aplicando las subclaves en orden inverso:

\[
K*{16}, K*{15}, \dots, K_1
\]

Gracias a la estructura de Feistel:

\[
D_K(E_K(M)) = M
\]

---

## 8. Seguridad

DES fue seguro en su época, pero actualmente es vulnerable debido a:

- Clave efectiva de solo 56 bits
- Ataques de fuerza bruta
- Avances en hardware

En 1998, la EFF rompió DES en menos de 3 días.

Hoy se considera inseguro y fue reemplazado por **AES**.

---

## 9. Resumen del Flujo

Texto Plano (64 bits)
↓
Permutación Inicial (IP)
↓
16 Rondas Feistel
↓
Intercambio final
↓
Permutación Final (FP)

---

## Conclusión

DES es un criptosistema clásico basado en:

- Confusión → S-Boxes
- Difusión → Permutaciones
- Seguridad estructural → Red de Feistel

Aunque ya no es seguro, sigue siendo fundamental para entender el diseño de cifrados modernos.
↓
Texto Cifrado (64 bits)
