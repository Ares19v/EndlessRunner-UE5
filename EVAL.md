# EVAL — EndlessRunner-UE5

> **Evaluation Date:** 2026-05-29  
> **Evaluator:** Automated Portfolio Review  
> **Maturity Level:** Production-Ready

---

## 1. Project Purpose & Problem Statement

EndlessRunner-UE5 is a procedural endless runner game built in Unreal Engine 5.7, designed as a technical showcase of the engine's newest systems rather than as a commercial product. The core problem it addresses is architectural: traditional endless runners are implemented with monolithic Blueprints or nested FSMs that become unmaintainable as complexity grows. This project demonstrates a production-grade alternative using UE 5.7's Gameplay StateTree for player state management, an Actor Pooling architecture for procedural level generation, and the Substrate material pipeline for rendering — three systems that are relatively new and underrepresented in public portfolio work.

The target audience is Unreal Engine developers, technical artists, and studio recruiters assessing UE 5.x architecture competence.

---

## 2. Technical Architecture

The system is organized around four interconnected subsystems:

**Gameplay StateTree (`ST_PlayerController`):**
The player's behavioral states (Running, Jumping, Sliding, Dead, Game Over) are managed via UE 5.7's StateTree framework instead of the traditional Anim Blueprint state machine or nested Blueprint FSMs. Each state is a discrete node with explicit transition conditions and no hard references to dependent systems — state transitions trigger Niagara effects and MetaSound cues via decoupled events rather than direct function calls.

**Actor Pool Manager:**
Procedural floor tiles and obstacles are pre-allocated into a fixed pool at game start and recycled rather than dynamically spawned/destroyed. This eliminates per-frame memory allocation overhead (a primary source of hitching in high-speed runners) and keeps the memory footprint predictable. Seed-based deterministic spawning allows consistent generation patterns across sessions.

**Input System — Enhanced Input 2.0:**
Player input is handled via UE's Enhanced Input system (IMC + IA assets) with low-latency action binding. Advanced collision channel management prevents high-speed character movement from passing through modular floor seams.

**Substrate Material Pipeline:**
Materials use UE 5.7's Substrate (formerly Strata) shading framework — a layered, physics-based material model that replaces the traditional single shading model. Provides multi-layered material fidelity without the overhead of multiple material passes.

**Communication Architecture:**
`BPInterface` (Blueprint Interface) assets serve as the communication contract between systems — GameMode, Pool Manager, HUD, and the Player Character communicate via interface calls rather than direct Blueprint references. This prevents circular dependencies and enables hot-swapping of implementations.

**VFX/Audio:** Niagara particle systems triggered on state transitions; MetaSound assets for procedural audio synchronized to gameplay events.

**VCS:** Git LFS for `.uasset` and `.umap` binary assets — correct and necessary for UE projects.

---

## 3. Strengths

- **Gameplay StateTree adoption** — UE 5.7's StateTree is a significant departure from traditional FSM approaches. Using it for player state management — with decoupled transition triggers for Niagara and MetaSounds — demonstrates awareness of Epic's current recommended architecture.
- **Actor Pooling** — manual object pooling in Unreal is a discipline that separates senior from junior developers. Eliminating dynamic spawn/destroy on a hot path in a high-speed game is the correct optimization.
- **BPInterface communication contracts** — using Blueprint Interfaces instead of direct Blueprint-to-Blueprint references is the UE equivalent of programming to an interface rather than an implementation. No hard references in the primary gameplay loop is explicitly noted as a project standard.
- **Zero Blueprint compile warnings** — a clean compile in UE is not trivial; this is a stated and presumably verified quality standard.
- **Substrate material pipeline** — adopting the new shading framework rather than the legacy material model positions the project on UE's forward path.
- **Enhanced Input 2.0** — latest UE input system with IMC/IA asset pattern is the correct modern approach.
- **Git LFS for binary assets** — essential for UE repos; absent LFS causes repository bloat and corrupts `.uasset` checkout.
- **Epic naming conventions** — `BP_`, `BPI_`, `IA_`, `ST_` prefixes consistently applied, matching Epic's technical standards.

