# issues.md — Drywall / Light Metal Stud Planner MVP

**Source:** PRD v1 — Drywall / Light Metal Stud Project Design Web Application  
**Preferred stack:** Nuxt / Vue, Three.js, Supabase  
**Primary user:** drywall / light metal framing contractors and experienced builders  
**Secondary user:** DIY users who need guided support  
**Market:** Europe / UK, metric workflows  
**MVP rule:** structured parameters + deterministic generation engine first; AI assists but does not directly generate geometry.

---

## How to use this file

This file converts the PRD into a developer-ready issue backlog. Each issue can be copied into GitHub Issues, Linear, Jira, or another project tracker.

Recommended labels:

- `phase-0-validation`
- `phase-1-prototype`
- `phase-2-core`
- `phase-3-templates`
- `phase-4-ai`
- `phase-5-beta`
- `frontend`
- `backend`
- `3d`
- `ai`
- `pdf`
- `admin`
- `analytics`
- `qa`
- `security`
- `mvp`

Recommended priority levels:

- `P0` — required to prove the core product works
- `P1` — required for full MVP completion
- `P2` — useful but can be simplified if timeline is tight

---

# Milestones

## Milestone 0 — Product and construction validation

Goal: define construction assumptions, supported scope, schemas, and validation rules before heavy development starts.

Includes issues:

- ISSUE-001 to ISSUE-007

## Milestone 1 — Wall partition technical prototype

Goal: prove the full core loop for one simple template: structured inputs → 3D skeleton → materials → cut list → basic PDF.

Includes issues:

- ISSUE-008 to ISSUE-018

## Milestone 2 — Core MVP foundation

Goal: add accounts, saved projects, checklists, dashboard, presets, and output invalidation logic.

Includes issues:

- ISSUE-019 to ISSUE-027

## Milestone 3 — Full MVP templates and workspace

Goal: add box/counter and TV wall/shelving templates, full workspace UX, validation system, and plasterboard overlay.

Includes issues:

- ISSUE-028 to ISSUE-037

## Milestone 4 — AI assistant layer

Goal: add AI-assisted description parsing, clarification, schema validation, summaries, and safe scope handling.

Includes issues:

- ISSUE-038 to ISSUE-044

## Milestone 5 — Sharing, branding, admin, analytics, beta hardening

Goal: prepare the MVP for private beta and client-facing use.

Includes issues:

- ISSUE-045 to ISSUE-060

---

# Phase 0 — Product and construction validation

---

## ISSUE-001 — Confirm MVP-supported construction scope

**Priority:** P0  
**Labels:** `phase-0-validation`, `mvp`, `qa`  
**Depends on:** none

### Description

Document exactly what the MVP supports and does not support so all later generation, validation, UI, and disclaimers are aligned.

The MVP supports simple, rectilinear, non-load-bearing drywall / light metal stud structures only.

### Included scope

- Wall partition
- Box / counter structure
- TV wall / shelving structure
- Simple rectangular geometry
- Europe / UK metric defaults
- Generic C-stud / U-track framing
- Estimated material quantities
- Non-certified planning outputs

### Excluded scope

- Load-bearing structures
- Curved or angled walls
- Fireplaces, BBQs, or heat/fire-related structures
- Plumbing/electrical integration
- Ceiling-hung/floating structures
- Structures supporting people
- Full kitchen systems with doors, drawers, hinges, appliances
- CAD/DWG/DXF export
- Supplier-specific product purchasing
- Photo upload / room visualization
- Certified engineering or building regulation approval

### Acceptance criteria

- [ ] MVP scope is documented in `/docs/mvp-scope.md` or equivalent.
- [ ] Supported and unsupported project types are clearly listed.
- [ ] Unsupported project types can be mapped to hard-block validation rules.
- [ ] Scope document is approved by product owner before Phase 1 development.

---

## ISSUE-002 — Define default Europe/UK material preset

**Priority:** P0  
**Labels:** `phase-0-validation`, `backend`, `mvp`  
**Depends on:** ISSUE-001

### Description

Create the default generic Europe/UK metric material preset used by the MVP.

### Default preset

- Internal unit: millimetres
- Stud/profile type: generic C-stud
- Track type: generic U-track
- Default profile width: 50 mm
- Default profile length: 3000 mm
- Default stud spacing: 600 mm centres
- Optional stud spacing: 400 mm centres
- Default plasterboard size: 1200 × 2400 mm
- Default plasterboard thickness: 12.5 mm
- Default layer count: 1
- Default waste allowance: 10%
- Screw estimate: calculated from board area / project assumptions
- Anchors/fixings: estimated from track length
- Joint tape: estimated from board joints/perimeter
- Joint compound: estimated from board area
- Corner bead: added where external corners exist

### Acceptance criteria

- [ ] Default material preset is documented.
- [ ] Preset includes profile, board, screw, fixing, finishing, and waste assumptions.
- [ ] Preset is represented in a machine-readable structure.
- [ ] Preset can later be edited from admin panel.
- [ ] Preset is clearly marked as generic, estimated, and expert-review-required.

---

## ISSUE-003 — Define strict template-specific project schemas

**Priority:** P0  
**Labels:** `phase-0-validation`, `backend`, `frontend`, `mvp`  
**Depends on:** ISSUE-001, ISSUE-002

### Description

Define strict schemas for each supported template. Do not use one loose universal schema for all project types.

Schemas should be implemented using TypeScript types and a runtime validation library such as Zod.

### Required schemas

- `WallPartitionProject`
- `BoxCounterProject`
- `TvWallShelvingProject`
- Shared base project fields
- Material preset schema
- Installation context schema
- Checklist item schema
- Validation warning schema

### Shared base fields

- `id`
- `projectName`
- `projectType`
- `unitSystem`
- `materialPresetId`
- `installationContext`
- `createdAt`
- `updatedAt`
- `createdBy`
- `lastGeneratedOutputAt`
- `outputsOutdated`

### Acceptance criteria

- [ ] All template schemas are defined in code.
- [ ] All schemas have runtime validation.
- [ ] Invalid project data cannot be passed into the generation engine.
- [ ] Schemas are documented for future AI output validation.
- [ ] Unit tests cover valid and invalid schema examples.

---

## ISSUE-004 — Define material calculation rules for MVP

**Priority:** P0  
**Labels:** `phase-0-validation`, `backend`, `mvp`  
**Depends on:** ISSUE-002, ISSUE-003

### Description

Define deterministic material calculation logic for the MVP. Calculations must produce estimated quantities, not guaranteed purchasing quantities.

### Calculation areas

