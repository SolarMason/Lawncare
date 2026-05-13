# NEPA-PRO Lawn Care — Pricing & Profit Logic

**Target net hourly:** $65/hr labor after per-visit overhead
**Overhead per visit (avg):** $8 (Small) → $18 (XL One-Time)
  - Battery + charging amortization: $1–3
  - Equipment wear / depreciation: $2–4
  - Insurance allocation per visit: $2
  - Travel time + truck fuel to/from site: $3–7
  - Debris bag/disposal allocation: $0–2

## Time-on-site assumptions (full visit: mow + edge + trim + blow-off)

| Tier | Baseline (Weekly) | Bi-Weekly (1.15×) | Monthly (1.4×) | One-Time (1.5×) |
|---|---|---|---|---|
| Small | 25 min | 29 min | 35 min | 38 min |
| Medium | 40 min | 46 min | 56 min | 60 min |
| Large | 60 min | 69 min | 84 min | 90 min |
| XL | 85 min | 98 min | 119 min | 128 min |

> Less-frequent visits take longer because the grass is taller and there's more debris. This is reflected in the time multipliers above.

## Profit verification — every cell clears $65/hr net

Formula: `net_hourly = (price - overhead) / (minutes_on_site / 60)`

### Small Yard
| Frequency | Price | Time | Overhead | Net Labor | Net $/hr |
|---|---|---|---|---|---|
| Weekly | $40 | 25 min | $8 | $32 | **$76.80** |
| Bi-Weekly | $45 | 29 min | $8 | $37 | **$76.55** |
| Monthly | $55 | 35 min | $10 | $45 | **$77.14** |
| One-Time | $70 | 38 min | $12 | $58 | **$91.58** |

### Medium Yard
| Frequency | Price | Time | Overhead | Net Labor | Net $/hr |
|---|---|---|---|---|---|
| Weekly | $60 | 40 min | $10 | $50 | **$75.00** |
| Bi-Weekly | $70 | 46 min | $10 | $60 | **$78.26** |
| Monthly | $85 | 56 min | $12 | $73 | **$78.21** |
| One-Time | $105 | 60 min | $14 | $91 | **$91.00** |

### Large Yard
| Frequency | Price | Time | Overhead | Net Labor | Net $/hr |
|---|---|---|---|---|---|
| Weekly | $85 | 60 min | $12 | $73 | **$73.00** |
| Bi-Weekly | $100 | 69 min | $13 | $87 | **$75.65** |
| Monthly | $120 | 84 min | $15 | $105 | **$75.00** |
| One-Time | $145 | 90 min | $16 | $129 | **$86.00** |

### XL Yard
| Frequency | Price | Time | Overhead | Net Labor | Net $/hr |
|---|---|---|---|---|---|
| Weekly | $115 | 85 min | $14 | $101 | **$71.29** |
| Bi-Weekly | $130 | 98 min | $15 | $115 | **$70.41** |
| Monthly | $160 | 119 min | $17 | $143 | **$72.10** |
| One-Time | $195 | 128 min | $18 | $177 | **$82.97** |

**Lowest net rate in the entire grid: $70.41/hr (XL Bi-Weekly) — clears $65/hr target with $5+ buffer.**

## Add-on pricing logic

| Service | Time | Materials | Overhead | Price | Net $/hr |
|---|---|---|---|---|---|
| Spring Cleanup | 180 min (3 hr) | $15 (bags, blades) | $25 | $295 | **$85.00** |
| Fall Cleanup | 180 min (3 hr) | $15 (bags) | $25 | $295 | **$85.00** |
| Aeration & Overseed | 90 min | $35 (seed + starter fert) | $20 | $225 | **$113.33** |
| Hedge Trimming | 60 min | $5 | $15 | $95 | **$75.00** |

Aeration runs hotter on hourly because it requires equipment rental/ownership cost amortization NOT captured in the standard overhead figure.

## Stripe billing model

- **Weekly subscription**: $X charged every 7 days; 1 visit per charge.
- **Bi-Weekly subscription**: $X charged every 14 days; 1 visit per charge.
- **Monthly subscription**: $X charged every 30 days; 1 visit per charge.
- **One-Time**: single immediate charge.

Customer can cancel any subscription anytime via Stripe portal — Stripe sends them a billing portal link in every receipt email.

## Levers if you need to adjust

- **Bagging upcharge**: +$10 (S/M) / +$15 (L/XL) per visit if customer requests.
- **First-cut surcharge** (lawns >6" tall on first visit): +25% on first visit only. Mention in welcome text.
- **Distance surcharge** (zip codes outside 184/185/186/187/188): +$15/visit.
- **HOA / commercial multi-property discount**: -10% on 3+ properties at same address/HOA.

## Annual revenue math (sanity check)

If you fill a single weekday with 8 small-yard weekly customers @ $40:
- Daily: $320
- Weekly: $1,600 (5 days × 8 customers)
- Annual (28-week NEPA season): $44,800 per route-day

Replace half of those with Medium @ $60:
- Daily: $400
- Weekly: $2,000
- Annual: $56,000 per route-day

Maxed route-day (8 customers × $85 Large Weekly): $3,400/wk → **$95,200/season per route-day.**
