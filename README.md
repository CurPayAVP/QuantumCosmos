# CurPay Quantum Cosmos — Engine File Reference

> A file-by-file map of the **CurPay Quantum Cosmos** simulation engine — every source file grouped by
> subsystem, with a one-line description of its purpose. Use this as a navigation aid when exploring the
> codebase or onboarding new contributors.

<p align="left">
  <img alt=".NET" src="https://img.shields.io/badge/.NET-10.0-512BD4?logo=dotnet&logoColor=white">
  <img alt="Language" src="https://img.shields.io/badge/language-C%23-239120?logo=csharp&logoColor=white">
  <img alt="Language" src="https://img.shields.io/badge/language-Q%23-512BD4?logo=microsoftazure&logoColor=white">
  <img alt="Azure Quantum" src="https://img.shields.io/badge/Azure%20Quantum-0062FF?logo=microsoftazure&logoColor=white">
  <img alt="Docs" src="https://img.shields.io/badge/docs-engine%20reference-informational">
</p>

---

## 📑 Table of Contents

- [🧭 How to read this document](#-how-to-read-this-document)
- [🌌 Core Engine](#-core-engine-cosmosengine)
- [🪐 Entities](#-entities-cosmosentities)
- [📐 Physics](#-physics-cosmosphysics)
- [🔬 Subsystem Domains](#-subsystem-domains-cosmos)
  - [Binary Stars](#binary-stars-cosmosbinarystars)
  - [Continuum](#continuum-cosmoscontinuum)
  - [Disc Physics](#disc-physics-cosmosdiscphysics-cosmosdiscplanetinteraction)
  - [Planetary Systems & Formation](#planetary-systems--formation)
  - [Multi-Planet, Resonances, Secular, Tides](#multi-planet-resonances-secular-tides)
  - [Stellar Winds](#stellar-winds-cosmosstellarwinds)
  - [Supernova](#supernova-cosmossupernova)
- [🏗️ UniverseEngine](#️-universeengine)
  - [Planet Destruction](#planet-destruction-universeengineplanetdestruction)
  - [Planet Formation Regulation](#planet-formation-regulation-universeengineplanetformationregulation)
  - [Small Bodies](#small-bodies-universeenginesmallbodies)
  - [Stellar Remnants](#stellar-remnants-universeenginestellarremnants)
- [🧮 Realism-Enforcement Layer](#-realism-enforcement-layer-staged-physics-completeness)
  - [Conservation Ledgers](#conservation-ledgers-cosmosledgers)
  - [Stage 2 — FRW Cosmology](#stage-2--frw-cosmology-cosmoscosmology)
  - [Stage 3 — Thermodynamics](#stage-3--thermodynamics-cosmosthermodynamics)
  - [Stage 4 — Electromagnetism / Plasma](#stage-4--electromagnetism--plasma-cosmoselectromagnetism)
  - [Stage 5 — Dark Sector](#stage-5--dark-sector-cosmosdarksector)
  - [Stage 6 — Radiative Transfer](#stage-6--radiative-transfer-cosmosradiativetransfer)
  - [Stage 7 — Chemistry Network](#stage-7--chemistry-network-cosmoschemistry)
  - [Stage 8 — N-Body Dynamics](#stage-8--n-body-dynamics-cosmosnbody)
  - [Stage 9 — Initial Conditions](#stage-9--initial-conditions-cosmosinitialconditions)
- [🖥️ Hosting, Realtime, Controllers & App](#️-hosting-realtime-controllers--app)

---

## 🧭 How to read this document

- Files are grouped by their folder / subsystem. Paths are relative to the project root.
- Each subsystem is collapsible — click the ► triangle to expand it.
- The **Realism-Enforcement Layer** modules are *gated, additive* physics domains that sit on top of the
  live universe and route all mass/energy changes through the shared [conservation ledgers](#conservation-ledgers-cosmosledgers).

---

## 🌌 Core Engine (`Cosmos\Engine`)

| File | Purpose |
|---|---|
| `CosmosRng.cs` | Deterministic random-number source for the simulation. |
| `CosmosSimulation.cs` | Main simulation lifecycle, tick order, and conservation audits. |
| `CosmosSimulation.AngularMomentum.cs` | Angular-momentum bookkeeping and updates per tick. |
| `CosmosSimulation.BinaryStars.cs` | Binary/triple star evolution and ejecta reconciliation. |
| `CosmosSimulation.BlackHoles.cs` | Black-hole growth, evaporation, AGN feedback, motion, and rogue escape. |
| `CosmosSimulation.Continuum.cs` | Continuum gas exchange and jet-related gas return. |
| `CosmosSimulation.GalaxyMotion.cs` | Galaxy dynamics, tidal stripping, and ram-pressure gas stripping. |
| `CosmosSimulation.IntergalacticReintegration.cs` | Unified module ensuring intergalactic-medium events conserve mass/energy. |
| `CosmosSimulation.Life.cs` | Emergence and evolution of life/civilizations on planets. |
| `CosmosSimulation.PlanetDestruction.cs` | Planet destruction and mass-redistribution pipeline. |
| `CosmosSimulation.Planets.cs` | Planet evolution, tidal heating, Roche shredding, and rogue behavior. |
| `CosmosSimulation.SmallBodyDestruction.cs` | Small-body destruction, sublimation, and fallback mass bookkeeping. |
| `CosmosSimulation.StellarDeath.cs` | Star death channels, supernova enrichment, remnants, and nebula spawning. |
| `CosmosSimulation.StellarWinds.cs` | Stellar-wind feedback mass return to the ISM. |
| `CosmosSimulation.Structure.cs` | Galaxy/structure formation and leftover-gas handling. |
| `CosmosSimulation.Wormholes.cs` | Wormhole nucleation, entanglement, traversal, and pinch-off. |
| `EventLog.cs` | In-memory rolling cosmic event log with optional disk forwarding. |
| `EventLogPersister.cs` | Per-universe disk writer for cosmic event logs. |
| `MassLedger.cs` | Central single-threaded mass-flow mediator and conservation ledger. |
| `QrngStats.cs` | Statistics tracking for the quantum random-number generator. |
| `RealismConfig.cs` | Master switch and per-domain toggles for the realism-enforcement layer. |
| `SimConfig.cs` | Simulation configuration and tunable parameters. |
| `SimulationProfile.cs` | Named parameter presets/profiles for simulation runs. |
| `SimulationRuntime.cs` | Runtime state and control wiring for the running simulation. |

---

## 🪐 Entities (`Cosmos\Entities`)

| File | Purpose |
|---|---|
| `BlackHole.cs` | Black-hole entity data model. |
| `Civilization.cs` | Civilization/life entity data model. |
| `Galaxy.cs` | Galaxy entity data model. |
| `Particles.cs` | Particle/matter-stream entity definitions. |
| `Planet.cs` | Planet entity data model. |
| `Remnants.cs` | Nebula and compact-remnant entity definitions. |
| `SolarSystem.cs` | Solar-system container entity model. |
| `Star.cs` | Star entity data model. |
| `Universe.cs` | Top-level universe state and reservoir container. |

---

## 📐 Physics (`Cosmos\Physics`)

| File | Purpose |
|---|---|
| `GrPhysics.cs` | General-relativity physics calculations. |
| `PlanetaryPhysics.cs` | Planetary physical property and orbit calculations. |
| `QuantumPhysics.cs` | Quantum-scale physics including wormhole exotic-energy formulas. |
| `SimConstants.cs` | Shared physical and simulation constants. |
| `StellarPhysics.cs` | Stellar structure and evolution physics. |
| `Vec2.cs` | 2D vector math helper type. |

---

## 🔬 Subsystem Domains (`Cosmos\...`)

| File | Purpose |
|---|---|
| `AngularMomentum\AngularMomentum.cs` | Angular-momentum physics model. |
| `Chemistry\Chemistry.cs` | Chemical enrichment and composition tracking. |
| `CosmicRays\CosmicRays.cs` | Cosmic-ray generation and effects. |
| `Feedback\Feedback.cs` | Generic energy/feedback injection model. |
| `Hydrodynamics\Hydrodynamics.cs` | Fluid/gas hydrodynamics calculations. |
| `ISM\Ism.cs` | Interstellar-medium model. |
| `MHD\Mhd.cs` | Magnetohydrodynamics model. |
| `Neutrinos\Neutrinos.cs` | Neutrino production and transport. |
| `Radiation\Radiation.cs` | Radiation transport and cooling. |
| `StarFormation\StarFormation.cs` | Star-formation rate and triggering model. |
| `Quantum\QuantumRandom.cs` | Quantum random-number source. |

<details>
<summary><strong>Binary Stars</strong> (<code>Cosmos\BinaryStars</code>)</summary>

| File | Purpose |
|---|---|
| `BinaryDiagnostics.cs` | Diagnostic output for binary evolution. |
| `BinaryEvolutionPipeline.cs` | Orchestrates binary-star evolution steps. |
| `BinaryEvolutionSettings.cs` | Configuration for binary evolution. |
| `BinaryStarsServiceCollectionExtensions.cs` | DI registration for binary-star services. |
| `CommonEnvelope\CommonEnvelopeModel.cs` | Common-envelope phase model. |
| `Detection\BinaryClassifier.cs` | Classifies binary interaction types. |
| `Detection\BinaryInteractionTypes.cs` | Enum/type definitions for binary interactions. |
| `Detection\BinaryOrbitalElements.cs` | Orbital-element data for binaries. |
| `Detection\BinaryRegistry.cs` | Registry tracking active binaries. |
| `Detection\BinarySystem.cs` | Binary-system data model. |
| `Detection\TripleSystem.cs` | Triple-system data model. |
| `GravitationalWaves\GravitationalWaveInspiralModel.cs` | GW inspiral and mass-loss model. |
| `MassTransfer\AccretionModel.cs` | Accretion during mass transfer. |
| `MassTransfer\MassTransferModel.cs` | Roche-lobe mass-transfer model. |
| `Mergers\BinaryMergerModel.cs` | Binary merger outcome model. |
| `Mergers\MergerRemnantFactory.cs` | Creates remnants from mergers. |
| `RocheLobe\RocheLobeCalculator.cs` | Roche-lobe geometry calculations. |
| `SupernovaChannels\BinarySupernovaModel.cs` | Binary-driven supernova model. |
| `SupernovaChannels\StrippedEnvelopeSNModel.cs` | Stripped-envelope supernova model. |
| `SupernovaChannels\TypeIaModel.cs` | Type Ia supernova model. |
| `SupernovaChannels\XRayBinaryModel.cs` | X-ray binary emission model. |
| `Tides\BinaryTidalModel.cs` | Tidal interaction in binaries. |
| `TripleDynamics\TripleDynamicsModel.cs` | Triple-system dynamical evolution. |

</details>

<details>
<summary><strong>Continuum</strong> (<code>Cosmos\Continuum</code>)</summary>

| File | Purpose |
|---|---|
| `ContinuumAutoHostedService.cs` | Hosted service driving continuum updates. |
| `ContinuumAutoWiring.cs` | Auto-wiring of continuum components. |
| `ContinuumServiceCollectionExtensions.cs` | DI registration for continuum services. |
| `ContinuumState.cs` | Continuum field state container. |
| `CosmosContinuumIntegration.cs` | Bridges continuum physics into the simulation. |
| `CosmosUniverseBridge.cs` | Maps universe state to/from continuum grid. |
| `Fields.cs` | Continuum field definitions. |
| `GridSpec.cs` | Continuum grid specification. |
| `PhysicsModule.cs` | Pluggable continuum physics module. |
| `UniversePhysicsPipeline.cs` | Pipeline running universe-level physics. |

</details>

<details>
<summary><strong>Disc Physics</strong> (<code>Cosmos\DiscPhysics</code>, <code>Cosmos\DiscPlanetInteraction</code>)</summary>

| File | Purpose |
|---|---|
| `DiscPhysics\DiscField.cs` | Protoplanetary-disc field data. |
| `DiscPhysics\DiscOptions.cs` | Disc-model configuration. |
| `DiscPhysics\DiscTurbulenceModel.cs` | Disc turbulence model. |
| `DiscPhysics\DiscViscosityModel.cs` | Disc viscosity model. |
| `DiscPhysics\DustEvolutionModel.cs` | Dust growth/evolution in discs. |
| `DiscPhysics\ProtoplanetaryDisc.cs` | Protoplanetary-disc entity/model. |
| `DiscPlanetInteraction\DiscPlanetInteractionModel.cs` | Disc–planet interaction model. |
| `DiscPlanetInteraction\EccentricityDampingModel.cs` | Eccentricity damping from disc. |
| `DiscPlanetInteraction\InclinationDampingModel.cs` | Inclination damping from disc. |
| `DiscPlanetInteraction\PlanetTrapModel.cs` | Planet-trap (migration halt) model. |

</details>

<details>
<summary><strong>Planetary Systems &amp; Formation</strong> (<code>Cosmos\PlanetarySystems</code>, <code>PlanetFormation</code>, <code>PlanetMigration</code>)</summary>

| File | Purpose |
|---|---|
| `PlanetarySystems\MultiPlanetDynamicsPipeline.cs` | Runs multi-planet dynamics steps. |
| `PlanetarySystems\PlanetaryDiagnostics.cs` | Diagnostics for planetary systems. |
| `PlanetarySystems\PlanetarySystemContext.cs` | Shared context for system pipelines. |
| `PlanetarySystems\PlanetarySystemsPipeline.cs` | Orchestrates planetary-system evolution. |
| `PlanetarySystems\PlanetarySystemsServiceCollectionExtensions.cs` | DI registration for planetary systems. |
| `PlanetarySystems\PlanetarySystemsSettings.cs` | Configuration for planetary systems. |
| `PlanetarySystems\PlanetFormationPipeline.cs` | Planet-formation step pipeline. |
| `PlanetarySystems\PlanetMigrationPipeline.cs` | Planet-migration step pipeline. |
| `PlanetarySystems\ResonancePipeline.cs` | Resonance-processing pipeline. |
| `PlanetFormation\EnvelopeAccretionModel.cs` | Gas-envelope accretion model. |
| `PlanetFormation\PebbleAccretionModel.cs` | Pebble-accretion model. |
| `PlanetFormation\PlanetesimalModel.cs` | Planetesimal formation model. |
| `PlanetFormation\PlanetFormationModel.cs` | Overall planet-formation model. |
| `PlanetFormation\PlanetFormationOptions.cs` | Formation configuration. |
| `PlanetMigration\GapOpeningModel.cs` | Disc gap-opening model. |
| `PlanetMigration\MigrationOptions.cs` | Migration configuration. |
| `PlanetMigration\MigrationRegime.cs` | Migration regime enum/logic. |
| `PlanetMigration\PlanetMigrationModel.cs` | Planet-migration model. |
| `PlanetMigration\TypeIMigration.cs` | Type I migration model. |
| `PlanetMigration\TypeIIMigration.cs` | Type II migration model. |
| `PlanetMigration\TypeIIIMigration.cs` | Type III migration model. |

</details>

<details>
<summary><strong>Multi-Planet, Resonances, Secular, Tides</strong></summary>

| File | Purpose |
|---|---|
| `MultiPlanetDynamics\ChaoticDynamicsModel.cs` | Chaotic N-body dynamics model. |
| `MultiPlanetDynamics\HillStabilityChecker.cs` | Hill-stability check for systems. |
| `MultiPlanetDynamics\IMultiPlanetIntegrator.cs` | Integrator interface. |
| `MultiPlanetDynamics\MultiPlanetIntegrator.cs` | Multi-planet numerical integrator. |
| `MultiPlanetDynamics\VerletMultiPlanetIntegrator.cs` | Verlet integration implementation. |
| `Resonances\ResonanceDetector.cs` | Detects orbital resonances. |
| `Resonances\ResonanceDynamicsModel.cs` | Resonance dynamical evolution. |
| `Resonances\ResonanceState.cs` | Resonance state container. |
| `SecularDynamics\KozaiLidovModel.cs` | Kozai–Lidov secular oscillation model. |
| `SecularDynamics\SecularDynamicsModel.cs` | Long-term secular dynamics model. |
| `Tides\OrbitalCircularizationModel.cs` | Tidal orbit-circularization model. |
| `Tides\RotationEvolutionModel.cs` | Tidal rotation evolution. |
| `Tides\StarTidalResponseModel.cs` | Stellar tidal-response model. |
| `Tides\TidalDissipationModel.cs` | Tidal energy dissipation model. |
| `Tides\TidalTorqueCalculator.cs` | Tidal torque calculations. |

</details>

<details>
<summary><strong>Stellar Winds</strong> (<code>Cosmos\StellarWinds</code>)</summary>

| File | Purpose |
|---|---|
| `BinaryCoupling\WindAccretionModel.cs` | Wind accretion in binaries. |
| `BinaryCoupling\WindBinaryInteractionModel.cs` | Wind–binary interaction model. |
| `BinaryCoupling\WindOrbitalEvolutionModel.cs` | Orbital evolution from winds. |
| `Feedback\CSMModel.cs` | Circumstellar-medium model. |
| `Feedback\WindFeedbackModel.cs` | Wind energy/momentum feedback. |
| `Feedback\WindInjectionEvent.cs` | Wind mass-injection event data. |
| `Models\CoolStarWindModel.cs` | Cool-star wind model. |
| `Models\DustDrivenWindModel.cs` | Dust-driven wind model. |
| `Models\LineDrivenWindModel.cs` | Line-driven wind model. |
| `Models\MagneticWindModel.cs` | Magnetically driven wind model. |
| `Models\MassLossRateCalculator.cs` | Mass-loss-rate calculator. |
| `Models\RotationalMassLossModel.cs` | Rotation-enhanced mass loss. |
| `Models\StellarWindModel.cs` | Base stellar-wind model. |
| `Models\WindRegime.cs` | Wind-regime enum/logic. |
| `StellarWindDiagnostics.cs` | Wind diagnostics output. |
| `StellarWindPipeline.cs` | Wind evolution pipeline. |
| `StellarWindSettings.cs` | Wind configuration. |
| `StellarWindsServiceCollectionExtensions.cs` | DI registration for wind services. |
| `Tracks\MassLossTrack.cs` | Precomputed mass-loss track data. |
| `Tracks\StellarMassLossIntegrator.cs` | Integrates stellar mass loss. |
| `Tracks\WindRegimeSelector.cs` | Selects wind regime by conditions. |
| `WR\WREvolutionModel.cs` | Wolf–Rayet evolution model. |
| `WR\WRMassLossModel.cs` | Wolf–Rayet mass-loss model. |
| `WR\WRSubtype.cs` | Wolf–Rayet subtype classification. |

</details>

<details>
<summary><strong>Supernova</strong> (<code>Cosmos\Supernova</code>)</summary>

| File | Purpose |
|---|---|
| `MassBudget.cs` | Supernova mass-budget accounting. |
| `SupernovaSinks.cs` | Mass/energy sink routing for supernovae. |

</details>

---

## 🏗️ UniverseEngine

<details>
<summary><strong>Planet Destruction</strong> (<code>UniverseEngine\PlanetDestruction</code>)</summary>

| File | Purpose |
|---|---|
| `Collisions\PlanetCollisionModel.cs` | Planet–planet collision model. |
| `Collisions\PlanetFragmentationModel.cs` | Collision fragmentation model. |
| `Collisions\PlanetMergerModel.cs` | Planet-merger outcome model. |
| `CompactObjectConsumption\CompactObjectPlanetAccretionModels.cs` | Compact-object accretion of planets. |
| `CompactObjectConsumption\CompactObjectPlanetConsumptionModel.cs` | Compact-object planet consumption model. |
| `Diagnostics\DestructionChannelSummary.cs` | Summary of destruction channels. |
| `Diagnostics\PlanetDestructionAuditReport.cs` | Planet-destruction audit report. |
| `MassBudget\PlanetMassBudgetTracker.cs` | Tracks planet mass budget. |
| `MassBudget\PlanetMassConservationValidator.cs` | Validates planet mass conservation. |
| `PlanetDestructionContracts.cs` | Interfaces/contracts for destruction. |
| `PlanetDestructionOptions.cs` | Destruction configuration. |
| `PlanetDestructionPipeline.cs` | Planet-destruction pipeline. |
| `PlanetDestructionServiceCollectionExtensions.cs` | DI registration for destruction. |
| `StellarEngulfment\CommonEnvelopePlanetModel.cs` | Planet common-envelope engulfment. |
| `StellarEngulfment\StellarEngulfmentModel.cs` | Stellar engulfment of planets. |
| `TidalInfall\CompactObjectTDEModel.cs` | Tidal-disruption-event model. |
| `TidalInfall\RocheLimitCalculator.cs` | Roche-limit calculator. |
| `TidalInfall\TidalInfallModel.cs` | Tidal-infall model. |

</details>

<details>
<summary><strong>Planet Formation Regulation</strong> (<code>UniverseEngine\PlanetFormationRegulation</code>)</summary>

| File | Purpose |
|---|---|
| `BaryonFraction\BaryonFractionModel.cs` | Baryon-fraction regulation model. |
| `BaryonFraction\GlobalMassBudgetTracker.cs` | Tracks global mass budget. |
| `DestructionChannels\PlanetDestructionModel.cs` | Formation-side destruction model. |
| `DestructionChannels\PlanetEjectionModel.cs` | Planet-ejection model. |
| `DestructionChannels\PlanetInfallModel.cs` | Planet-infall model. |
| `DestructionChannels\PlanetMergerModel.cs` | Formation-side merger model. |
| `Diagnostics\MassConservationValidator.cs` | Validates mass conservation. |
| `Diagnostics\MassFlowDiagnostics.cs` | Mass-flow diagnostics. |
| `Diagnostics\PlanetFormationAuditReport.cs` | Formation audit report. |
| `Diagnostics\RegulationConstants.cs` | Regulation constants. |
| `DiscMassBudget\DiscLifetimeModel.cs` | Disc-lifetime model. |
| `DiscMassBudget\DiscMassBudgetModel.cs` | Disc mass-budget model. |
| `DiscMassBudget\DiscMassLimiter.cs` | Limits disc mass usage. |
| `FormationLimits\PlanetFormationLimiter.cs` | Caps planet formation. |
| `FormationLimits\PlanetMassBudgetTracker.cs` | Tracks formation mass budget. |
| `PebbleFlux\PebbleDestructionModel.cs` | Pebble-destruction model. |
| `PebbleFlux\PebbleFluxRegulator.cs` | Regulates pebble flux. |
| `PebbleFlux\PebbleIsolationModel.cs` | Pebble-isolation-mass model. |
| `PlanetesimalEfficiency\PlanetesimalEfficiencyModel.cs` | Planetesimal-formation efficiency. |
| `PlanetesimalEfficiency\SolidLossModel.cs` | Solid-mass loss model. |
| `PlanetesimalEfficiency\StreamingInstabilityModel.cs` | Streaming-instability model. |
| `PlanetFormationRegulationContracts.cs` | Interfaces/contracts for regulation. |
| `PlanetFormationRegulationOptions.cs` | Regulation configuration. |
| `PlanetFormationRegulationPipeline.cs` | Formation-regulation pipeline. |

</details>

<details>
<summary><strong>Small Bodies</strong> (<code>UniverseEngine\SmallBodies</code>)</summary>

| File | Purpose |
|---|---|
| `Asteroids\AsteroidModels.cs` | Asteroid data/behavior models. |
| `Comets\CometModels.cs` | Comet data/behavior models. |
| `Diagnostics\SmallBodyChannelSummary.cs` | Small-body channel summary. |
| `Diagnostics\SmallBodyDestructionAuditReport.cs` | Small-body destruction audit. |
| `Dust\DustModels.cs` | Dust models. |
| `DwarfPlanets\DwarfPlanetModels.cs` | Dwarf-planet models. |
| `MassBudget\SmallBodyMassBudgetTracker.cs` | Tracks small-body mass budget. |
| `MassBudget\SmallBodyMassConservationValidator.cs` | Validates small-body conservation. |
| `MassBudget\SmallBodyMassFlowReport.cs` | Small-body mass-flow report. |
| `Meteoroids\MeteoroidModels.cs` | Meteoroid models. |
| `Moons\MoonModels.cs` | Moon models. |
| `SmallBodyContracts.cs` | Interfaces/contracts for small bodies. |
| `SmallBodyDestructionPipeline.cs` | Small-body destruction pipeline. |
| `SmallBodyDestructionServiceCollectionExtensions.cs` | DI registration for small bodies. |
| `SmallBodyOptions.cs` | Small-body configuration. |
| `SmallBodyReservoir.cs` | Small-body mass reservoir. |
| `SmallBodySeedingModel.cs` | Seeds initial small bodies. |

</details>

<details>
<summary><strong>Stellar Remnants</strong> (<code>UniverseEngine\StellarRemnants</code>)</summary>

| File | Purpose |
|---|---|
| `BinaryEffects\BinaryRemnantModifier.cs` | Adjusts remnants for binary effects. |
| `CollapseEngines\IRemnantRandom.cs` | Randomness interface for collapse. |
| `CollapseEngines\StandardCollapseEngine.cs` | Standard stellar-collapse engine. |
| `MetallicityEffects\MetallicityMassLossModel.cs` | Metallicity-dependent mass loss. |
| `RemnantClassification\RemnantClassifier.cs` | Classifies remnant type. |
| `RemnantClassification\RemnantEnums.cs` | Remnant-type enums. |
| `RemnantClassification\RemnantModels.cs` | Remnant data models. |
| `RemnantMass\IRemnantMassModel.cs` | Remnant-mass model interface. |
| `RemnantMass\RemnantMassModels.cs` | Remnant-mass implementations. |
| `StellarRemnantPipeline.cs` | Stellar-remnant formation pipeline. |
| `StellarRemnantPipelineFactory.cs` | Factory for the remnant pipeline. |
| `StellarRemnantsServiceCollectionExtensions.cs` | DI registration for remnants. |

</details>

---

## 🧮 Realism-Enforcement Layer (staged physics-completeness)

> A set of **gated, additive** physics domains layered on top of the live universe. Each is a self-contained
> `Options → Model → State → Pipeline → Validator → Diagnostics` unit registered through
> `AddRealismExtensions()`. A master switch (`EnableRealismExtensions`) plus one per-domain toggle in
> `RealismConfig` gate every module, so the entire layer is a no-op when disabled. Domains write only to
> their own state and route only *conservative* transitions through the shared ledgers.
>
> **Tick order:** Cosmology → Thermodynamics → Electromagnetism → Dark Sector → Radiative Transfer →
> Chemistry → N-Body → Initial Conditions.

### Conservation Ledgers (`Cosmos\Ledgers`)

| File | Purpose |
|---|---|
| `EnergyLedger.cs` | Canonical energy-conservation ledger (clamped, never negative). |
| `ExoticEnergyLedger.cs` | Exotic/vacuum energy ledger (e.g. wormhole pinch-off release). |
| `MomentumLedger.cs` | Total-momentum conservation ledger for closed-system invariants. |
| `RealismConservationSystem.cs` | Aggregates and runs the per-tick conservation validators. |
| `RealismServiceCollectionExtensions.cs` | Central DI chain wiring all realism domains (`AddRealismExtensions`). |

### Stage 2 — FRW Cosmology (`Cosmos\Cosmology`)

| File | Purpose |
|---|---|
| `CosmologyOptions.cs` | FRW/ΛCDM background configuration (Ω values, H₀, scale factor). |
| `FriedmannSolver.cs` | Integrates the scale factor a(t) from the Friedmann equation. |
| `CosmologyState.cs` | Live cosmology state (a, H, redshift, curvature). |
| `CosmologyPipeline.cs` | Per-tick driver advancing the cosmological background. |
| `FrwConsistencyValidator.cs` | Validates flatness/budget closure and background consistency. |
| `CosmologyDiagnostics.cs` | Snapshot/report of the cosmological state. |
| `CosmologyServiceCollectionExtensions.cs` | DI registration (`AddCosmology`). |

### Stage 3 — Thermodynamics (`Cosmos\Thermodynamics`)

| File | Purpose |
|---|---|
| `ThermodynamicsOptions.cs` | Thermodynamics configuration (reference temperature, coupling). |
| `AdiabaticGasModel.cs` | Adiabatic cooling law (T ∝ a⁻² monatomic; T ∝ a⁻¹ radiation). |
| `ThermalState.cs` | Live thermal state (temperature, entropy contribution). |
| `ThermodynamicsPipeline.cs` | Per-tick driver; routes non-negative entropy into the shared budget. |
| `ThermalConsistencyValidator.cs` | Enforces the second law (entropy monotone, bounded drift). |
| `ThermodynamicsDiagnostics.cs` | Snapshot/report of the thermal state. |
| `ThermodynamicsServiceCollectionExtensions.cs` | DI registration (`AddThermodynamics`). |

### Stage 4 — Electromagnetism / Plasma (`Cosmos\Electromagnetism`)

| File | Purpose |
|---|---|
| `PlasmaOptions.cs` | Plasma/ionization configuration. |
| `SahaIonizationModel.cs` | Saha-style equilibrium ionization fraction vs. temperature. |
| `PlasmaState.cs` | Live plasma state (ionization fraction, electron count). |
| `ElectromagnetismPipeline.cs` | Per-tick driver; recombination energy routed via `EnergyLedger`. |
| `ChargeNeutralityValidator.cs` | Enforces global charge neutrality and electron-count conservation. |
| `ElectromagnetismDiagnostics.cs` | Snapshot/report (flags recombined/neutral state). |
| `ElectromagnetismServiceCollectionExtensions.cs` | DI registration (`AddElectromagnetism`). |

### Stage 5 — Dark Sector (`Cosmos\DarkSector`)

| File | Purpose |
|---|---|
| `DarkSectorOptions.cs` | Dark-matter/dark-energy configuration (equation of state w). |
| `DarkMatterRelicModel.cs` | Dark-matter relic density / dilution model. |
| `DarkSectorState.cs` | Live dark-sector state (densities, dominance). |
| `DarkSectorPipeline.cs` | Per-tick driver evolving dark densities against the background. |
| `DarkSectorConsistencyValidator.cs` | Validates densities vs. present-day Ω at the reference epoch. |
| `DarkSectorDiagnostics.cs` | Snapshot/report (frozen relic, sane densities). |
| `DarkSectorServiceCollectionExtensions.cs` | DI registration (`AddDarkSector`). |

### Stage 6 — Radiative Transfer (`Cosmos\RadiativeTransfer`)

| File | Purpose |
|---|---|
| `RadiativeTransferOptions.cs` | Radiative-transfer configuration (opacity law). |
| `RadiativeTransferModel.cs` | Optical-depth and attenuation model (τ increases with nₑ). |
| `RadiativeTransferState.cs` | Live radiation state (thermal vs. escaped sectors). |
| `RadiativeTransferPipeline.cs` | Per-tick driver; conservative routing preserves grand total. |
| `RadiativeTransferConsistencyValidator.cs` | Validates the sum over sectors is invariant. |
| `RadiativeTransferDiagnostics.cs` | Snapshot/report of the radiation state. |
| `RadiativeTransferServiceCollectionExtensions.cs` | DI registration (`AddRadiativeTransfer`). |

### Stage 7 — Chemistry Network (`Cosmos\Chemistry`)

| File | Purpose |
|---|---|
| `ChemistryOptions.cs` | Chemistry-network configuration (primordial mass fractions). |
| `PrimordialChemistryModel.cs` | Splits total nuclei into H/He; tracks neutral/ionized species. |
| `ChemistryState.cs` | Live chemistry state (species abundances). |
| `ChemistryNetworkPipeline.cs` | Per-tick driver conserving the total nuclei count. |
| `ChemistryConsistencyValidator.cs` | Flags spurious creation/destruction of nuclei. |
| `ChemistryDiagnostics.cs` | Snapshot/report of the chemistry state. |
| `Chemistry.cs` | Shared chemistry helper/types for the network. |
| `ChemistryServiceCollectionExtensions.cs` | DI registration (`AddChemistryNetwork`). |

### Stage 8 — N-Body Dynamics (`Cosmos\NBody`)

| File | Purpose |
|---|---|
| `NBodyOptions.cs` | N-body configuration (softening length, integrator). |
| `GravitationalNBodyModel.cs` | Softened pairwise gravity acceleration model. |
| `NBodyState.cs` | Live N-body state (positions, velocities, masses). |
| `NBodyPipeline.cs` | Per-tick driver; symplectic leapfrog (kick–drift–kick). |
| `NBodyConsistencyValidator.cs` | Validates momentum symmetry and bounded energy drift. |
| `NBodyDiagnostics.cs` | Snapshot/report of the N-body population. |
| `NBodyServiceCollectionExtensions.cs` | DI registration (`AddNBody`). |

### Stage 9 — Initial Conditions (`Cosmos\InitialConditions`)

| File | Purpose |
|---|---|
| `InitialConditionsOptions.cs` | IC configuration (grid, modes, spectral index nₛ, amplitude, seed). |
| `GaussianFieldModel.cs` | Deterministic Gaussian density-field generator from P(k) = A·kⁿˢ. |
| `InitialConditionsState.cs` | Live primordial field state (field, spectrum, mean, variance). |
| `InitialConditionsPipeline.cs` | Seed-time generator; `Step()` is a deliberate no-op. |
| `InitialConditionsConsistencyValidator.cs` | Validates finiteness, zero mean, and variance vs. expectation. |
| `InitialConditionsDiagnostics.cs` | Snapshot/report of the primordial field (stats + min/max). |
| `InitialConditionsServiceCollectionExtensions.cs` | DI registration (`AddInitialConditions`). |

---

## 🖥️ Hosting, Realtime, Controllers & App

| File | Purpose |
|---|---|
| `Program.cs` | App entry point and service/simulation wiring. |
| `Controllers\PhysicsReferenceController.cs` | API for physics-reference data. |
| `Controllers\UniverseController.cs` | API for universe control/state. |
| `Realtime\CosmosHub.cs` | SignalR hub for real-time updates. |
| `Realtime\SimulationHostedService.cs` | Background service running the sim loop. |
| `Realtime\Snapshot\SafeDoubleJsonConverter.cs` | JSON converter guarding non-finite doubles. |
| `Realtime\Snapshot\SafeDoubleMessagePackFormatter.cs` | MessagePack formatter for safe doubles. |
| `Realtime\Snapshot\SnapshotMapper.cs` | Maps universe state to snapshots. |
| `Realtime\Snapshot\UniverseSnapshot.cs` | Serializable universe snapshot model. |
| `Models\UniverseModels.cs` | DTO/view models for the universe. |

---

<sub>Generated as a navigation reference for the CurPay Quantum Cosmos engine. See
<a href="wwwroot/physics-reference.html">physics-reference.html</a> for the physics behind each subsystem.</sub>
