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
  - Most forests in North America are in some stage of recovery [@pan_2010_age] and are rapidly aging [@radeloff_2012_economic]
  - Midwest -- Regional disturbances transitioning from severe, stand-replacing events to more moderate disturbances (partial defoliation; loss of selected species) [@pregitzer_2004_carbon,@birdsey_2006_forest,@williams_2012_carbon]
	- Review of disturbance effects on North America -- [@hicke_2011_effects]
  - Part of larger global trend -- moderate disturbances are on the rise [@allen_2010_global]
- Productivity theory vs. observations
  - "Traditional" ecology theory (e.g. Odum) predicts NPP should decline with succession
    - See figure 3 in [Gough et al. 2016 Ecosphere](https://esajournals.onlinelibrary.wiley.com/doi/abs/10.1002/ecs2.1375).
  - But many recent observations, from here (Gough, Hardiman) and elsewhere (citations therein) suggest that NPP may be stable through succession in hardwood forests
  - Possible explanation is that higher canopy complexity improves resource (especially light, nitrogen) use efficiency, which stabilizes productivity
  - Part of a bigger-picture trend on biodiversity-productivity relationship in terrestrial ecosystems
- Lots of observational work on composition, but less work on modeling
  - Why model? Allow exploration of mechanisms, and projection into future. Implications for global carbon cycle.
    - Testing theoretical models of disturbance response mechanisms is important [@foster_2016_integrating]
  - Few studies that _have_ modeled this have shown that canopy complexity can improve productivity 
  - ...but, these studies do not model long time series, and are not full models of vegetation dynamics and biogeochemical cycling
  - [@bond-lamberty_2015_moderate] test whether we can get the response. They found they cannot. Here, we test if the models can even reproduce the state.
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
  - Secondary successional forest -- bigtooth aspen (/Populus grandidentata/), northern red oak (/Quercus rubra/), red maple (/Acer rubrum/), paper birch (/Betula papyrifera/), eastern white pine (/Pinus strobus/)
  - Average age -- 95 years (2013)
  - NEP in UMBS tower is 1.58 MG C ha-1 yr-1 (0.80-1.98) (1999-2006), but with landscape variation
  - Heavily logged in late 1800s and early 1900s, disturbed by fire until 1923
  - Present day composition typical of upper Great Lakes region
	- Previously, the site of the FASET experiment [@gough_2013_sustained; @gough_2008_multi]
- Model selection
  - OBJECTIVE: Pick models based on hypotheses. Looking for:
    - Competition within a patch -- i.e. big leaf vs. gap models
      - Big-leaf: SIPNET (PEcAn), Biome-BGC
      - Gap models: ED2 (PEcAn), CLM-FATES (PEcAn?), ZELIG, [SIBBORK](https://github.com/SIBBORK/SIBBORK), LINKAGES (PEcAn), Biome-ESS
    - Sophisticated canopy radiative transfer -- i.e. Beer's law exponential decline vs. finite canopy gap (3D heterogeneity?)
      - If there aren't good models that fit this bill, might be worth modifying/enhancing the radiative transfer scheme of one of the models.
	- Dynamic N allocation -- models with vs. without trait plasticity?
  - Some candidate models:
    - SIPNET (PEcAn) 
      - Big leaf
      - No RTM
      - Fixed traits
      - Subdaily fluxes; only one PFT (at a time)
    - DALEC (PEcAn)
      - Big leaf
      - No RTM
    - MAESPA (PEcAn)
      - Sophisticated leaf hydraulics (developed by Belinda Medlyn)
    - Biome-BGC
      - Big leaf
      - No RTM
      - N redistribution
      - PFTs?
    - ED2 (PEcAn)
      - Cohort-based gap model
      - Multiple RTM options -- multi-level two-stream, optional finite canopy radius
      - Can toggle N cycle. Recent commit adds optional trait plasticity, but not sure which traits.
      - PFTs, but with successional distinction. Possibly extensible to species via hacks.
    - CLM (PEcAn?)
      - Big leaf
      - Two-layer RTM (sun vs. shade), two-stream approximation
    - CLM-FATES (PEcAn?)
      - CLM internals with ED2 cohort structure (and RTM?)
    - LINKAGES (PEcAn)
      - Individual gap model
      - Annual time step (designed for paleo-ecology)
    - ZELIG
      - Individual gap model
    - SIBBORK
      - Individual gap model
      - Sophisticated 3D canopy RTM?
    - Biome-ESS
      - Individual gap model
- Calibration and parameterization datasets
  - TRY database for parameters
  - Local site surveys
  - Flux tower
  - Consider the parameters from Table 2 in [@bond-lamberty_2015_moderate]
- Model execution
  - Start from common initial conditions (pools and, where appropriate, composition) ~1900
  - Common parameters (based on TRY, etc.)
  - (1) Simple run (ensemble?) 1900 to present. Compare against flux tower time series and composition.
  - (2) Calibrate (parameter data assimilation) against flux tower time series (no composition). Run again and validate.
    - Use Istem's model emulator.
  - (3) Calibrate against composition (no flux tower). Run again and validate.
  - (4) Calibrate against both. Run again and validate.
- Comparisons
  - UMBS site data
  - Results of [@bond-lamberty_2015_moderate]
  
## Additional notes

- (Ben) Maybe pull CMIP5 data for Great Lakes / UMBS grid cell and look at trajectories over time - could be a discussion figure
- (Ben) Could also calibrate against UMBS chronosequence data - longer term albeit less precise than flux tower
- [@bond-lamberty_2015_moderate] -- Radiative transfer is important to capturing resilience to disturbance. Beer's law formulations are insufficient.
  - In ED, increase in light unable to trigger understory light response. Perhaps because canopy is still closed (i.e. no gaps)? What if we tried the finite canopy radius model?
- Look at physical variables as well where possible -- e.g. canopy light environment, temperature, albedo
- Nature of the disturbance regime shapes the course of evolution, including in the tropics [@pennington_2015_contrasting]
- Model uncertainties more important at longer time scales (sampling more important at short time-scales), with mortality as the main driver of model uncertainty [@melo_2018_estimating]