- C-stud quantity
- U-track quantity
- Profile length rounding
- Basic cut list grouping
- Plasterboard sheet estimate
- Screws estimate
- Anchors/fixings estimate
- Joint tape estimate
- Joint compound estimate
- Corner bead estimate
- Optional reinforcement items
- Waste allowance

### Acceptance criteria

- [ ] Material calculation assumptions are documented.
- [ ] Calculations are deterministic from project parameters and material preset.
- [ ] Quantities are rounded upward where appropriate.
- [ ] Waste allowance is applied transparently.
- [ ] User-facing copy says quantities are estimates and must be verified.
- [ ] Rules are ready for expert review before beta.

---

## ISSUE-005 — Define validation rules, soft warnings, and hard blocks

**Priority:** P0  
**Labels:** `phase-0-validation`, `backend`, `frontend`, `mvp`  
**Depends on:** ISSUE-001, ISSUE-003

### Description

Create a validation rules document and implementation plan for project safety, scope control, and usability.

### Soft warnings

Soft warnings allow the user to continue after acknowledgement.

Examples:

- Shelf span may need reinforcement.
- Depth seems unusually large.
- Stud spacing is wider than recommended default.
- Waste allowance is low.
- Structure may require additional anchoring.
- Site conditions must be verified.

### Hard blocks

Hard blocks stop final generation.

Examples:

- Load-bearing request
- Fireplace / BBQ / heat-related build
- Ceiling-hung or floating structure
- Curved or angled geometry
- Plumbing/electrical integration
- Structure intended to support people
- Unsupported or unrealistic dimensions

### Acceptance criteria

- [ ] Validation rules are documented.
- [ ] Each rule has a severity: `info`, `soft_warning`, or `hard_block`.
- [ ] Each rule has user-facing copy.
- [ ] Hard-blocked projects cannot generate material list or build guide.
- [ ] Soft warnings require acknowledgement before material generation.

---

## ISSUE-006 — Draft expert-review checklist

**Priority:** P0  
**Labels:** `phase-0-validation`, `qa`, `mvp`  
**Depends on:** ISSUE-002, ISSUE-004, ISSUE-005

### Description

Prepare a checklist for a qualified drywall / light metal framing expert to review before private beta.

### Expert should review

- Default Europe/UK material preset
- Stud/profile assumptions
- Board size and board thickness assumptions
- Stud spacing defaults
- Reinforcement assumptions
- Warning thresholds
- Hard-block logic
- Material calculation rules
- Cut list logic
- Build guide templates
- Disclaimer wording

### Acceptance criteria

- [ ] Expert-review checklist exists.
- [ ] Checklist maps to product areas and developer modules.
- [ ] The product cannot be marked beta-ready until checklist is completed.
- [ ] Any expert corrections are tracked as follow-up issues.

---

## ISSUE-007 — Define safety and legal disclaimer copy

**Priority:** P0  
**Labels:** `phase-0-validation`, `frontend`, `pdf`, `mvp`  
**Depends on:** ISSUE-005

### Description

Define standard disclaimer copy shown during project review, material generation, PDF export, and shared client view.

### Required disclaimer locations

- Before skeleton generation / review step
- Before generating material list
- On materials/checklist screen
- In PDF footer or disclaimer section
- In shared client view

### Suggested copy

> This tool creates an estimated non-certified planning model based on the information provided. It does not replace professional construction judgement, site inspection, structural engineering, or building regulation approval.

> Material quantities are estimates based on selected assumptions. Verify all quantities, dimensions, site conditions, and supplier specifications before purchasing.

### Acceptance criteria

- [ ] Disclaimer text is stored centrally.
- [ ] Disclaimer text can be edited later from admin panel.
- [ ] PDF and shared pages include disclaimer.
- [ ] Material checklist includes verify-before-purchase note.

---

# Phase 1 — Wall partition technical prototype

---

## ISSUE-008 — Scaffold Nuxt/Vue MVP application

**Priority:** P0  
**Labels:** `phase-1-prototype`, `frontend`, `mvp`  
**Depends on:** ISSUE-003

### Description

Create the initial Nuxt/Vue application structure.

### Requirements

- Nuxt app initialized
- TypeScript enabled
- Basic routing structure
- UI framework selected and configured, preferably Nuxt UI + Tailwind
- Environment variables structure created
- Linting/formatting configured
- Basic layout shell created

### Acceptance criteria

- [ ] App runs locally.
- [ ] TypeScript is enabled.
- [ ] Basic routes are available.
- [ ] UI component system is configured.
- [ ] Project includes README setup instructions.

---

## ISSUE-009 — Set up Supabase project and base data model

**Priority:** P1  
**Labels:** `phase-1-prototype`, `backend`, `mvp`  
**Depends on:** ISSUE-003, ISSUE-008

### Description

Create initial Supabase setup for later persistence, even if Phase 1 prototype can temporarily run with local state.

### Base tables

- `profiles`
- `projects`
- `material_presets`
- `project_outputs`
- `share_links`
- `feedback`

### Acceptance criteria

- [ ] Supabase project is connected to Nuxt app.
- [ ] Base migration files exist.
- [ ] Local development environment can connect to Supabase.
- [ ] Project JSON can be stored in `projects` table.
- [ ] Row-level security plan is documented, even if not fully implemented in prototype.

---

## ISSUE-010 — Implement unit conversion helper

**Priority:** P0  
**Labels:** `phase-1-prototype`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-003

### Description

Implement a unit conversion helper that accepts user inputs in mm, cm, or m and normalizes values to millimetres internally.

### Requirements

- Internal unit: mm
- User input examples supported: `2400 mm`, `240 cm`, `2.4 m`
- Validation for unrealistic or invalid values
- Output values shown in mm by default

### Acceptance criteria

- [ ] Inputs in mm/cm/m are parsed correctly.
- [ ] Values are stored internally as millimetres.
- [ ] Invalid input returns user-friendly validation error.
- [ ] Unit conversion has tests.

---

## ISSUE-011 — Build wall partition wizard

**Priority:** P0  
**Labels:** `phase-1-prototype`, `frontend`, `mvp`  
**Depends on:** ISSUE-008, ISSUE-010

### Description

Build the first guided wizard for creating a wall partition project.

### Required fields

- Project name
- Width
- Height
- Stud spacing: 600 mm default, 400 mm optional
- Board side: single-sided / double-sided / skeleton only
- Board layers: 1 default, 2 optional
- Material preset
- Installation context: wall/floor/ceiling/freestanding basics

### Acceptance criteria

