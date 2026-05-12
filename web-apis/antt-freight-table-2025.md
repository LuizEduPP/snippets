---
tags: ["python", "data", "antt", "freight", "logistics"]
---
# ANTT Freight Rate Table — Brazil 2025

A structural data dictionary containing the official 2025 ANTT (Brazilian Land Transportation Agency) freight reference values. It is heavily utilized as a structured JSON/Python standard data source for logistical calculation systems.

## 🛠️ How it works under the hood

The system builds access via layered nested associative arrays (dictionaries).
- **First Level**: Operational modality (e.g., `full_load`).
- **Second Level**: Physical cargo type (e.g., `general cargo`).
- **Third Level**: Axle configuration (e.g., `5`).

Each lookup resolves to a tuple holding:
1. `ccd`: Distance-based load reference cost (BRL per km)
2. `cc`: Trip-based fixed load cost (BRL)

---

## 🚀 Usage Guide

```python
# The underlying data structure loaded into memory:
ANTT_2025 = {
    'full_load': {
        'general cargo': {
            2: {'ccd': 2.34, 'cc': 150.0},
            3: {'ccd': 3.10, 'cc': 210.0},
            4: {'ccd': 4.05, 'cc': 285.0},
            5: {'ccd': 5.25, 'cc': 355.0},
            6: {'ccd': 6.15, 'cc': 430.0},
            7: {'ccd': 7.30, 'cc': 510.0},
            9: {'ccd': 8.95, 'cc': 635.0},
        },
        'bulk solid': {
            5: {'ccd': 5.10, 'cc': 330.0}
            # Other axles omitted for brevity...
        }
    }
}

def calculate_estimated_freight(modality: str, cargo: str, axles: int, distance_km: float) -> float:
    try:
        table = ANTT_2025[modality][cargo][axles]
        
        # Freight = (cost_per_km * total_distance) + base_fee
        freight = (table['ccd'] * distance_km) + table['cc']
        return freight
        
    except KeyError:
        print("❌ Error: Invalid modality, cargo format, or axle count requested.")
        return 0.0

if __name__ == "__main__":
    distance = 800  # km
    est_value = calculate_estimated_freight('full_load', 'general cargo', 5, distance)
    
    if est_value > 0:
         print(f"💰 Estimated freight cost: R$ {est_value:.2f}")
```
