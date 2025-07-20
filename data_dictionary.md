# Data Dictionary for Cost-Tier Comparison Project

## Overview
This document provides detailed information about the sensor data collected from nodes 3 and 5 for comparing low-cost, mid-cost, and high-cost air quality sensors.

**Data Collection Period:** April 16, 2025 to July 16, 2025

**Sensor Co-location:** All sensors are positioned within less than 1 meter of each other to ensure comparable measurements.

**Location Information:**
- **Node 3**: QMUL Mile End Road (51.522530, -0.042155) - co-located with TH2 reference station
- **Node 5**: King Edward Memorial Park (51.509477, -0.050541) - co-located with TH7 reference station
- **Environment**: Both locations are roadside urban traffic sites 

**Data Collection Frequencies:**
- **Low-cost and Mid-cost sensors**: 30 seconds
- **High-cost sensors (reference stations)**: 15 minutes
- **No resampling applied** - data preserved at original frequencies

**Missing Values:** Data is downloaded with original timestamps from database. Missing values occur naturally due to sensor interruptions and are preserved as gaps in the time series rather than filled with NaN.

**Timestamp Format:** All CSV files use London time (GMT/BST) with separate date and time columns:
- **Date format**: `YYYY-MM-DD` (e.g., `2025-04-15`)
- **Time format**: `HH:MM:SS` (e.g., `14:40:42`)
- **Timezone**: Europe/London (automatically handles GMT/BST transitions)

## CSV Files Structure
Each measurement type has its own CSV file within each cost tier folder:

**Low-cost sensors:**
- `node_3/low_cost/temperature.csv`
- `node_3/low_cost/humidity.csv`
- `node_3/low_cost/pm2_5.csv`
- etc.

**Mid-cost sensors (multi-column format):**
- `node_3/mid_cost/co_alphasense.csv` (op1_raw, op1_voltage, op2_raw, op2_voltage)
- `node_3/mid_cost/no2_alphasense.csv` (op1_raw, op1_voltage, op2_raw, op2_voltage)
- `node_3/mid_cost/ozone_alphasense.csv` (op1_raw, op1_voltage, op2_raw, op2_voltage)

**High-cost sensors:**
- `node_3/high_cost/no2.csv`
- `node_3/high_cost/pm2_5.csv`

## Column Descriptions

### Standard Columns

**Low-cost and High-cost sensors:**
- **`date`**: Date in YYYY-MM-DD format (London time)
- **`time`**: Time in HH:MM:SS format (London time)
- **`value`**: Sensor measurement value

**Mid-cost sensors (Alphasense):**
- **`date`**: Date in YYYY-MM-DD format (London time)
- **`time`**: Time in HH:MM:SS format (London time)
- **`op1_raw`**: Working electrode raw ADC value (0-65535)
- **`op1_voltage`**: Working electrode voltage (0-6144 mV)
- **`op2_raw`**: Auxiliary electrode raw ADC value (0-65535)
- **`op2_voltage`**: Auxiliary electrode voltage (0-6144 mV)

### Common Columns in All Files
| Column | Description | Data Type | Format | Example |
|--------|-------------|-----------|--------|---------|
| date | Date of measurement | String | YYYY-MM-DD | 2025-04-15 |
| time | Time of measurement | String | HH:MM:SS | 14:40:42 |
| value | Sensor measurement value | Numeric | Varies by sensor | 23.45 |

## Low-Cost Sensors (nodes 3 and 5)

### Environmental Measurements

#### Temperature (temperature.csv)
| Property | Value |
|----------|-------|
| **Sensor** | SHT45 (Sensirion) |
| **Units** | Degrees Celsius (°C) |
| **Range** | -40 to +125°C (sensor specification) |
| **Precision** | 2 decimal places |
| **Frequency** | 30 seconds |

#### Humidity (humidity.csv)
| Property | Value |
|----------|-------|
| **Sensor** | SHT45 (Sensirion) |
| **Units** | Percentage (%) |
| **Range** | 0 to 100% (sensor specification) |
| **Precision** | 2 decimal places |
| **Frequency** | 30 seconds |