- [ ] User can create a wall partition project from structured inputs.
- [ ] Required fields are validated.
- [ ] Defaults are pre-filled from material preset.
- [ ] User can proceed to skeleton generation only with valid data.

---

## ISSUE-012 — Implement wall partition parametric generation engine

**Priority:** P0  
**Labels:** `phase-1-prototype`, `backend`, `3d`, `mvp`  
**Depends on:** ISSUE-003, ISSUE-011

### Description

Implement deterministic wall partition skeleton generation from structured project parameters.

### Generated elements

- Bottom U-track
- Top U-track
- Left/right side tracks if applicable
- Vertical C-studs
- Basic stud spacing
- Optional extra end studs

### Engine output

The engine should output a structured list of framing elements, not raw 3D mesh as source of truth.

Each framing element should include:

- `id`
- `type`
- `profileType`
- `position`
- `rotation`
- `lengthMm`
- `dimensionsMm`
- `label`

### Acceptance criteria

- [ ] Engine produces deterministic output for same input.
- [ ] Track and stud positions are dimensionally accurate.
- [ ] Stud count updates when width or spacing changes.
- [ ] Output can be consumed by 3D viewer and material calculator.
- [ ] Unit tests cover common wall partition examples.

---

## ISSUE-013 — Build Three.js 3D viewer shell

**Priority:** P0  
**Labels:** `phase-1-prototype`, `frontend`, `3d`, `mvp`  
**Depends on:** ISSUE-008, ISSUE-012

### Description

Create browser-based 3D viewer for displaying simplified rectangular framing elements.

### Required viewer features

- Render simplified studs/tracks as rectangular profiles
- Rotate
- Zoom
- Pan
- Reset view
- Front view
- Side view
- Top view
- Perspective view
- Basic camera controls

### Acceptance criteria

- [ ] Viewer renders wall partition skeleton from generated elements.
- [ ] User can rotate, zoom, and pan.
- [ ] User can switch basic views.
- [ ] Viewer works on desktop and tablet widths.
- [ ] Rendering remains performant for typical MVP projects.

---

## ISSUE-014 — Add basic dimension labels to 3D viewer

**Priority:** P0  
**Labels:** `phase-1-prototype`, `frontend`, `3d`, `mvp`  
**Depends on:** ISSUE-013

### Description

Add simple dimension annotations to the 3D viewer.

### Required labels

- Overall width
- Overall height
- Stud spacing
- Individual profile length on hover/click

### Acceptance criteria

- [ ] Overall wall width and height are visible.
- [ ] Stud spacing label is visible.
- [ ] User can toggle dimensions on/off.
- [ ] Clicking or hovering a profile shows profile type and length.

---

## ISSUE-015 — Implement wall partition material calculator

**Priority:** P0  
**Labels:** `phase-1-prototype`, `backend`, `mvp`  
**Depends on:** ISSUE-004, ISSUE-012

### Description

Generate estimated material checklist for wall partition projects.

### Required materials

- C-stud profiles
- U-track profiles
- Plasterboard sheets
- Drywall screws
- Anchors/fixings
- Joint tape
- Joint compound
- Corner bead if relevant
- Waste allowance note

### Acceptance criteria

- [ ] Material list is generated from project parameters and material preset.
- [ ] Quantities are rounded upward.
- [ ] Waste allowance is included.
- [ ] Items are marked as auto-calculated.
- [ ] User-facing copy says quantities are estimates.

---

## ISSUE-016 — Implement basic cut list for wall partition

**Priority:** P0  
**Labels:** `phase-1-prototype`, `backend`, `mvp`  
**Depends on:** ISSUE-012, ISSUE-015

### Description

Generate a basic cut list for wall partition profiles.

### Cut list should include

- Profile type
- Length to cut
- Quantity
- Source material length assumption
- Notes

### Acceptance criteria

- [ ] Vertical stud cuts are listed by height.
- [ ] Top/bottom track cuts are listed by width.
- [ ] Cut list groups identical lengths.
- [ ] Cut list is clearly marked as basic and not optimized nesting.

---

## ISSUE-017 — Build simple prototype PDF export

**Priority:** P0  
**Labels:** `phase-1-prototype`, `pdf`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-013, ISSUE-014, ISSUE-015, ISSUE-016

### Description

Create a simple PDF export for the wall partition prototype.

### PDF includes

- Project name
- Project type
- Overall dimensions
- One skeleton screenshot
- Basic material checklist
- Basic cut list
- Disclaimer

### Acceptance criteria

- [ ] User can export a wall partition project as PDF.
- [ ] PDF includes a skeleton preview.
- [ ] PDF includes material checklist and cut list.
- [ ] PDF includes disclaimer.
- [ ] Exported PDF is readable and client-presentable enough for prototype validation.

---

## ISSUE-018 — QA wall partition prototype end-to-end

**Priority:** P0  
**Labels:** `phase-1-prototype`, `qa`, `mvp`  
**Depends on:** ISSUE-011, ISSUE-012, ISSUE-013, ISSUE-015, ISSUE-016, ISSUE-017

### Description

Test the complete wall partition prototype flow.

### Test flow

1. Enter wall partition dimensions.
2. Generate skeleton.
3. Inspect 3D viewer.
4. Toggle dimensions.
5. Generate material checklist.
6. Generate cut list.
7. Export PDF.

### Acceptance criteria

- [ ] Full flow works without developer intervention.
- [ ] First skeleton can be generated in under 5 minutes by a test user.
- [ ] Material list updates when project dimensions change.
- [ ] PDF export works reliably.
- [ ] Known limitations are documented before Phase 2.

---

# Phase 2 — Core MVP foundation

---

## ISSUE-019 — Implement Supabase Auth account flow

**Priority:** P1  
**Labels:** `phase-2-core`, `backend`, `frontend`, `security`, `mvp`  
**Depends on:** ISSUE-009

### Description

Implement account creation and login. Users can start creating without an account, but need an account to save, duplicate, export, or share.

### Requirements

- Email/password login
- Optional Google login if practical
- Auth-protected dashboard
- Account required for save/export/share
- Public unauthenticated project creation preview remains possible

### Acceptance criteria

- [ ] User can create account.
- [ ] User can log in/out.
- [ ] Unauthenticated user can create and preview a project locally.
- [ ] Save/export/share prompts login if user is not authenticated.
- [ ] Project ownership is associated with authenticated user.

---

## ISSUE-020 — Implement project dashboard

**Priority:** P1  
**Labels:** `phase-2-core`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-019

### Description

Create a dashboard for logged-in users to manage saved projects.

### Dashboard shows

