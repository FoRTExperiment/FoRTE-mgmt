---
title: FoRTE project paper ideas
---

# Can models reproduce trends in Midwestern forest productivity?

Potential journals:

- AGU -- Geophysical Research Letters, JGR-Biogeosciences
- ESA journals -- Ecology, Ecological Applications, Ecological Monographs
- PNAS
- Global Change Biology

## Introduction

- Background on Midwestern forest ecology/composition
  - Cleared around turn of 19th century
  - Dominated in many places by early-successional species (birch, aspen)
  - Recently, early-successional species declining and slowly replaced by mid-successional (maple, oak, pine)
- Productivity theory vs. observations
  - "Traditional" ecology theory (e.g. Odum) predicts NPP should decline with succession
	- See figure 3 in [Gough et al. 2016 Ecosphere](https://esajournals.onlinelibrary.wiley.com/doi/abs/10.1002/ecs2.1375).
  - But many recent observations, from here (Gough, Hardiman) and elsewhere (citations therein) suggest that NPP may be stable through succession in hardwood forests
  - Possible explanation is that higher canopy complexity improves resource (especially light, nitrogen) use efficiency, which stabilizes productivity
  - Part of a bigger-picture trend on biodiversity-productivity relationship in terrestrial ecosystems
- Lots of observational work on composition, but less work on modeling
  - Why model? Allow exploration of mechanisms, and projection into future. Implications for global carbon cycle.
  - Few studies that _have_ modeled this have shown that canopy complexity can improve productivity 
  - ...but, these studies do not model long time series, and are not full models of vegetation dynamics and biogeochemical cycling
- Research questions:
  - Which models (if any) can reproduce trends in productivity from ~1900 to present?
	- Can models be trained (i.e. parameterized) to fit productivity trends? How realistic are the resulting parameters?
  - Same thing for trends in composition.
  - Does calibrating/assimilating/forcing models to reproduce composition better capture trends in productivity?
  - What are the characteristics of models that can reproduce both?
- Hypotheses:
  - To capture the NPP-composition relationship, models need all of the following:
    - (1) At least cohort-level competition within a patch
    - (2) Canopy radiative transfer scheme that allows some fraction of direct light to penetrate into the understory, and where this is linked to productivity
	  - (Ben) What about a Nitrogen cycle? Good hypothesis.

## Methods

- Site -- UMBS and surroundings
- Model selection
  - Simple "box" biogeochemical models
    - SIPNET -- subdaily fluxes, but one PFT at a time
  - Cohort-level models
    - ED2 -- with and without finite canopy radius model
	- CLM-FATES?
  - Individual gap models
    - LINKAGES
    - Biome-ESS?
- Calibration and parameterization datasets
  - TRY database for parameters
  - Local site surveys
  - Flux tower
- Model execution
  - Start from common initial conditions (pools and, where appropriate, composition) ~1900
  - Common parameters (based on TRY, etc.)
  - (1) Simple run (ensemble?) 1900 to present. Compare against flux tower time series and composition.
  - (2) Calibrate (parameter data assimilation) against flux tower time series (no composition). Run again and validate.
    - Use Istem's model emulator.
  - (3) Calibrate against composition (no flux tower). Run again and validate.
  - (4) Calibrate against both. Run again and validate.
  
## Additional notes

- (Ben) Maybe pull CMIP5 data for Great Lakes / UMBS grid cell and look at trajectories over time - could be a discussion figure
- (Ben) Could also calibrate against UMBS chronosequence data - longer term albeit less precise than flux tower