### Particle Measurements

#### PM2.5 (particles_pm2_5.csv)
| Property | Value |
|----------|-------|
| **Sensor** | SPS30 (Sensirion) |
| **Units** | Micrograms per cubic meter (µg/m³) |
| **Range** | 0 to 1000 µg/m³ (sensor specification) |
| **Precision** | ±10% (sensor specification) |
| **Frequency** | 30 seconds |

#### PM10 (particles_pm10.csv)
| Property | Value |
|----------|-------|
| **Sensor** | SPS30 (Sensirion) |
| **Units** | Micrograms per cubic meter (µg/m³) |
| **Range** | 0 to 1000 µg/m³ (sensor specification) |
| **Precision** | ±10% (sensor specification) |
| **Frequency** | 30 seconds |

### Gas Measurements (Low-Cost)

#### Carbon Monoxide (co_raw.csv)
| Property | Value |
|----------|-------|
| **Sensor** | Grove Multichannel Gas v2 (GM702B) |
| **Units** | Raw sensor value |
| **Range** | 0 to 999 (sensor library limitation) |
| **Precision** | Integer |
| **Frequency** | 30 seconds |
| **Notes** | Requires calibration for ppm conversion |

#### Nitrogen Dioxide (no2_raw.csv)
| Property | Value |
|----------|-------|
| **Sensor** | Grove Multichannel Gas v2 (GM102B) |
| **Units** | Raw sensor value |
| **Range** | 0 to 999 (sensor library limitation) |
| **Precision** | Integer |
| **Frequency** | 30 seconds |
| **Notes** | Requires calibration for ppb conversion |

#### Ozone (ozone_raw.csv)
| Property | Value |
|----------|-------|
| **Sensor** | MQ131 (Winsen) |
| **Units** | Raw ADC value |
| **Range** | 0 to 65535 (16-bit ADC) |
| **Precision** | Integer |
| **Frequency** | 30 seconds |
| **Notes** | Requires calibration for ppm conversion. Connected via ADS1115 ADC |

#### VOC Index (voc.csv)
| Property | Value |
|----------|-------|
| **Sensor** | SGP40 (Sensirion) |
| **Units** | VOC Index |
| **Range** | 0 to 500 (sensor specification) |
| **Precision** | Integer |
| **Frequency** | 30 seconds |
| **Notes** | Temperature and humidity compensated |

## Mid-Cost Sensors (Alphasense - nodes 3 and 5)

### Electrochemical Gas Sensors

**Technical Overview:**
Alphasense electrochemical sensors use a **4-electrode configuration** for accurate gas detection:

- **OP1 (Working Electrode)**: Primary sensing electrode that responds to the target gas concentration. This electrode generates a current proportional to the gas concentration.
- **OP2 (Auxiliary/Counter Electrode)**: Reference electrode used for temperature compensation and baseline correction. It experiences the same environmental conditions but is not exposed to the target gas.

**Why Both Electrodes?**
- **Temperature Compensation**: Environmental temperature affects both electrodes similarly, allowing for compensation
- **Baseline Drift Correction**: The difference (OP1 - OP2) removes common-mode interference and sensor drift
- **Improved Accuracy**: Dual-electrode configuration significantly improves measurement precision compared to single-electrode sensors

**Data Processing**: For accurate gas concentration, you can use either format:

**Gas Concentration Calculation:**
```
Gas Concentration = (OP1_voltage - OP2_voltage) × Sensitivity_Factor
```

**Where:**
- **OP1_voltage**: Working electrode voltage (mV)
- **OP2_voltage**: Auxiliary electrode voltage (mV)  
- **Sensitivity_Factor**: Alphasense calibration constant (mV/ppm or mV/ppb)


