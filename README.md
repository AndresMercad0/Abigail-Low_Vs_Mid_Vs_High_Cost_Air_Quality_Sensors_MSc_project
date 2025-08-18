# Air Quality Sensors Cost-Tier Comparison Study

## 📊 Project Overview

This repository contains data and documentation for Abigail's MSc project comparing the performance of **low-cost**, **mid-cost**, and **high-cost** air quality sensors. The study evaluates sensor accuracy, reliability, and cost-effectiveness across different price tiers for urban air quality monitoring.

## 🎯 Research Objectives

- Compare measurement accuracy between different cost tiers of air quality sensors
- Evaluate the cost-effectiveness of low and mid-cost sensors against reference-grade equipment
- Assess sensor performance in real-world urban traffic environments
- Provide recommendations for air quality monitoring network deployment strategies

## 📍 Study Locations

**Node 3**: QMUL Mile End Road (51.522530, -0.042155)
- Co-located with TH2 reference station
- Environment: Roadside - Urban Traffic

**Node 5**: King Edward Memorial Park (51.509477, -0.050541)
- Co-located with TH7 reference station  
- Environment: Roadside - Urban Traffic

## 📅 Data Collection Period

**April 16, 2025 - July 16, 2025** (3 months)

## 🔬 Sensor Categories

### Low-Cost Sensors (~£10-100)
- **Temperature/Humidity**: Sensirion SHT45
- **Particulate Matter**: Sensirion SPS30 (PM2.5, PM10)
- **Gas Sensors**: Grove Multichannel Gas Sensor v2 (CO, NO2)
- **Ozone**: Winsen MQ131
- **VOC**: Sensirion SGP40
- **Sampling Frequency**: 30 seconds

### Mid-Cost Sensors (~£100-500)
- **CO**: Alphasense CO-B4 (4-electrode electrochemical)
- **NO2**: Alphasense NO2-B43F (4-electrode electrochemical)
- **Ozone**: Alphasense OX-B431 (4-electrode electrochemical)
- **Sampling Frequency**: 30 seconds

### High-Cost Sensors (>£10,000)
- **Reference Stations**: DEFRA/AURN stations TH2 and TH7
- **NO2 & PM2.5**: Met One Instruments
- **Sampling Frequency**: 15 minutes
- **Quality Assurance**: Continuous calibration and validation

## 📁 Repository Structure

```
├── README.md                    # This file
├── .gitignore                   # Git ignore rules
├── data_dictionary.md           # Detailed data documentation
├── deployment_details.csv       # Sensor deployment information
├── sensor_specifications.csv    # Technical sensor specifications
├── node_3/                      # Data from QMUL Mile End Road
│   ├── low_cost/                # Low-cost sensor data
│   │   ├── temperature.csv
│   │   ├── humidity.csv
│   │   ├── particles_pm2_5.csv
│   │   ├── particles_pm10.csv
│   │   ├── co_raw.csv
│   │   ├── no2_raw.csv
│   │   ├── ozone_raw.csv
│   │   └── voc.csv
│   ├── mid_cost/               # Mid-cost sensor data
│   │   ├── co_alphasense.csv
│   │   ├── no2_alphasense.csv
│   │   └── ozone_alphasense.csv
│   └── high_cost/              # Reference station data
│       ├── no2.csv
│       └── pm2_5.csv
└── node_5/                     # Data from King Edward Memorial Park
    ├── low_cost/               # (Same structure as node_3)
    ├── mid_cost/
    └── high_cost/
```

## 📊 Data Format

### Timestamp Format
- **Date**: YYYY-MM-DD format
- **Time**: HH:MM:SS format  
- **Timezone**: Europe/London (GMT/BST)
- **Missing Values**: Preserved as gaps (no NaN filling)

### File Structure
Each CSV file contains:
- `date`: Date column (YYYY-MM-DD)
- `time`: Time column (HH:MM:SS)
- Measurement columns (varies by sensor type)

## 🔧 Data Processing Notes

- **No resampling applied** - data preserved at original collection frequencies
- **Co-location**: All sensors positioned within <1m of each other
- **Quality Control**: Reference station data includes continuous calibration
- **Raw Data**: Low-cost sensor data requires calibration for accurate units
- **Multi-column Format**: Mid-cost sensors provide raw voltages and processed values

## 📖 Documentation Files

- **`data_dictionary.md`**: Comprehensive data documentation with column descriptions, units, and processing notes
- **`deployment_details.csv`**: Sensor deployment locations and reference station information
- **`sensor_specifications.csv`**: Technical specifications for all sensors used

## 🚀 Getting Started

1. **Clone the repository**
2. **Read the data dictionary** (`data_dictionary.md`) for detailed column descriptions
3. **Check deployment details** for location and sensor information
4. **Load data** using your preferred analysis tool (Python pandas, R, etc.)

## 📋 Data Usage Guidelines

- Data is provided for research and educational purposes
- Reference the original study when using this dataset
- Consider calibration requirements for low-cost sensor data
- Account for different sampling frequencies when comparing sensors

## 🏫 Institution

**Queen Mary University of London**  
IoT2US Lab http://iot.eecs.qmul.ac.uk/  
School of Electronic Eng. & Comp. Sci.  

## 📧 Contact

**Andres A. Mercado-Velazquez**  
[a.mercadovelazquez@qmul.ac.uk](mailto:a.mercadovelazquez@qmul.ac.uk)  

---

*This dataset represents real-world air quality measurements from urban traffic environments in London, UK. The data supports research into cost-effective air quality monitoring solutions.*