- Project name
- Project type
- Last edited date
- Output status: current / outputs outdated
- Buttons: open, duplicate, export, share, delete if implemented

### Acceptance criteria

- [ ] Logged-in user can see their own projects.
- [ ] Projects are sorted by last edited date.
- [ ] User can open a project from dashboard.
- [ ] User cannot see other users’ projects.
- [ ] Dashboard works on desktop and tablet.

---

## ISSUE-021 — Save and load project structured JSON

**Priority:** P1  
**Labels:** `phase-2-core`, `backend`, `frontend`, `mvp`  
**Depends on:** ISSUE-019, ISSUE-020

### Description

Persist project structured parameters as the source of truth. The app should regenerate 3D skeleton and outputs from project JSON.

### Requirements

- Save project parameters
- Load project parameters
- Regenerate skeleton from saved data
- Do not store generated mesh as source of truth
- Store preview images only as optional export/share assets

### Acceptance criteria

- [ ] Saved project reloads correctly.
- [ ] 3D skeleton is regenerated from saved parameters.
- [ ] Material list can be regenerated from saved parameters.
- [ ] Invalid saved JSON fails safely with an error message.

---

## ISSUE-022 — Implement duplicate project

**Priority:** P1  
**Labels:** `phase-2-core`, `backend`, `frontend`, `mvp`  
**Depends on:** ISSUE-021

### Description

Allow users to duplicate a project instead of implementing full version history.

### Acceptance criteria

- [ ] User can duplicate any project they own.
- [ ] Duplicated project copies parameters, material assumptions, and checklist state where appropriate.
- [ ] Duplicated project gets a new ID and name suffix such as “Copy”.
- [ ] Original project remains unchanged.

---

## ISSUE-023 — Implement editable material presets

**Priority:** P1  
**Labels:** `phase-2-core`, `backend`, `admin`, `mvp`  
**Depends on:** ISSUE-002, ISSUE-009

### Description

Store material presets in Supabase and make them consumable by project wizard and calculators.

### MVP requirement

The user can select the default preset and edit project-level assumptions in Advanced Settings. Full admin editing comes later in ISSUE-049/050.

### Acceptance criteria

- [ ] Default Europe/UK preset exists in database.
- [ ] Project wizard loads default preset.
- [ ] Project-level assumptions can override default values.
- [ ] Calculators use the selected/overridden assumptions.
- [ ] Preset fields are validated.

---

## ISSUE-024 — Implement editable material checklist state

**Priority:** P1  
**Labels:** `phase-2-core`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-015, ISSUE-021

### Description

Allow users to edit generated material checklists and save checklist progress.

### User can

- Check/uncheck items
- Add custom items
- Remove items
- Change quantities
- Add notes

### Item metadata

Each item should indicate:

- Auto-calculated
- Manually edited
- Manually added

### Acceptance criteria

- [ ] Material checklist is editable.
- [ ] Checklist state persists after reload.
- [ ] Auto-calculated vs manual items are visually distinguishable.
- [ ] User can add a custom material item.
- [ ] User can add notes to checklist items.

---

## ISSUE-025 — Implement tools checklist

**Priority:** P1  
**Labels:** `phase-2-core`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-021

### Description

Generate and persist a separate tools checklist based on project template.

### Default tools

- Tape measure
- Laser level or spirit level
- Pencil/marker
- Tin snips or metal cutting tool
- Drill/driver
- Drywall screw bit
- Utility knife
- Straight edge
- Plasterboard saw
- Sanding block
- Protective gloves
- Safety glasses

### Acceptance criteria

- [ ] Tools checklist is generated for a project.
- [ ] Tools checklist is separate from material checklist.
- [ ] User can check/uncheck tools.
- [ ] User can add/remove tools.
- [ ] Tools checklist state persists.

---

## ISSUE-026 — Implement build guide checklist framework

**Priority:** P1  
**Labels:** `phase-2-core`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-006, ISSUE-021

### Description

Build framework for step-by-step build guide as checkable tasks.

### Build guide sections

- Preparation
- Marking out
- Frame installation
- Boarding
- Finishing

### Step fields

- Title
- Short instruction
- Related materials/tools if relevant
- Warning note if applicable
- Completed/not completed
- Optional user note

### Acceptance criteria

- [ ] Build guide is shown as checklist, not plain text only.
- [ ] User can mark steps complete.
- [ ] Step completion persists.
- [ ] Build guide is generated from template logic, not freeform LLM output.

---

## ISSUE-027 — Implement output invalidation after design changes

**Priority:** P1  
**Labels:** `phase-2-core`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-021, ISSUE-024, ISSUE-026

### Description

If project parameters change after material outputs have been generated, mark material list, cut list, and build guide as outdated.

### Rules

- Current editable project remains latest source of truth.
- Last generated outputs are marked outdated after relevant parameter change.
- User can regenerate outputs.
- Manual checklist additions are preserved where possible.
- Auto-calculated items are recalculated.
- Manually edited calculated items are flagged for review or reset.

### Acceptance criteria

- [ ] Changing dimensions marks outputs as outdated.
- [ ] Changing material assumptions marks outputs as outdated.
- [ ] User sees clear warning that outputs may no longer match design.
- [ ] Regenerate button recalculates outputs.
- [ ] Manually added items are preserved during regeneration.

---

# Phase 3 — Full MVP templates and workspace

---

## ISSUE-028 — Implement box/counter wizard schema and UI

**Priority:** P1  
**Labels:** `phase-3-templates`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-003, ISSUE-011

### Description

Create guided wizard inputs for box/counter projects.

### Required fields

- Width
- Height
- Depth
- Number of vertical sections
- Top support/reinforcement option
- Board coverage sides
- Stud spacing
- Material preset
- Installation context

### Acceptance criteria

- [ ] User can create valid box/counter project.
- [ ] Width, height, depth are required.
- [ ] Inputs are validated against schema.
- [ ] Defaults load from material preset.
- [ ] Invalid dimensions produce useful error messages.

---

## ISSUE-029 — Implement box/counter skeleton engine

**Priority:** P1  
**Labels:** `phase-3-templates`, `backend`, `3d`, `mvp`  
**Depends on:** ISSUE-012, ISSUE-028

### Description

Generate simplified 3D metal stud skeleton for box/counter structures.

### Generated elements

- Bottom rectangular frame
- Top rectangular frame
- Vertical supports
- Side supports
- Optional internal section dividers
- Optional top reinforcement

### Acceptance criteria

