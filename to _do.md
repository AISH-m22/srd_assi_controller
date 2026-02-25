## Overview

Previously, a constant velocity was used in the Stanley controller. However, to operate the vehicle near the handling limit, the velocity must be dynamically computed based on path curvature and vehicle performance constraints.

The goal is to compute the **maximum safe velocity at each point of the reference path** rather than using a fixed speed.

---

## Physical Principle

When a vehicle turns, it requires lateral acceleration given by:

\[
a_y = \frac{v^2}{R}
\]

Where:

- \( v \) = vehicle velocity  
- \( R \) = turn radius  
- \( a_y \) = lateral acceleration  

Rearranging:

\[
v = \sqrt{a_y \cdot R}
\]

Key insight:

- Tight curves (small radius) → lower allowable speed  
- Gentle curves (large radius) → higher allowable speed  

---

## Implementation Steps

### 1. Compute Path Curvature

If curvature is represented as:

\[
\kappa
\]

Then the turning radius is:

\[
R = \frac{1}{\kappa}
\]

---

### 2. Determine Maximum Lateral Acceleration

The maximum lateral acceleration can be obtained from vehicle performance data.

#### Option 1: Using GGV / Performance Envelope

Use the vehicle’s GGV diagram or lookup table.

#### Option 2: Simplified Approximation

If detailed dynamics data is unavailable:

\[
a_{lat,max} = \mu g
\]

Where:

- \( \mu \) = tire-road friction coefficient  
- \( g \) = gravitational acceleration  

---

### 3. Compute Maximum Velocity for Each Path Point

The curvature-based velocity limit is:

\[
v_{max}(s) = \sqrt{a_{lat,max} \cdot R}
\]

Compute this for every reference path index \( s \).

---

### 4. Integrate With Stanley Controller

Replace constant reference velocity with:
