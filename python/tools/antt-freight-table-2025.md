---
tags: ["python", "tools", "antt", "freight"]
---
# ANTT Freight Rate Table — Brazil 2025

Python dictionary with the official 2025 ANTT (Brazilian Land Transportation Agency) freight reference values, organized by transport modality, cargo type, and axle count.

Useful as a data source for freight calculation systems.

## Structure

```
ANTT_2025[modality][cargo_type][axles] → { ccd, cc }
```

| Key | Description |
|-----|-------------|
| `ccd` | Distance-based reference cost (R$/km) |
| `cc` | Load-based reference cost (R$ per trip) |
| `axles` | Number of vehicle axles: `2`, `3`, `4`, `5`, `6`, `7`, or `9` |

## Usage example

```python
axles = 5
cargo = 'general cargo'
distance_km = 800

table = ANTT_2025['full_load'][cargo][axles]
freight = table['ccd'] * distance_km + table['cc']
print(f"Estimated freight: R$ {freight:.2f}")
# Estimated freight: R$ 5097.32
```

## Cargo types available (under `full_load`)

- `bulk solid`
- `bulk liquid`
- `refrigerated or heated`
- `containerized`
- `general cargo`
- `neo-bulk`
- `hazardous bulk solid`
- `hazardous bulk liquid`
- `hazardous refrigerated or heated`
- `hazardous containerized`
- `hazardous general cargo`
- `pressurized bulk`

## Code

```python
ANTT_2025 = {
    'full_load': {
        'bulk solid': {
            2: {'ccd': 3.7421, 'cc': 413.06},
            3: {'ccd': 4.7423, 'cc': 503.16},
            4: {'ccd': 5.4133, 'cc': 547.19},
            5: {'ccd': 5.7673, 'cc': 503.06},
            6: {'ccd': 6.4431, 'cc': 534.98},
            7: {'ccd': 7.3863, 'cc': 729.94},
            9: {'ccd': 8.3346, 'cc': 782.50},
        },
        'bulk liquid': {
            2: {'ccd': 3.7975, 'cc': 420.01},
            3: {'ccd': 4.8140, 'cc': 514.58},
            4: {'ccd': 5.6223, 'cc': 588.12},
            5: {'ccd': 5.9126, 'cc': 526.44},
            6: {'ccd': 6.5789, 'cc': 555.76},
            7: {'ccd': 7.5406, 'cc': 755.80},
            9: {'ccd': 8.4986, 'cc': 811.04},
        },
        'refrigerated or heated': {
            2: {'ccd': 4.3949, 'cc': 470.77},
            3: {'ccd': 5.5382, 'cc': 563.73},
            4: {'ccd': 6.4295, 'cc': 641.71},
            5: {'ccd': 6.8793, 'cc': 597.75},
            6: {'ccd': 7.6390, 'cc': 623.07},
            7: {'ccd': 8.8913, 'cc': 903.05},
            9: {'ccd': 9.9944, 'cc': 961.91},
        },
        'containerized': {
            2: {'ccd': 4.8151, 'cc': 523.18},
            3: {'ccd': 5.3495, 'cc': 529.65},
            4: {'ccd': 5.6974, 'cc': 483.84},
            5: {'ccd': 6.3669, 'cc': 514.02},
            6: {'ccd': 7.4249, 'cc': 740.55},
            7: {'ccd': 8.2864, 'cc': 769.24},
        },
        'general cargo': {
            2: {'ccd': 3.7116, 'cc': 404.67},
            3: {'ccd': 4.7063, 'cc': 493.25},
            4: {'ccd': 5.3919, 'cc': 541.33},
            5: {'ccd': 5.7491, 'cc': 498.04},
            6: {'ccd': 6.4328, 'cc': 532.13},
            7: {'ccd': 7.3819, 'cc': 728.74},
            9: {'ccd': 8.3597, 'cc': 789.41},
        },
        'neo-bulk': {
            2: {'ccd': 3.3596, 'cc': 404.67},
            3: {'ccd': 4.7056, 'cc': 493.06},
            4: {'ccd': 5.4037, 'cc': 544.57},
            5: {'ccd': 5.7402, 'cc': 495.60},
            6: {'ccd': 6.4258, 'cc': 530.22},
            7: {'ccd': 7.4215, 'cc': 739.60},
            9: {'ccd': 8.3528, 'cc': 787.50},
        },
        'hazardous bulk solid': {
            2: {'ccd': 4.4451, 'cc': 547.62},
            3: {'ccd': 5.4453, 'cc': 637.73},
            4: {'ccd': 6.1625, 'cc': 689.83},
            5: {'ccd': 6.5166, 'cc': 645.70},
            6: {'ccd': 7.1923, 'cc': 677.62},
            7: {'ccd': 8.1635, 'cc': 880.27},
            9: {'ccd': 9.1412, 'cc': 940.93},
        },
        'hazardous bulk liquid': {
            2: {'ccd': 4.5121, 'cc': 566.04},
            3: {'ccd': 5.5286, 'cc': 660.62},
            4: {'ccd': 6.3530, 'cc': 742.24},
            5: {'ccd': 6.6433, 'cc': 680.55},
            6: {'ccd': 7.3096, 'cc': 709.88},
            7: {'ccd': 8.2993, 'cc': 917.61},
            9: {'ccd': 9.2867, 'cc': 980.95},
        },
        'hazardous refrigerated or heated': {
            2: {'ccd': 4.9455, 'cc': 570.02},
            3: {'ccd': 6.0888, 'cc': 662.98},
            4: {'ccd': 7.0111, 'cc': 751.48},
            5: {'ccd': 7.4609, 'cc': 707.52},
            6: {'ccd': 8.2206, 'cc': 732.84},
            7: {'ccd': 9.5092, 'cc': 1022.80},
            9: {'ccd': 10.6506, 'cc': 1092.20},
        },
        'hazardous containerized': {
            2: {'ccd': 5.1524, 'cc': 611.30},
            3: {'ccd': 5.7330, 'cc': 625.86},
            4: {'ccd': 6.0809, 'cc': 580.04},
            5: {'ccd': 6.7504, 'cc': 610.22},
            6: {'ccd': 7.8364, 'cc': 844.45},
            7: {'ccd': 8.7273, 'cc': 881.24},
        },
        'hazardous general cargo': {
            2: {'ccd': 4.0488, 'cc': 492.80},
            3: {'ccd': 5.0436, 'cc': 581.37},
            4: {'ccd': 5.7754, 'cc': 637.53},
            5: {'ccd': 6.1326, 'cc': 594.24},
            6: {'ccd': 6.8162, 'cc': 628.33},
            7: {'ccd': 7.7934, 'cc': 832.63},
            9: {'ccd': 8.8006, 'cc': 901.40},
        },
        'pressurized bulk': {
            2: {'ccd': 6.0407, 'cc': 578.22},
            3: {'ccd': 6.7779, 'cc': 627.03},
            4: {'ccd': 8.7789, 'cc': 904.69},
        },
    },
}
```

> Source: ANTT Resolution nº 6.442/2025