#### CO Alphasense (co_alphasense.csv)
| Property | Value |
|----------|-------|
| **Sensor** | Alphasense CO-B4 |
| **Columns** | date, time, op1_raw, op1_voltage, op2_raw, op2_voltage |
| **Units** | Raw ADC (0-65535), Voltage (0-6144 mV) |
| **Precision** | Integer (raw), 5 decimals (voltage) |
| **Frequency** | 30 seconds |
| **Notes** | Multi-column format with both raw ADC and voltage values |

#### NO2 Alphasense (no2_alphasense.csv)
| Property | Value |
|----------|-------|
| **Sensor** | Alphasense NO2-B43F |
| **Columns** | date, time, op1_raw, op1_voltage, op2_raw, op2_voltage |
| **Units** | Raw ADC (0-65535), Voltage (0-6144 mV) |
| **Precision** | Integer (raw), 5 decimals (voltage) |
| **Frequency** | 30 seconds |
| **Notes** | Multi-column format with both raw ADC and voltage values |

#### Ozone Alphasense (ozone_alphasense.csv)
| Property | Value |
|----------|-------|
| **Sensor** | Alphasense OX-B431 |
| **Columns** | date, time, op1_raw, op1_voltage, op2_raw, op2_voltage |
| **Units** | Raw ADC (0-65535), Voltage (0-6144 mV) |
| **Precision** | Integer (raw), 5 decimals (voltage) |
| **Frequency** | 30 seconds |
| **Notes** | Multi-column format with both raw ADC and voltage values |

## High-Cost Sensors (Government Reference Stations)

### TH2 Station (co-located with Node 3)

#### NO2 Reference (no2.csv)
| Property | Value |
|----------|-------|
| **Station** | Tower Hamlets TH2 (DEFRA/AURN) |
| **Units** | Micrograms per cubic meter (µg/m³) |
| **Range** | TBD (reference station specification) |
| **Precision** | As reported by station |
| **Frequency** | 15 minutes |
| **QA/QC** | Continuous calibration and validation |

#### PM2.5 Reference (pm2_5.csv)
| Property | Value |
|----------|-------|
| **Station** | Tower Hamlets TH2 (DEFRA/AURN) |
| **Units** | Micrograms per cubic meter (µg/m³) |
| **Range** | TBD (reference station specification) |
| **Precision** | As reported by station |
| **Frequency** | 15 minutes |
| **QA/QC** | Continuous calibration and validation |

### TH7 Station (co-located with Node 5)

#### NO2 Reference (no2.csv)
| Property | Value |
|----------|-------|
| **Station** | Tower Hamlets TH7 (DEFRA/AURN) |
| **Units** | Micrograms per cubic meter (µg/m³) |
| **Range** | TBD (reference station specification) |
| **Precision** | As reported by station |
| **Frequency** | 15 minutes |
| **QA/QC** | Continuous calibration and validation |

#### PM2.5 Reference (pm2_5.csv)
| Property | Value |
|----------|-------|
| **Station** | Tower Hamlets TH7 (DEFRA/AURN) |
| **Units** | Micrograms per cubic meter (µg/m³) |
| **Range** | TBD (reference station specification) |
| **Precision** | As reported by station |
| **Frequency** | 15 minutes |
| **QA/QC** | Continuous calibration and validation |

## Data Quality and Processing Notes

### Temporal Information
- **Low/Mid-cost Frequency**: 30 seconds
- **High-cost Frequency**: 15 minutes  
- **Time Zone**: All timestamps in UTC
- **Period**: April 16, 2025 to July 16, 2025

### Data Processing
- **Missing Values**: Original timestamps preserved from database without artificial gap filling
- **No Resampling**: Data preserved at original collection frequencies and timestamps
- **Quality Control**: Basic sensor validation applied
- **Temporal Integrity**: Natural gaps due to sensor interruptions are preserved

### Calibration Status
- **Low-cost**: Factory calibration only, may require field correction
- **Mid-cost**: Raw readings, require post-processing with calibration curves
- **High-cost**: Fully calibrated and QA/QC validated reference measurements