- [ ] Engine generates dimensionally accurate 3D box/counter frame.
- [ ] Depth is represented correctly.
- [ ] Number of sections changes internal supports.
- [ ] Output works in existing 3D viewer.
- [ ] Generated elements feed cut list and material calculator.

---

## ISSUE-030 — Implement box/counter material and board calculations

**Priority:** P1  
**Labels:** `phase-3-templates`, `backend`, `mvp`  
**Depends on:** ISSUE-029

### Description

Generate materials, cut list, plasterboard estimate, tools, and build guide data for box/counter structures.

### Acceptance criteria

- [ ] C-stud/U-track estimates are generated.
- [ ] Cut list groups identical lengths.
- [ ] Board quantity is estimated based on selected coverage.
- [ ] Reinforcement option affects material list.
- [ ] Outputs are marked as estimates.

---

## ISSUE-031 — Implement TV wall/shelving wizard schema and UI

**Priority:** P1  
**Labels:** `phase-3-templates`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-003, ISSUE-028

### Description

Create guided wizard for the main showcase template: TV wall / shelving.

### Required fields

- Width
- Height
- Depth
- Layout type
- TV opening width
- TV opening height
- TV opening position
- Left shelves: yes/no/count
- Right shelves: yes/no/count
- Shelf spacing or auto distribute
- Reinforcement around opening: default yes
- Board coverage
- Stud spacing
- Material preset
- Installation context

### Acceptance criteria

- [ ] User can create TV wall/shelving project from structured inputs.
- [ ] TV opening cannot exceed available space.
- [ ] Shelf count and layout options are validated.
- [ ] Defaults produce a reasonable starting design.
- [ ] Wizard clearly explains what each field means.

---

## ISSUE-032 — Implement TV wall/shelving skeleton engine

**Priority:** P1  
**Labels:** `phase-3-templates`, `backend`, `3d`, `mvp`  
**Depends on:** ISSUE-029, ISSUE-031

### Description

Generate simplified 3D skeleton for TV wall / shelving structures.

### Generated elements

- Outer frame
- Vertical studs
- Horizontal shelf supports
- Central TV opening frame
- Reinforcement around TV/opening
- Left/right shelf zones
- Optional bottom counter/plinth if included by layout

### Acceptance criteria

- [ ] TV wall skeleton renders correctly in 3D viewer.
- [ ] TV opening dimensions match input.
- [ ] Shelves are generated on selected sides.
- [ ] Reinforcement elements are added around opening.
- [ ] Changes to shelf count or opening size update the skeleton.

---

## ISSUE-033 — Implement TV wall/shelving material and cut list calculations

**Priority:** P1  
**Labels:** `phase-3-templates`, `backend`, `mvp`  
**Depends on:** ISSUE-032

### Description

Generate estimated material checklist and cut list for TV wall/shelving structures.

### Acceptance criteria

- [ ] Profiles are calculated from generated skeleton elements.
- [ ] Horizontal shelf supports are included.
- [ ] Reinforcement profiles are included.
- [ ] Plasterboard estimate respects board coverage settings.
- [ ] Cut list groups repeated shelf support lengths.
- [ ] Warnings are shown for large openings/spans where needed.

---

## ISSUE-034 — Add simple plasterboard overlay toggle

**Priority:** P1  
**Labels:** `phase-3-templates`, `frontend`, `3d`, `mvp`  
**Depends on:** ISSUE-013, ISSUE-029, ISSUE-032

### Description

Add optional simple plasterboard overlay view to 3D viewer.

### Viewer modes

- Skeleton mode — default
- Board overlay mode
- Combined mode if technically feasible

### Non-goals

- No photorealistic finish
- No texture/material realism
- No exact board seam optimization
- No final interior render

### Acceptance criteria

- [ ] User can toggle board overlay on/off.
- [ ] Overlay reflects single-sided/double-sided coverage where applicable.
- [ ] Skeleton remains primary/default view.
- [ ] Overlay is visually simple and performance-friendly.

---

## ISSUE-035 — Implement complete validation engine

**Priority:** P1  
**Labels:** `phase-3-templates`, `backend`, `frontend`, `mvp`  
**Depends on:** ISSUE-005, ISSUE-028, ISSUE-031

### Description

Build validation engine that applies schema validation, construction sanity checks, soft warnings, and hard blocks across all templates.

### Acceptance criteria

- [ ] Validation runs before skeleton generation.
- [ ] Validation runs before material output generation.
- [ ] Soft warnings are visible and acknowledgeable.
- [ ] Hard blocks prevent material/build output generation.
- [ ] All warning/block messages are user-friendly.
- [ ] Validation results are stored with the project output where useful.

---

## ISSUE-036 — Build unified project workspace

**Priority:** P1  
**Labels:** `phase-3-templates`, `frontend`, `mvp`  
**Depends on:** ISSUE-020, ISSUE-024, ISSUE-026, ISSUE-034

### Description

Create one unified project workspace instead of separate disconnected pages.

### Workspace areas

- 3D viewer main area
- Side panel for editable parameters
- Validation warning area
- Tabs or sections:
  - Design
  - Materials
  - Build Guide
  - Export & Share

### Acceptance criteria

- [ ] User can edit parameters and see skeleton update.
- [ ] Materials tab shows material, tools, and cut list.
- [ ] Build Guide tab shows step checklist.
- [ ] Export & Share tab contains PDF/share controls.
- [ ] Workspace is usable on desktop and tablet.

---

## ISSUE-037 — Implement responsive support for desktop/tablet and mobile viewing

**Priority:** P1  
**Labels:** `phase-3-templates`, `frontend`, `qa`, `mvp`  
**Depends on:** ISSUE-036

### Description

Optimize full project creation for desktop and tablet. Mobile should support viewing shared projects and checklists, but does not need full editing parity.

### Acceptance criteria

- [ ] Desktop project creation works well.
- [ ] Tablet project creation is usable.
- [ ] Mobile can open shared project links.
- [ ] Mobile can view project summary and checklists.
- [ ] Mobile does not break critical layouts.

---

# Phase 4 — AI assistant layer

---

## ISSUE-038 — Add server-side LLM integration

**Priority:** P1  
**Labels:** `phase-4-ai`, `backend`, `ai`, `security`, `mvp`  
**Depends on:** ISSUE-003, ISSUE-035

### Description

Create secure server-side integration with an LLM provider. Do not expose API keys to client.

### Requirements

- Server-side Nuxt API route
- Environment variable configuration
- Request/response logging strategy without storing sensitive content unnecessarily
- Error handling
- Timeout handling
- Rate limiting or basic abuse protection

### Acceptance criteria

