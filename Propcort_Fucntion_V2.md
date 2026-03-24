# 1️⃣ Micro Market Score

#  Core Idea

You are trying to answer:

> “Is this property **overpriced or underpriced** compared to its micro-market?”

So we compare:

```id="g8g9n1"
Property Price (₹/sqft)
vs
Micro-market Average Price (₹/sqft)
```

---

#  Step 1 — Define Micro-Market

A **micro-market** is a small localized area:

Examples:

* Whitefield
* Sarjapur Road
* Varthur

Each micro-market should have:

```id="y5z7wx"
avg_price_per_sqft
median_price_per_sqft
price_std_deviation
```

---

# Step 2 — Price Deviation Formula

### Basic Formula

<img width="731" height="369" alt="image" src="https://github.com/user-attachments/assets/a9179c82-bb6c-4f7c-b2d4-27cdfe4f425d" />


---

#  Step 3 — Convert to Score (Most Important Part)

Now convert deviation → **score (0–100)**

---

## Method 1 (Recommended — Linear Model)

Define range:

```id="brc9az"
-20% (undervalued) → best
0% → neutral
+20% (overpriced) → worst
```

### Formula

<img width="649" height="116" alt="image" src="https://github.com/user-attachments/assets/daadc99f-db0c-4b29-85ae-a13fe94a58ac" />

---

### Final Mapping

| Deviation | Score |
| --------- | ----- |
| -20%      | 100   |
| -10%      | 90    |
| 0%        | 75    |
| +10%      | 60    |
| +20%      | 40    |

---

### Example

Deviation = +5.5%

[
Score =
100 - (0.055/0.20 × 50)
]

[
= 100 - 13.75
= 86.25
]

✅ **Price Score ≈ 86**

---

# Step 4 — Improved Model (Production Grade)

The above is good, but real systems use **z-score normalization**.

---

## Method 2 (Advanced — Z Score Model)

Use standard deviation:

<img width="706" height="480" alt="image" src="https://github.com/user-attachments/assets/87f6c446-45fb-4744-91cd-c183e429e97b" />


---

| Z  | Score |
| -- | ----- |
| -2 | 100   |
| -1 | 90    |
| 0  | 75    |
| +1 | 60    |
| +2 | 45    |

---

### Result

Z = 0.5

[
Score = 100 - (0.5 × 15)
= 92.5
]

---



# 2️⃣ Commute Score
## we have to assign some constant values for school as 0.12, Hospital as 0.15 and Malls and IT hubs as 0.10 (Higher ther value higher the priority)
Score = 100 - distance

Then:

1 km → 99
5 km → 95
10 km → 90

❌ This is WRONG because:

1 km vs 5 km difference is HUGE in real life
8 km vs 10 km difference is small
🔷 Decay Score solves this

It makes the score drop faster initially, then slowly.

🔷 The Formula
Exponential Decay Function
𝑆
𝑐
𝑜
𝑟
𝑒
=
𝑒
−
𝛼
⋅
𝑑
Score=e
−α⋅d

Where:

𝑑
d = distance (km) or time (minutes)
𝛼
α = decay constant (controls how fast score drops)
🔷 How it behaves

Example (α = 0.15):

Distance	Score
1 km	0.86
3 km	0.64
5 km	0.47
10 km	0.22

👉 Notice:

Big drop from 1 → 5 km
Smaller drop from 5 → 10 km

That’s real-world behavior.
## we can use inbuilt exp() to calculate that.
### lets say school is 5km away.
<img width="668" height="773" alt="image" src="https://github.com/user-attachments/assets/2934803a-8c5c-4d59-a040-36759c5a1801" />


