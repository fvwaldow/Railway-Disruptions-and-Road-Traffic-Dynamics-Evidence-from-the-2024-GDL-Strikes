# Railway Disruptions and Road Traffic Dynamics: Evidence from the 2024 GDL Strikes

Frederik von Waldow

## Overview

This project quantifies how the German Train Drivers' Union (GDL) strikes of January–March 2024 shifted traffic from rail to road. Using hourly counting-station data from Germany's motorway and federal road network, it asks to what extent rail service disruptions produce measurable increases in road traffic, and how those effects vary by strike, road type, and transport purpose (passenger vs. freight).

The analysis separates strike effects from regular traffic rhythms with a two-part seasonal-trend decomposition: STL with a 24-hour period for daily cycles, followed by a Fourier regression on harmonics of a 168-hour cycle for weekly seasonality. Strike hours are excluded when fitting, so the fitted trend plus seasonal components serve as a counterfactual against which observed strike-period traffic is compared.

## Main findings

- Road traffic rose during all four strike windows, most strongly during the first strike in January: roughly 12–13% for freight and 4–9% for passenger vehicles.
- Effects were most pronounced on motorways, consistent with their role in absorbing diverted long-distance freight and regional commuting.
- Increases shrank across successive strikes, pointing to adaptation by travellers and logistics operators — and to the shorter duration of the March strikes.

## Data

None of the raw data is committed to this repository; only codebooks and figures are included under `data_road/`. To reproduce the analysis, download the following into `data_road/`:

| Source | Content | Expected path |
| --- | --- | --- |
| [BASt](https://www.bast.de/DE/Publikationen/Daten/Verkehrstechnik/DZ-Richtung.html) | Hourly directional traffic counts, Jan–Mar 2024, motorways (A) and federal roads (B), plus station metadata | `data_road/Roh_2024_A_S/`, `data_road/Roh_2024_B_S/` |
| [Geoportal](https://www.geoportal.de/Info/tk_03-bundesfernstrassennetz) | Federal trunk road network (GeoPackage) | `data_road/Daten-BISStra/BFStr_Netz_v2025q2.gpkg` |
| Eurostat `demo_r_pjangrp3` | State-level population, used for traffic intensity per capita | fetched at runtime via the `eurostat` package |

Strike windows are hard-coded in the notebook, with separate start and end times for freight and passenger services (freight strikes began several hours earlier in each case).

## Limitations

The decomposition uses aggregate traffic per station rather than station-specific seasonal and trend components, and does not control for weather, roadworks, or concurrent events — the black-ice event of 17 January 2024, visible as a sharp drop in the raw series, is one example of such confounding. Results should be read as a preliminary, descriptive assessment of mode substitution rather than a causal estimate.
