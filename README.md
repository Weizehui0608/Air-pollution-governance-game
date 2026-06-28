# Campaign-and-Relapse in Air Pollution Governance — Data

> **Campaign-and-Relapse in Air Pollution Governance: A Tripartite Evolutionary Game with Environmental Feedback and Central-Inspection Forcing**
>  Juan Wei, Renkang Xiang. *Systems* 

This repository provides the monthly air-quality panel for the Beijing–Tianjin–Hebei
**"2+26" cities (2014–2024)** that motivates and disciplines the model in the paper
(Figure 2 and Section 5.4), together with the meteorological controls and the policy /
difference-in-differences design used in the supporting empirical analysis.

---

## Repository contents

| File | Rows | Columns | Purpose |
|------|------|---------|---------|
| `Module_A_2Plus26_Month_Panel_Fixed.csv` | 3,552 | 5 | Core air-quality panel (city × month) |
| `Module_AB_Panel_Final.csv` | 3,552 | 9 | Core panel **+** meteorological controls |
| `Module_ABD_Panel_Empirical_Ready.csv` | 3,552 | 12 | Core + meteorology **+** policy / DiD design |

---

## Coverage

- **Cities (28):** Beijing, Tianjin, and the 26 channel cities — Shijiazhuang, Tangshan,
  Langfang, Baoding, Cangzhou, Hengshui, Xingtai, Handan (Hebei); Taiyuan, Yangquan,
  Changzhi, Jincheng (Shanxi); Jinan, Zibo, Jining, Dezhou, Liaocheng, Binzhou, Heze
  (Shandong); Zhengzhou, Kaifeng, Anyang, Hebi, Xinxiang, Jiaozuo, Puyang (Henan).
- **Provinces (6):** Beijing, Tianjin, Hebei, Shanxi, Shandong, Henan.
- **Period:** 2014-05 to 2024-12 (128 months).
- **Unit of observation:** city × month (3,552 rows).

---

## Variable dictionary

### Common columns (all files)

| Column | Description | Unit |
|--------|-------------|------|
| `city` | City name (Chinese) | — |
| `year_month` | Observation month, `YYYY-MM` | — |
| `AQI` | Monthly mean Air Quality Index | index (unitless) |
| `PM2.5` | Monthly mean PM2.5 concentration | µg/m³ |
| `n_t` | Normalized air-quality state used in the model | [0, 1] |

`n_t` is the empirical counterpart of the model's air-quality state and is defined as

```
n_t = 1 − PM2.5 / PM2.5_max
```

where `PM2.5_max` is the maximum monthly PM2.5 across the panel. Higher `n_t` = cleaner air
(`n_t → 1` is the "blue-sky" state; `n_t → 0` is the most polluted state). In this panel `n_t`
ranges from 0.00 to 0.94.

### Additional columns in `Module_AB_*` and `Module_ABD_*` (meteorological controls)

| Column | Description | Unit |
|--------|-------------|------|
| `Temperature` | Monthly mean air temperature | °C |
| `Pressure` | Monthly mean surface pressure | hPa |
| `WindSpeed` | Monthly mean wind speed | m/s |
| `Precipitation` | Monthly precipitation | mm |

### Additional columns in `Module_ABD_*` (policy / difference-in-differences)

| Column | Description |
|--------|-------------|
| `Province` | Province the city belongs to |
| `Policy_Month` | Month the city's province first received the central environmental inspection (`YYYY-MM`) |
| `DID` | Post-treatment indicator: `1` if `year_month` ≥ `Policy_Month`, else `0` (staggered DiD) |

`Policy_Month` takes the values 2016-01, 2016-07, 2016-11, 2017-04, and 2017-08, corresponding
to the staggered rollout batches of the central environmental protection inspection across the
six provinces.

---

## Data sources

<!-- TODO (author): replace the placeholders below with the exact sources and access dates. -->

- **Air quality (AQI, PM2.5):** 〈e.g., China National Environmental Monitoring Centre (CNEMC) /
  national real-time air-quality release platform〉. Accessed 〈date〉.
- **Meteorology (Temperature, Pressure, WindSpeed, Precipitation):** 〈e.g., China Meteorological
  Administration / NOAA station data〉. Accessed 〈date〉.
- **Policy dates (`Policy_Month`):** official announcements of the central environmental
  protection inspection batches, 〈source / official document〉.

Monthly values were aggregated from the raw 〈daily/hourly〉 records by 〈arithmetic mean〉.

---
