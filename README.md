# Extreme-Wind-Event-Prediction-Using-ERA5

Example code to access the [ERA5 dataset](https://cds.climate.copernicus.eu/datasets/reanalysis-era5-single-levels?tab=download)
```
import cdsapi

c = cdsapi.Client()
c.retrieve(
    'reanalysis-era5-single-levels',
    {
        'product_type': 'reanalysis',
        'format': 'netcdf',
        'variable': ['10m_u_component_of_wind', '10m_v_component_of_wind', 'mean_sea_level_pressure'],
        'year': '2023',
        'month': '01',
        'day': ['01', '02'],
        'time': [f'{h:02d}:00' for h in range(24)],
    ', 'era5_wind_data.nc')

```

## Possible architevtures we can use:
- LSTM / Bi-LSTM: For the Time-series forecasting
- CNN: Downscaling and feature extraction
- Hybrid (CNN & LSTM): Spacio-temporal prediction
- Quantile Random Forest(QRF): Structured data & baseline
- Transformers: Long-range dependencies

## Possible set of predictors we can use:
- 10m / 100m u-component of wind: Eastward wind speed.
- 10m / 100m v-component of wind: Northward wind speed.
- 10m wind gust since previous post-processing: Maximum 3-second wind at 10m; vital for detecting extreme turbulence.
- Surface sensible heat flux (SHF)
- Convective available potential energy (CAPE): Indicates atmospheric instability and potential for severe weather development.
- 2m temperature / Skin temperature: Affects air density and thermal stability.
- 2m dewpoint temperature: Used with temperature to calculate relative humidity and assess moisture content.
- Mean sea level pressure (MSLP): A primary driver of wind formation; pressure gradients directly impact wind speed.
- Boundary layer height: Represents the depth of the atmosphere most affected by surface friction and heat transfer.
- Surface pressure: Critical for local wind dynamics.
- Total precipitation: Often co-occurs with extreme wind events (e.g., in cyclones)
- Geopotential at surface (Orography): Essential for models to learn how terrain impacts wind speeds.
- Land-sea mask: Differentiates between surface roughness over water vs. land.
- Sub-gridscale orography (Slope, Anisotropy, etc.): Accounts for topographic features smaller than the model's 31km grid.