- [ ] LLM calls happen server-side only.
- [ ] API keys are not exposed in browser.
- [ ] Failed AI requests produce graceful fallback.
- [ ] LLM responses are parsed and validated before use.

---

## ISSUE-039 — Implement AI description-to-schema for wall partition

**Priority:** P1  
**Labels:** `phase-4-ai`, `backend`, `ai`, `mvp`  
**Depends on:** ISSUE-038, ISSUE-011

### Description

Allow user to describe a wall partition in natural language. AI should convert description into structured wall partition parameters.

### Example input

> I need a 3m wide partition, 2.4m high, double-sided plasterboard, with 600mm stud spacing.

### Acceptance criteria

- [ ] AI returns structured data matching `WallPartitionProject` schema.
- [ ] Missing critical fields trigger clarification question.
- [ ] Non-critical fields can use visible defaults.
- [ ] User must review and approve AI-filled values before generation.
- [ ] Invalid AI output is rejected by schema validation.

---

## ISSUE-040 — Implement AI description-to-schema for box/counter and TV wall/shelving

**Priority:** P1  
**Labels:** `phase-4-ai`, `backend`, `ai`, `mvp`  
**Depends on:** ISSUE-039, ISSUE-028, ISSUE-031

### Description

Extend AI interpretation to all MVP templates.

### Acceptance criteria

- [ ] AI can identify project type from user description when clear.
- [ ] AI can populate box/counter fields.
- [ ] AI can populate TV wall/shelving fields.
- [ ] Unsupported requests are flagged instead of forced into a template.
- [ ] User must confirm structured fields before skeleton generation.

---

## ISSUE-041 — Implement AI clarification question flow

**Priority:** P1  
**Labels:** `phase-4-ai`, `frontend`, `backend`, `ai`, `mvp`  
**Depends on:** ISSUE-039, ISSUE-040

### Description

If critical details are missing, the AI should ask concise clarification questions instead of silently guessing.

### Critical details

- Project type
- Width
- Height
- Depth for 3D structures
- Main opening sizes
- Basic layout
- Load-heavy items
- Wall/floor/ceiling attachment context

### Acceptance criteria

- [ ] Missing critical fields create targeted clarification questions.
- [ ] User answers update structured project fields.
- [ ] Clarification flow does not feel like an endless chat.
- [ ] User can skip AI and fill fields manually.

---

## ISSUE-042 — Build AI-assisted wizard prefill UX

**Priority:** P1  
**Labels:** `phase-4-ai`, `frontend`, `ai`, `mvp`  
**Depends on:** ISSUE-041

### Description

Add optional “Describe your project” entry point that pre-fills wizard fields using AI.

### UX requirements

- Description input is optional.
- AI pre-fills fields.
- AI-filled fields are visibly editable.
- User sees a review screen before generation.
- User can manually override any AI-filled value.

### Acceptance criteria

- [ ] User can describe a project at the start.
- [ ] Wizard fields are pre-filled from AI output.
- [ ] User can edit all fields before generation.
- [ ] AI does not bypass schema validation.

---

## ISSUE-043 — Add AI explanations and project summaries

**Priority:** P2  
**Labels:** `phase-4-ai`, `frontend`, `backend`, `ai`, `mvp`  
**Depends on:** ISSUE-042

### Description

Use AI to make the app easier to understand, without letting AI create construction rules.

### AI may help with

- Explaining what a setting means
- Summarizing project assumptions
- Explaining warnings in plain English
- Rewording template-based instructions for clarity

### Acceptance criteria

- [ ] AI can generate short project summary.
- [ ] AI can explain user-facing settings.
- [ ] AI cannot invent new construction rules.
- [ ] Safety-related content is based on approved templates/rules.

---

## ISSUE-044 — Add AI safety guardrails and unsupported request handling

**Priority:** P1  
**Labels:** `phase-4-ai`, `backend`, `ai`, `security`, `mvp`  
**Depends on:** ISSUE-035, ISSUE-038

### Description

Ensure AI does not produce unsupported or unsafe project recommendations.

### Requirements

- Prompt clearly states MVP scope.
- AI must refuse or flag unsupported requests.
- AI output always goes through schema validation.
- AI cannot directly generate 3D geometry.
- AI cannot override hard blocks.

### Acceptance criteria

- [ ] AI flags fireplace/BBQ/load-bearing requests as unsupported.
- [ ] AI does not return geometry meshes.
- [ ] AI cannot bypass hard-block validation.
- [ ] Unsupported requests receive clear, helpful messages.

---

# Phase 5 — Sharing, branding, admin, analytics, beta hardening

---

## ISSUE-045 — Build full PDF project pack export

**Priority:** P1  
**Labels:** `phase-5-beta`, `pdf`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-017, ISSUE-036

### Description

Upgrade prototype PDF into full project pack export.

### PDF sections

- Project overview
- Project assumptions
- Skeleton previews: front, side, top, perspective if possible
- Key dimensions
- Material checklist
- Tools checklist
- Basic cut list
- Build guide checklist
- Warnings
- Disclaimers
- Contractor branding if configured

### Acceptance criteria

- [ ] PDF includes all required sections.
- [ ] PDF includes contractor branding when available.
- [ ] PDF includes warnings and disclaimers.
- [ ] PDF can be downloaded from project workspace.
- [ ] PDF can be included in shared full project pack if enabled.

---

## ISSUE-046 — Implement contractor branding settings

**Priority:** P1  
**Labels:** `phase-5-beta`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-019, ISSUE-045

### Description

Allow project owners to add basic branding for PDFs and shared pages.

### Fields

- Company name
- Logo upload
- Contact name
- Phone
- Email
- Website optional

### Acceptance criteria

- [ ] User can save branding settings.
- [ ] User can upload logo.
- [ ] Branding appears in PDF.
- [ ] Branding appears in shared project page.
- [ ] Missing branding falls back gracefully.

---

## ISSUE-047 — Implement view-only share links

**Priority:** P1  
**Labels:** `phase-5-beta`, `frontend`, `backend`, `security`, `mvp`  
**Depends on:** ISSUE-019, ISSUE-021, ISSUE-036

### Description

Allow project owners to create unlisted view-only share links that do not require client login.

### Client can view

- 3D skeleton
- Dimensions
- Project summary
- Warnings/disclaimers
- Optional full project pack depending on share mode

### Client cannot

- Edit project
- Change dimensions
- Regenerate materials
- Access owner dashboard

### Acceptance criteria