---

## 4. Limitations & Known Gaps

- **No gameplay screenshots or video in the README.** This is the single biggest presentation gap for a game project — there is no visual evidence of the game running. A GIF or YouTube link would dramatically improve the portfolio impact.
- **No gameplay metrics or performance benchmarks.** No FPS numbers, no memory profiling data, no pool size justification. A senior UE developer would want to see profiler screenshots or Unreal Insights data.
- **README does not describe gameplay.** The README is focused entirely on architecture; it never explains how the game actually plays, what the progression curve is, or what makes it interesting to play. The experience layer is undocumented.
- **No C++ components visible in the repository breakdown.** The README mentions "C++ / Blueprints" in the project description but the directory table only lists Blueprint and configuration directories. The extent of C++ involvement is unclear.
- **Substrate is still experimental in UE 5.7.** Using experimental features demonstrates awareness of cutting-edge systems but introduces risk — Substrate's API has changed between engine versions and some platform targets do not support it.
- **Single-platform (Windows).** No mention of mobile, console, or web targets. Not a limitation for a technical showcase but worth noting.
- **No automated testing.** UE provides `FAutomationTest` and the Functional Testing framework; neither appears to be used. Runtime assertions or automation tests for the pool manager logic would strengthen the quality claim.

---

## 5. Code Quality Assessment

**Structure:** Content directory organization follows Epic's recommended conventions with `Content/BluePrints/`, `Content/BPInterface/`, `Content/ThirdPerson/`, `Content/Input/`, `Content/UserWidget/`. Clean separation of concerns by UE content type.

**Documentation:** README is technically focused with a Mermaid architecture diagram showing the StateTree → GameMode → Pool → Floor/Spawner → VFX/Audio dependency graph. Developer workflow standards (naming, optimization, VCS) are explicitly documented.

**Blueprint Quality:** Zero compile warnings is a stated standard. No hard references in the gameplay loop is documented. These are verifiable quality claims for anyone who opens the project in the editor.

**VCS:** Git LFS properly configured for `.uasset` and `.umap`. This is a non-trivial setup for UE repos.

---

## 6. Maturity Breakdown

| Dimension | Score | Notes |
|-----------|-------|-------|
| Functionality | 7/10 | Systems described as production-grade; no visual verification in README |
| Code Quality | 8/10 | Correct UE conventions; BPInterface decoupling; zero-warning policy |
| Documentation | 6/10 | Architecture well-documented; gameplay experience not described; no screenshots |
| Scalability | 8/10 | Actor pooling; deterministic spawning; StateTree handles complexity growth |
| Security | N/A | Game project; not applicable |
| **Overall** | **7.3/10** | Technically sound UE architecture; needs visual evidence and gameplay description |

---

## 7. Suggested Next Steps

1. **Add gameplay footage.** Record a 30-second gameplay GIF or YouTube clip and embed it in the README. This is the single highest-impact change — a game project without screenshots is unconvincing regardless of the architectural quality.
2. **Add Unreal Insights profiling data.** Capture a profiler session showing the pool manager eliminating spawn hitches, the memory footprint under sustained gameplay, and the frame budget breakdown. This transforms "Actor Pooling reduces allocations" from a claim into a demonstrated result.
3. **Document the C++ vs Blueprint split.** Clarify which systems are implemented in C++ and which are Blueprint-only. If StateTree tasks or pool manager logic are in C++, show the relevant code in the README or link to specific source files — C++ proficiency in UE is a significant differentiator.

---

## 9. Verdict

EndlessRunner-UE5 demonstrates genuine depth in Unreal Engine 5.7's latest architectural systems — Gameplay StateTree for decoupled player state management, Actor Pooling for allocation-free procedural generation, BPInterface communication contracts, and Substrate materials. The design choices are correct and well-reasoned; the zero-compile-warning standard and no-hard-references policy show professional discipline. The project's primary weakness is presentation: there are no screenshots, no gameplay video, and no performance data, making it difficult for anyone who cannot open the project in the editor to assess the quality of the result. The architecture is there; it simply needs to be shown.
