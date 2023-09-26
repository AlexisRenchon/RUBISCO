---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Welcome to Slidev
---

# An introduction to ClimaLSM.jl

Alexandre A. Renchon, Katherine Deck, Renato Braghiere, Julia Sloan, Edward Speer

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
I will present CliMA land surface model and go in more details for our SOC implementation
-->

---

# Background #1: CliMA ESM

- [clima.caltech.edu](https://clima.caltech.edu)
- [github.com/CliMA](https://github.com/CliMA)
<br>
<br>

- Data assimilation & AI "A step change in the accuracy and usability of climate predictions"
- Scalable and modular
- Ecosystem of front-end apps

<div grid="~ cols-2 gap-2" m="-t-2">

<img src="images/test.png">

</div>

---

# Background #2: CliMA LSM 

- CliMA/land
<div grid="~ cols-2 gap-2" m="-t-2">

<img src="images/CliMAland.png">

</div>

<br>

- **CliMA/ClimaLSM.jl**
	- Coupled to atmosphere
	- Early development

---

# Background #3: An ESM 100% written in Julia

- Modern, fast, dynamic, open-source, reproducible, composable
- Great for GPU and AI
- No call between programming languages
<br>
<br>
- [julialang.org](https://julialang.org/)

---

# ClimaLSM.jl design #1: standalone and integrated  

- Each submodel can be run independently (e.g., soil CO2)
- Example below: constant rain, free drainage 
	- submodels: 
		- energy (latent & sensible heat) 
		- hydrology (prognostic moisture) 
		- biogeochemistry (prognostic co2: production & diffusion)

<div grid="~ cols-1 gap-2" m="-t-2">

<video width="320" height="240" controls>
  <source src="images/time_animation2.mp4" type="video/mp4">
</video>

</div>

---
layout: iframe-right
url: https://clima.github.io/ClimaLSM.jl/previews/PR214/dynamicdocs/pages/soil_biogeochemistry/microbial_respiration/
scale: 0.4 
---

# ClimaLSM.jl design #2: clear documentation 

- 100s of web apps to facilitate communication 
- Equations for parameterisation and prognostic variables
- Table of variable with name, symbol, units and typical range
<br>
<br>
- Delta SOC = input (litterfall, root exudates) - output (heterotrophic respiration, export)
- Prognostic: Water, SOC, CO2, O2
- Discretised soil layers but only one SOM pool 

---

# ClimaLSM.jl design #3: modularity

- Julia multiple dispatch allow to easily swap between submodels
- E.g., soil biogeochemistry:
	- Dual Arrhenius Michaelis Menten
	- CENTURY
	- Heterogeneous kinetics

---

# ClimaLSM.jl design #4: accessibility

- Web app to run single site, producing visualisation & output file
- Example below: prototype with ozark data, and g1 parameter
- Future widgets: domain, timestepper, parameters

<div grid="~ cols-2 gap-2" m="-t-2">

<img src="images/ClimaLSMwebapp.png">

</div>

---
layout: iframe-right
url: https://cupoftea.earth/menu2/
scale: 0.4 
---

# ClimaLSM.jl design #5: ModEx: emergent pattern at scales

- E.g., at ecosystem scale, ecosystem respiration optimal moisture
- Do LSM capture this? (where, when, PFT, ...)
- Multiple other example: Topt of ER, GPP, Gs vs. SWC, VPD, ...
- Stay up-to-date with data and model dev, versioning

---

# ClimaLSM.jl next steps

- Test our parameterisation scheme
	- can we perform better than other LSM at Flux sites, despite simpler model?
- Global run (currently, only single site)
- Couple ClimaLSM.jl to the atmosphere
<br>
<br>
- Manuscript ClimaLSM.jl vs FLUXNET, structure, design, modularity, parameterisation, docs, tutorials, web apps, emergent pattern
