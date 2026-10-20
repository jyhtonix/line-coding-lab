# line-coding-lab
Pick an encoding scheme, type a bit sequence and a transmission time, and see how the data rate, signal elements and baud rate come out, with every calculation shown and the waveform drawn to scale.


To access the webpage: https://jyhtonix.github.io/line-coding-lab/


# Bit Rate vs Baud Rate in Line Encoding

A quick reference for understanding the difference between **bit rate (bps)** and **baud rate (baud)**, and how each line/block encoding scheme affects the relationship between them.

## Definitions

| Symbol | Meaning | Unit |
|--------|---------|------|
| `R` | Bit rate | bps |
| `S` | Baud rate (signal elements per second) | baud |
| `r` | Number of bits represented by one signal element | bits/signal element |

## General Formula

```
S = R / r
```

or, equivalently,

```
R = S × r
```

## Summary Table

| Encoding Scheme | Bits per Signal Element (`r`) | Baud-Rate Formula | Relationship |
|-----------------|-------------------------------|-------------------|--------------|
| NRZ-L | 1 | `S = R / 1` | Baud = Bit rate |
| NRZ-I | 1 | `S = R / 1` | Baud = Bit rate |
| Manchester | 1/2 | `S = R / (1/2) = 2R` | Baud = 2 × Bit rate |
| Differential Manchester | 1/2 | `S = R / (1/2) = 2R` | Baud = 2 × Bit rate |
| Bipolar-AMI | 1 | `S = R / 1` | Baud = Bit rate |
| 4B/5B | 4 bits → 5 signal elements | `S = R × 5/4` | Baud = 1.25 × Bit rate |

---

## 1. NRZ-L

Each bit uses **one signal element**.

```
S = R
```

**Example:** 8 bits transmitted in 2 seconds

```
R = 8 / 2 = 4 bps
S = R = 4 baud
```

## 2. NRZ-I

NRZ-I also uses **one signal element per bit**.

```
S = R
```

The difference between NRZ-L and NRZ-I is *how the signal represents 0 and 1*, not the number of signal elements required per bit.

## 3. Manchester

Each bit contains **two signal levels/transitions** within one bit period, so each bit requires **2 signal elements**.

```
S = 2R
```

**Example:**

```
R = 4 bps
S = 2(4) = 8 baud
```

## 4. Differential Manchester

Same baud-rate relationship as Manchester:

```
S = 2R
```

The encoding method differs in how the transition at the beginning of the bit period represents the data, but each bit still requires **two signal elements**.

## 5. Bipolar-AMI

Bipolar-AMI uses **one signal element per bit**.

```
S = R
```

The three signal levels are typically:

- `0` → zero voltage
- `1` → positive voltage
- next `1` → negative voltage
- next `1` → positive voltage, and so on

The alternating polarity does **not** mean two signal elements are required.

## 6. 4B/5B

This one is different because **4 data bits are encoded into 5-bit code groups**.

For every 4 bits of actual data, 5 bits are transmitted:

```
S = R × (5/4)
```

or:

```
S = 1.25R
```

**Example:** original data rate `R = 4 Mbps`

```
S = 4 × (5/4)
S = 5 Mbaud
```

> **Teaching note:** 4B/5B is technically a *block coding* scheme, rather than a *line encoding* scheme like NRZ-L or Manchester. The 1.25 factor comes from its 4-to-5 bit expansion. If 4B/5B is subsequently transmitted using another line code, the final baud rate can depend on that underlying line encoding.

---

## Formula Sheet

| Scheme | Formula |
|--------|---------|
| NRZ-L | `S = R` |
| NRZ-I | `S = R` |
| Manchester | `S = 2R` |
| Differential Manchester | `S = 2R` |
| Bipolar-AMI | `S = R` |
| 4B/5B | `S = 1.25R` |