- [ ] Owner can generate a share link.
- [ ] Shared link opens without login.
- [ ] Shared page is view-only.
- [ ] Shared page does not expose owner dashboard data.
- [ ] Owner can disable or regenerate link if implemented.

---

## ISSUE-048 — Implement share modes: Preview Only and Full Project Pack

**Priority:** P1  
**Labels:** `phase-5-beta`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-047

### Description

Add simple share mode control.

### Preview Only includes

- 3D skeleton
- Dimensions
- Project summary
- Warnings/disclaimers

### Full Project Pack includes

- 3D skeleton
- Dimensions
- Material checklist
- Tools checklist
- Cut list
- Build guide
- Optional PDF download

### Acceptance criteria

- [ ] Owner can choose Preview Only or Full Project Pack.
- [ ] Preview Only hides material/tools/build outputs.
- [ ] Full Project Pack shows all selected outputs.
- [ ] Owner can toggle PDF download on/off.

---

## ISSUE-049 — Build lightweight admin panel for beta access and users

**Priority:** P1  
**Labels:** `phase-5-beta`, `admin`, `backend`, `frontend`, `security`, `mvp`  
**Depends on:** ISSUE-019, ISSUE-020

### Description

Create an internal admin panel for managing beta users and manual Pro/unlimited flags.

### Admin can

- View users
- View project counts
- Set beta access / manual Pro flag
- Set saved project/export/share limits if implemented

### Acceptance criteria

- [ ] Admin-only route exists.
- [ ] Non-admin users cannot access admin panel.
- [ ] Admin can mark user as beta/pro/unlimited.
- [ ] Admin can view basic user/project info for support.

---

## ISSUE-050 — Add admin management for presets, warnings, and disclaimers

**Priority:** P1  
**Labels:** `phase-5-beta`, `admin`, `backend`, `frontend`, `mvp`  
**Depends on:** ISSUE-023, ISSUE-049

### Description

Allow admin to edit material preset values and user-facing warning/disclaimer copy. Core algorithms remain code-controlled.

### Admin can edit

- Profile type labels
- Standard profile lengths
- Board sizes
- Board thickness
- Default waste percentage
- Stud spacing defaults
- Warning copy
- Disclaimer copy

### Admin cannot edit in MVP

- Skeleton generation algorithms
- Geometry rules
- Reinforcement logic
- Calculation formulas

### Acceptance criteria

- [ ] Admin can edit material preset fields safely.
- [ ] Admin can edit disclaimer/warning copy.
- [ ] Edited presets validate before saving.
- [ ] Core generation logic is not editable from admin panel.

---

## ISSUE-051 — Implement product analytics events

**Priority:** P1  
**Labels:** `phase-5-beta`, `analytics`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-036, ISSUE-042, ISSUE-048

### Description

Track basic product analytics for MVP validation.

### Events to track

- Project started
- Template selected
- Dimensions entered
- Skeleton generated
- AI description submitted
- AI fields accepted/edited
- Material list generated
- Checklist manually edited
- PDF exported
- Share link created
- Soft warning shown
- Hard block triggered
- Feedback submitted

### Acceptance criteria

- [ ] Analytics events are implemented for key funnel steps.
- [ ] Events do not expose sensitive project details unnecessarily.
- [ ] Events can be reviewed during beta.
- [ ] Privacy approach is documented.

---

## ISSUE-052 — Add in-app feedback prompts

**Priority:** P1  
**Labels:** `phase-5-beta`, `analytics`, `frontend`, `mvp`  
**Depends on:** ISSUE-051

### Description

Collect lightweight qualitative feedback during beta.

### Feedback prompts

- Was this material list useful?
- Did the skeleton match what you wanted to build?
- What would you change before using this with a client?
- Would you send this project pack to a real client?

### Acceptance criteria

- [ ] Feedback prompt appears after project pack generation.
- [ ] User can submit rating and optional text.
- [ ] Feedback is stored in Supabase.
- [ ] Feedback is linked to project/template where appropriate.

---

## ISSUE-053 — Build lightweight onboarding and contextual hints

**Priority:** P1  
**Labels:** `phase-5-beta`, `frontend`, `mvp`  
**Depends on:** ISSUE-036

### Description

Create a short first-use onboarding flow and contextual helper hints.

### Onboarding steps

1. Choose a template or describe your project.
2. Review and adjust the generated skeleton.
3. Generate materials, tools, build checklist, PDF, and share link.

### Contextual hints

- Drag to rotate
- Scroll to zoom
- Click a stud to view length
- Toggle dimensions on/off
- Review assumptions before material generation

### Acceptance criteria

- [ ] First-time user sees lightweight intro.
- [ ] User can skip onboarding.
- [ ] 3D viewer includes helper hints.
- [ ] Onboarding does not block experienced users.

---

## ISSUE-054 — Add demo projects library

**Priority:** P1  
**Labels:** `phase-5-beta`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-028, ISSUE-031, ISSUE-036

### Description

Create prebuilt demo projects for each MVP template.

### Demo projects

1. Simple wall partition
   - 3000 mm × 2400 mm
   - 600 mm stud spacing
   - double-sided plasterboard

2. Basic box/counter
   - 2000 mm × 900 mm × 600 mm
   - simple rectangular frame
   - top support included

3. TV wall with shelves
   - 3000 mm × 2400 mm × 400 mm
   - central TV opening
   - shelves on both sides

### Acceptance criteria

- [ ] User can preview demo projects.
- [ ] User can duplicate demo as editable project.
- [ ] Demo projects work without broken outputs.
- [ ] Demo library is available from landing/start screen.

---

## ISSUE-055 — Implement privacy/data-use safeguards

**Priority:** P1  
**Labels:** `phase-5-beta`, `security`, `backend`, `frontend`, `mvp`  
**Depends on:** ISSUE-019, ISSUE-051

### Description

Ensure project data is private by default.

### Requirements

- Projects are private to owner unless shared.
- User project content is not used for AI training by default.
- Analytics are anonymized or minimized where possible.
- Voluntary feedback can be collected.
- Admin access is limited to support/beta review needs.

### Acceptance criteria

- [ ] Project RLS prevents cross-user access.
- [ ] Shared links expose only intended project data.
- [ ] Privacy copy is available in app.
- [ ] AI data handling is documented.
- [ ] User consent is required for public examples or marketing use.

---

## ISSUE-056 — Prepare private beta testing script

**Priority:** P1  
**Labels:** `phase-5-beta`, `qa`, `mvp`  
**Depends on:** ISSUE-052, ISSUE-054

### Description

Create a beta testing script for expert, contractor, and beginner testers.

### Beta group

