# Funcionamiento del Criptosistema de Vigenère

## 1. Descripción General

El **cifrado de Vigenère** es un criptosistema clásico de sustitución polialfabética, descrito en el siglo XVI y asociado históricamente a Blaise de Vigenère.

- Tipo: Cifrado simétrico
- Naturaleza: Sustitución polialfabética
- Dominio típico: Alfabeto latino (26 letras)
- Operación base: Aritmética modular

---

## 2. Modelo Algebraico

Se trabaja sobre el anillo:

\[
\mathbb{Z}\_{26} = \{0,1,\dots,25\}
\]

con la codificación:

\[
A=0,\; B=1,\; \dots,\; Z=25
\]

Sea:

\[
M = m_1 m_2 \dots m_n
\]

el mensaje y

\[
K = k_1 k_2 \dots k_t
\]

la clave.  
La clave se repite periódicamente hasta longitud \(n\).

---

## 3. Cifrado

Para cada posición \(i\):

\[
c_i = (m_i + k_i) \mod 26
\]

donde:

- \(m_i\) es el valor numérico del mensaje
- \(k_i\) es el valor numérico de la clave
- \(c_i\) es el símbolo cifrado

En forma vectorial:

\[
C = M + K \pmod{26}
\]

---

## 4. Descifrado

El descifrado consiste en restar módulo 26:

\[
m_i = (c_i - k_i) \mod 26
\]

En forma compacta:

\[
M = C - K \pmod{26}
\]

---

## 5. Interpretación como Cifrados César Variables

Cada letra de la clave define un desplazamiento distinto:

\[
E\_{k_i}(x) = (x + k_i) \mod 26
\]

Por tanto:

\[
E*K(M) = E*{k*1}(m_1)\, E*{k*2}(m_2)\, \dots \, E*{k_n}(m_n)
\]

Si la clave tiene longitud \(t\), el sistema equivale a \(t\) cifrados César independientes aplicados de manera periódica.

---

## 6. Ejemplo

Mensaje:

```

ATAQUE

```

Clave:

```

SOL

```

Clave extendida:

```

SOLSOL

```

Conversión numérica:

\[
A=0,\; T=19,\; S=18,\; O=14,\; L=11
\]

Cálculo:

\[
c_1 = (0 + 18) \mod 26 = 18
\]
\[
c_2 = (19 + 14) \mod 26 = 7
\]
\[
c_3 = (0 + 11) \mod 26 = 11
\]

Resultado parcial:

```

SHL...

```

---

## 7. Seguridad

Ventajas históricas:

- Rompe el análisis de frecuencia simple
- Introduce variabilidad en el desplazamiento

Debilidades:

- Si la clave es corta → patrones periódicos
- Vulnerable al método de Kasiski
- Vulnerable al índice de coincidencia

Si la clave es:

- Aleatoria
- De la misma longitud que el mensaje
- Nunca reutilizada

Entonces el sistema se convierte en:

\[
c_i = (m_i + k_i) \mod 26
\]

lo cual corresponde al **One-Time Pad**, que es perfectamente seguro en sentido teórico.

---

## 8. Resumen Operativo

```

Mensaje
↓
Convertir letras a números
↓
Sumar clave módulo 26
↓
Convertir números a letras
↓
Texto cifrado

```

---

## Conclusión

El criptosistema de Vigenère:

- Introduce la sustitución polialfabética
- Generaliza el cifrado César
- Se modela elegantemente con aritmética modular
- Es fundamental para comprender la evolución de la criptografía clásica
