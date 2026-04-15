# Heart Disease Risk & Heart Age Calculator based on TG and HDL

A simple tool that estimates your 10-year heart disease risk and your **heart age** from a standard blood test — just triglycerides and HDL cholesterol.

**[Try it →](https://cvdrisk.github.io/)**

## What You Get

Enter your age, triglycerides, and HDL cholesterol (from any routine lipid panel). The calculator shows:

- **Your heart age** — if your lipids are worse than average, your heart may be aging faster than you are. A 50-year-old with poor TG/HDL could have the heart of a 60-year-old. If your lipids are good, your heart age can be younger than your actual age.
- **Relative risk** — how much more (or less) likely you are to develop heart disease compared to someone with the best TG/HDL combination
- **10-year risk estimate** — your estimated chance of a heart disease event in the next decade, adjusted for your age
- **TG/HDL ratio** — a single number from your blood work that captures most of the lipid-driven risk. Lower is better.

## What Counts as "Heart Disease" Here?

The underlying study tracked heart attacks (fatal and non-fatal) and angina (chest pain from restricted blood flow to the heart). It does **not** include strokes or other vascular conditions.

## Where the Numbers Come From

### The Risk Grid

**Jeppesen J, Hein HO, Suadicani P, Gyntelberg F.** Triglyceride concentration and ischemic heart disease: an eight-year follow-up in the Copenhagen Male Study. *Circulation.* 1998;97(11):1029–1036. [Full text](https://doi.org/10.1161/01.CIR.97.11.1029)

Researchers followed 2,906 men (aged 53–74, free of heart disease at the start) for 8 years. They measured fasting triglycerides and HDL cholesterol, split each into thirds, and counted how many men in each of the resulting 9 groups developed heart disease. The key finding: the TG/HDL combination was a stronger predictor of heart disease than LDL cholesterol, total cholesterol, or HDL alone.

The 9-cell grid of outcomes is what the calculator interpolates across:

|  | Low HDL | Mid HDL | High HDL |
|---|---|---|---|
| **Low TG** | 7.4% | 3.1% | 3.5% |
| **Mid TG** | 10.2% | 7.2% | 5.4% |
| **High TG** | 13.1% | 9.8% | 8.5% |

The best group (low TG + mid HDL) had a 3.1% incidence over 8 years. The worst (high TG + low HDL) had 13.1% — more than four times the risk.

### The Age Curve

**Goff DC Jr, Lloyd-Jones DM, Bennett G, et al.** 2013 ACC/AHA Guideline on the Assessment of Cardiovascular Risk. *Circulation.* 2014;129(25 suppl 2):S49–S73. [Full text](https://doi.org/10.1161/01.cir.0000437741.48606.98)

The study cohort had a mean age of 63. To estimate risk at other ages, the calculator uses the ACC/AHA Pooled Cohort Equations — the standard US cardiovascular risk model — to derive how baseline risk scales with age for a healthy man with optimal risk factors. Risk roughly doubles every decade: ~0.8% at 40, ~2.7% at 50, ~7% at 60, ~15% at 70.

This age curve is used for two things:
- Scaling the study's results up or down to match your age
- Computing heart age: finding which age on the baseline curve matches your actual calculated risk

## How the Math Works

1. **Interpolate** your TG and HDL values on the 9-cell grid to get an 8-year risk estimate
2. **Normalize to 10 years** using a constant hazard model: derive the annual rate from the 8-year figure, then project forward to 10 years
3. **Adjust for your age** by scaling proportionally to the baseline age curve
4. **Find your heart age** by looking up which age on the baseline curve has the same risk as your calculated result

## Features

- **Unit toggle** — switch between mmol/L and mg/dL with one tap
- **Remembers your values** — your inputs and unit preference are saved in your browser so they're there when you come back
- **Works offline** — runs entirely in your browser, no data sent anywhere
- **Mobile-friendly** — works on any screen size

## Important Limitations

- **Men only** — the Copenhagen study enrolled only men. Results may not apply to women.
- **Ages 53–74 in the study** — the calculator extrapolates to ages 40–79 using the age curve, but this is approximate outside the original range.
- **White European men** — participants were Danish. Results may differ for other ethnicities.
- **1980s cohort** — data collected before widespread statin use. Absolute risk numbers may be higher than what you'd see today with modern treatment.
- **Fasting blood work required** — the study used fasting triglycerides. Non-fasting values will read higher and overestimate your risk.
- **Heart disease only** — this estimates heart attack and angina risk, not total cardiovascular risk (which also includes stroke).

## This Is Not Medical Advice

This calculator is for educational purposes only. It is not a validated clinical tool. Talk to your doctor about your actual cardiovascular risk and whether any intervention is appropriate for you.

## License

MIT

## References

1. Jeppesen J, Hein HO, Suadicani P, Gyntelberg F. Triglyceride concentration and ischemic heart disease: an eight-year follow-up in the Copenhagen Male Study. *Circulation.* 1998;97(11):1029–1036.
2. Goff DC Jr, Lloyd-Jones DM, Bennett G, et al. 2013 ACC/AHA Guideline on the Assessment of Cardiovascular Risk. *Circulation.* 2014;129(25 suppl 2):S49–S73.