- 1 qualified drywall / light metal framing expert
- 3–5 experienced contractors/builders
- 2–3 less experienced DIY testers

### Test tasks

- Create wall partition
- Create box/counter
- Create TV wall/shelving project
- Review skeleton
- Generate materials/tools/cut list/build guide
- Export PDF
- Share project link
- Provide feedback

### Acceptance criteria

- [ ] Beta script exists.
- [ ] Testers know exactly what to test.
- [ ] Feedback questions are prepared.
- [ ] Issues found during beta can be logged against templates/features.

---

## ISSUE-057 — Run expert review before private beta

**Priority:** P0  
**Labels:** `phase-5-beta`, `qa`, `mvp`  
**Depends on:** ISSUE-006, ISSUE-035, ISSUE-045

### Description

Before private beta, run expert review of construction logic, material assumptions, warnings, and build guide templates.

### Acceptance criteria

- [ ] Expert reviews material preset.
- [ ] Expert reviews material calculation outputs for sample projects.
- [ ] Expert reviews warning and hard-block rules.
- [ ] Expert reviews build guide templates.
- [ ] Corrections are logged as issues.
- [ ] Product is not marked beta-ready until critical corrections are completed.

---

## ISSUE-058 — Add deployment, environment, and release setup

**Priority:** P1  
**Labels:** `phase-5-beta`, `backend`, `frontend`, `security`, `mvp`  
**Depends on:** ISSUE-008, ISSUE-009, ISSUE-038

### Description

Set up deployable environments for development/staging/beta.

### Requirements

- Hosting configured for Nuxt app
- Supabase environment configured
- Environment variables documented
- LLM API keys stored securely
- Preview deploys if possible
- Basic error logging

### Acceptance criteria

- [ ] App can be deployed to staging/beta.
- [ ] Environment variables are documented.
- [ ] Secrets are not committed.
- [ ] Supabase connection works in deployed environment.
- [ ] LLM integration works in deployed environment.

---

## ISSUE-059 — Add E2E tests for critical MVP flows

**Priority:** P1  
**Labels:** `phase-5-beta`, `qa`, `frontend`, `backend`, `mvp`  
**Depends on:** ISSUE-036, ISSUE-045, ISSUE-048

### Description

Add end-to-end tests for the most important flows.

### Critical flows

- Create wall partition manually
- Generate skeleton
- Generate material list
- Export PDF
- Create account and save project
- Reload saved project
- Duplicate project
- Create share link
- Open shared view without login

### Acceptance criteria

- [ ] E2E tests cover critical flows.
- [ ] Tests can run in CI or local test command.
- [ ] Failing critical flow blocks release.
- [ ] Test data does not pollute production database.

---

## ISSUE-060 — Create final MVP acceptance checklist

**Priority:** P0  
**Labels:** `phase-5-beta`, `qa`, `mvp`  
**Depends on:** ISSUE-018, ISSUE-036, ISSUE-045, ISSUE-048, ISSUE-057, ISSUE-059

### Description

Create final MVP acceptance checklist based on the PRD completion definition.

### MVP is complete when users can

- Create projects for all three templates
- Use AI-assisted interpretation optionally
- Review and approve structured assumptions
- Generate dimensionally accurate simplified skeletons
- View dimensions and plasterboard overlay
- Generate material checklist, tools checklist, cut list, and build guide
- Save, duplicate, export, and share projects
- Use Preview Only and Full Project Pack sharing modes
- Add basic contractor branding
- See warnings, hard blocks, and disclaimers
- Provide feedback during beta

### Acceptance criteria

- [ ] Acceptance checklist exists.
- [ ] Each checklist item maps to one or more issues.
- [ ] Product owner signs off checklist before public launch.
- [ ] Known non-blocking limitations are documented.

---

# Backlog / Post-MVP roadmap issues

These are intentionally not MVP issues, but should be preserved as future product opportunities.

---

## ROADMAP-001 — Payment and subscription system

**Status:** Post-MVP  
**Reason:** MVP uses free limited beta access and manual Pro/unlimited flags.

Possible future features:

- Stripe subscription
- Free/pro limits
- Team plans
- Billing portal
- Usage-based exports or projects

---

## ROADMAP-002 — CAD/DWG/DXF export

**Status:** Post-MVP  
**Reason:** MVP focuses on browser 3D view and PDF project pack.

Possible future features:

- DXF export
- DWG export
- SketchUp export
- BIM/Revit integration
- Technical drawing sheets

---

## ROADMAP-003 — Supplier catalog and live pricing

**Status:** Post-MVP  
**Reason:** MVP uses generic material categories, not supplier-specific shopping lists.

Possible future features:

- Supplier product mapping
- Live prices
- Inventory availability
- Affiliate links
- Export shopping list to supplier basket

---

## ROADMAP-004 — Photo upload and room visualization

**Status:** Post-MVP  
**Reason:** MVP models only the drywall/light metal stud structure, not the surrounding room.

Possible future features:

- Upload room photo
- Scale calibration
- Place structure into photo
- Approximate finished visual preview
- AR-style preview

---

## ROADMAP-005 — Full team collaboration

**Status:** Post-MVP  
**Reason:** MVP has project owner, view-only client, and admin only.

Possible future features:

- Team workspaces
- Multiple editors
- Client comments
- Approval workflow
- Version history
- Task assignments

---

# Developer notes

## Architecture principles

- Store projects as structured parametric data.
- Regenerate 3D skeleton from project data.
- Do not treat generated mesh as source of truth.
- Use deterministic generation engine for geometry and materials.
- Use AI only for interpretation, clarification, explanations, and summaries.
- Validate AI output against strict schemas before using it.
- Keep construction logic in code, not freely editable from admin panel.
- Mark all generated material quantities as estimates.
- Keep safety disclaimers visible across project review, materials, PDF, and sharing.

## Suggested implementation order

1. Phase 0 validation documents and schemas
2. Nuxt app scaffold
3. Wall partition wizard
4. Wall partition skeleton engine
5. Three.js viewer
6. Wall partition materials/cut list/PDF
7. Supabase auth and project persistence
8. Dashboard/checklists/output invalidation
9. Box/counter template
10. TV wall/shelving template
11. Unified workspace
12. AI assistant layer
13. Sharing/PDF branding/admin/analytics
14. Expert review and private beta

## Definition of core technical success

The hardest technical proof is not AI. The first proof is:

> Can structured inputs reliably generate a clear, dimensionally accurate 3D skeleton and useful estimated material list for a wall partition?

Do not overbuild AI, payments, supplier integrations, or photorealistic rendering before this is proven.
