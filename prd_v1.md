# PRD v1 — Drywall / Light Metal Stud Project Design Web Application

**Document status:** Draft v1  
**Product type:** Web application / MVP  
**Primary target market:** Europe / UK, metric construction workflows  
**Preferred implementation stack:** Nuxt / Vue, Three.js, Supabase  
**Primary user:** Drywall / light metal framing contractors and experienced builders  
**Secondary user:** DIY / non-experienced users who need guided support

---

## 1. Product Overview

The product is a web application that helps users design simple drywall / light metal stud projects. Users choose a project template, enter dimensions and project parameters, optionally describe the project in natural language, and generate a simplified but dimensionally accurate 3D metal stud skeleton.

After reviewing and approving the skeleton, users can generate:

- estimated material checklist,
- tools checklist,
- basic cut list,
- step-by-step build guide,
- PDF project pack,
- view-only client share link.

The MVP focuses on planning and visualizing the internal metal stud skeleton, not on photorealistic finished interior design.

### Product positioning

A fast, visual drywall/light metal stud framing planner for contractors — simple enough for beginners, powerful enough for pros.

### Core product promise

Help contractors and builders go from project idea to clear skeleton, estimated materials, build checklist, and client-ready project pack.

---

## 2. Target Users

### 2.1 Primary user: contractors / experienced builders

The MVP should primarily serve:

- drywall contractors,
- light metal framing installers,
- interior fit-out contractors,
- builders who create simple built-in structures,
- professionals who want to present planned work to clients.

Primary users need speed, accuracy, visual clarity, and a practical material list.

### 2.2 Secondary user: DIY / less experienced users

The MVP should also be understandable for beginners through:

- guided wizard,
- plain language labels,
- helper tooltips,
- AI clarification questions,
- tool and material checklists,
- step-by-step build guide.

However, the app should not be optimized primarily for total beginners at the expense of professional usefulness.

---

## 3. MVP Scope

The MVP supports simple, rectilinear, non-load-bearing drywall/light metal stud structures only.

### 3.1 Included MVP project templates

The MVP includes three parametric project templates:

1. **Wall partition**
   - straight wall partition,
   - no complex openings in first prototype,
   - validates core framing, board calculation, cut list, and PDF export.

2. **Box / counter structure**
   - simple rectangular 3D frame,
   - useful for counters, low stands, plinths, and simple built-ins,
   - introduces depth and 3D framing.

3. **TV wall / shelving structure**
   - visually attractive showcase use case,
   - central TV/opening option,
   - shelves or compartments on left/right/both sides,
   - simple reinforcement around openings.

### 3.2 Main MVP outputs

The MVP generates:

- 3D simplified metal stud skeleton,
- optional simple plasterboard overlay,
- dimension labels,
- estimated materials checklist,
- tools checklist,
- basic cut list,
- checkable build guide,
- PDF project pack,
- view-only share link.

### 3.3 MVP construction assumptions

The MVP uses:

- Europe / UK metric defaults,
- millimetres as internal unit,
- generic material categories,
- editable material assumptions,
- non-certified planning logic,
- expert-reviewed construction rules before beta launch.

---

## 4. Out of Scope for MVP

The MVP does **not** support:

- curved walls,
- angled walls,
- load-bearing structures,
- structures that support people,
- suspended / ceiling-hung / floating structures,
- complex ceiling systems,
- staircases,
- multi-room layouts,
- kitchen systems with doors, hinges, drawers, appliances, plumbing, or electrical,
- fireplaces, BBQs, gas, heat, fire, or ventilation-adjacent structures,
- plumbing/electrical integration,
- full surrounding room modelling,
- photo upload / AR / “see it in my room” visualization,
- realistic finished renderings,
- CAD / DWG / DXF / BIM export,
- supplier-specific product catalogues,
- live pricing or purchasing,
- quotes or invoices,
- full subscription/payment system,
- full team collaboration,
- client comments / approval workflows,
- full version history,
- certified engineering drawings,
- building regulation compliance certification.

---

## 5. Product Principles

1. **Template-first, AI-assisted**  
   Templates and structured fields are the foundation. AI helps interpret, clarify, and explain.

2. **Deterministic generation, not AI geometry**  
   The LLM does not directly generate the 3D model. The app generates skeletons through a deterministic parametric engine.

3. **Fast and visual**  
   Once parameters are confirmed, skeleton updates should feel near-instant.

4. **Simple but useful**  
   The MVP should avoid CAD-level complexity while remaining practical for real contractors.

5. **Planning aid, not certification**  
   The product must consistently communicate that generated outputs are estimated planning aids.

6. **Editable assumptions**  
   Professionals must be able to adjust key material assumptions.

7. **Private by default**  
   User projects and client data are private unless explicitly shared by the user.

---

## 6. User Roles

### 6.1 Project owner

A logged-in builder/contractor/user who creates projects.

Can:

- create projects,
- edit parameters,
- generate skeletons,
- generate material lists,
- edit checklists,
- export PDFs,
- duplicate projects,
- create share links,
- manage basic contractor branding.

### 6.2 View-only client

A recipient of a shared project link.

Can:

- view the 3D skeleton,
- view dimensions,
- view project summary,
- view material/tools/build outputs if owner shares full project pack,
- download PDF if enabled by owner.

Cannot:

- edit project,
- change dimensions,
- modify checklists,
- regenerate materials,
- access owner dashboard.

### 6.3 Admin

Internal app owner/team role.

Can:

- view users,
- manage beta access,
- manually mark users as Pro/unlimited,
- manage material presets,
- manage warning/disclaimer text,
- view projects for support/debugging where appropriate.

---

## 7. Core MVP Screens

### 7.1 Landing / start screen

Purpose: explain the tool and let users start quickly.

Includes:

- product value proposition,
- “Create a project”,
- “Try demo project”,
- simple 3-step workflow explanation,
- sign in / create account.

### 7.2 Project dashboard

Available after login.

Includes:

- saved projects,
- project type,
- project status,
- last edited date,
- buttons: open, duplicate, export, share.

### 7.3 New project wizard

Main creation flow.

Steps:

1. Choose project type.
2. Enter main dimensions.
3. Define layout.
4. Select material assumptions.
5. Review assumptions and warnings.
6. Generate skeleton.

### 7.4 Unified project workspace

The core workspace after project creation.

Should include:

- 3D viewer,
- editable parameter side panel,
- validation warnings,
- tabs/panels for outputs.

Recommended workspace sections:

- **Design** — skeleton, dimensions, editable parameters.
- **Materials** — material checklist, tools checklist, cut list.
- **Build Guide** — step-by-step checkable task list.
- **Export & Share** — PDF export, share link, branding preview.

### 7.5 Shared client view

Public view-only link.

Modes:

1. **Preview Only**
   - 3D skeleton,
   - dimensions,
   - project summary,
   - warnings/disclaimers.

2. **Full Project Pack**
   - everything in Preview Only,
   - material checklist,
   - tools checklist,
   - cut list,
   - build guide,
   - optional PDF download.

### 7.6 Profile / branding settings

For contractor branding.

Includes:

- company name,
- logo upload,
- user/contact name,
- phone,
- email,
- website optional.

### 7.7 Admin panel

Lightweight internal panel.

Includes:

- users,
- beta limits,
- manual Pro/unlimited flag,
- material presets,
- warning/disclaimer text.

---

## 8. Main User Flows

### 8.1 Create project without account

1. User lands on app.
2. User chooses “Create project” or “Try demo project”.
3. User selects template.
4. User enters dimensions and layout.
5. User generates skeleton preview.
6. User can rotate, zoom, pan, inspect.
7. User must create account/login to save, export, duplicate, or share.

### 8.2 Create project with AI assistance

1. User enters natural language project description.
2. AI interprets description into structured fields.
3. App validates AI output against template-specific schema.
4. Missing critical details trigger clarification questions.
5. Non-critical values use transparent editable defaults.
6. User reviews and approves parameters.
7. Parametric engine generates skeleton.

### 8.3 Generate material outputs

1. User reviews skeleton and assumptions.
2. App displays warnings if relevant.
3. User clicks “Approve design & generate material list”.
4. App generates:
   - material checklist,
   - tools checklist,
   - cut list,
   - build guide.
5. User can edit checklists.
6. Checklist progress is saved per project.

### 8.4 Edit after generation

1. User changes design parameters after outputs were generated.
2. App marks material list, cut list, build guide, and PDF as outdated.
3. User is prompted to regenerate outputs.
4. Auto-calculated items are recalculated.
5. Manually added checklist items are preserved.
6. Manually edited calculated items are flagged for review or reset to the new calculated value.

### 8.5 Export PDF project pack

1. User opens Export & Share.
2. User confirms branding details.
3. App generates PDF with:
   - project overview,
   - skeleton views,
   - key dimensions,
   - material checklist,
   - tools checklist,
   - cut list,
   - build guide,
   - warnings/disclaimers.

### 8.6 Share with client

1. User selects share mode:
   - Preview Only,
   - Full Project Pack.
2. User optionally enables PDF download.
3. App creates unlisted view-only link.
4. Client opens link without login.

---

## 9. Template Requirements

## 9.1 Wall Partition Template

### Purpose

The simplest template and first technical prototype.

### Required fields

- project name,
- width,
- height,
- stud spacing,
- profile type,
- profile length,
- board coverage: single-sided / double-sided / skeleton only,
- board size,
- board thickness,
- installation context:
  - floor-fixed,
  - ceiling-fixed,
  - wall-fixed optional,
  - freestanding warning if relevant.

### Generated skeleton

Should include:

- bottom U-track,
- top U-track,
- vertical C-studs,
- optional side tracks/studs,
- simple dimension labels,
- stud spacing labels.

### Outputs

Should calculate:

- C-stud quantity,
- U-track quantity,
- plasterboard sheets,
- drywall screws,
- fixings/anchors,
- joint tape,
- joint compound,
- optional insulation,
- cut list for studs and tracks,
- build guide checklist.

### Acceptance criteria

- User can enter wall width and height in mm/cm/m.
- App normalizes dimensions to mm.
- App generates a correct simplified wall skeleton.
- Studs are spaced according to selected spacing.
- Material list is generated as estimated quantities.
- PDF export includes at least one skeleton screenshot, dimensions, and material checklist.

---

## 9.2 Box / Counter Template

### Purpose

Simple 3D rectangular frame for counters, plinths, low stands, and box-like built-ins.

### Required fields

- project name,
- width,
- height,
- depth,
- number of vertical sections optional,
- top support / reinforcement option,
- board coverage sides,
- stud spacing,
- material preset,
- installation context.

### Generated skeleton

Should include:

- front and back rectangular frames if applicable,
- vertical studs,
- horizontal top/bottom tracks,
- side depth profiles,
- optional intermediate supports,
- dimensions for width/height/depth.

### Outputs

Should calculate:

- metal profiles,
- plasterboard sheets based on selected covered sides,
- screws/fixings,
- cut list for vertical/horizontal/depth profiles,
- tools checklist,
- build guide checklist.

### Acceptance criteria

- User can generate a rectangular 3D box/counter skeleton.
- Depth is represented correctly.
- Material list updates when side coverage changes.
- App warns about unusually deep or unsupported structures.

---

## 9.3 TV Wall / Shelving Template

### Purpose

Primary showcase template for client presentation and market appeal.

### Required fields

- project name,
- width,
- height,
- depth,
- layout option:
  - shelves left,
  - shelves right,
  - shelves both sides,
  - central TV opening,
  - lower counter included/not included,
- TV/opening width,
- TV/opening height,
- shelf count,
- shelf spacing or auto-distribution,
- reinforcement around opening,
- board coverage,
- material preset,
- installation context.

### Generated skeleton

Should include:

- outer rectangular frame,
- central opening frame,
- vertical section divisions,
- shelf supports,
- horizontal supports,
- reinforcement around TV/opening,
- dimensions for key openings and shelves.

### Outputs

Should calculate:

- metal profile quantities,
- plasterboard sheet estimate,
- screws/fixings,
- reinforcement profiles if selected/required,
- corner bead where external corners exist,
- cut list,
- tools checklist,
- build guide checklist.

### Acceptance criteria

- User can create a TV wall/shelving skeleton with central opening and shelves.
- App prevents TV opening from exceeding available structure area.
- App warns if openings or shelves may need reinforcement.
- App generates client-presentable PDF/project pack.

---

## 10. AI Assistant Requirements

### 10.1 Role of AI

The AI assistant helps with:

- interpreting natural language project descriptions,
- pre-filling wizard fields,
- asking clarification questions,
- explaining settings,
- summarizing project assumptions,
- making approved instruction templates easier to read.

The AI must **not** directly generate the 3D mesh or construction geometry.

### 10.2 AI output validation

All AI-generated structured data must be:

- returned as structured JSON,
- validated against strict template-specific schemas,
- checked for missing critical fields,
- checked for invalid values,
- reviewed/approved by the user before generation.

### 10.3 Critical details AI must not silently guess

AI should ask clarification questions for:

- project type,
- width,
- height,
- depth for 3D structures,
- opening sizes,
- basic layout,
- intended use,
- heavy/load-related items,
- wall/floor/ceiling attachment context.

### 10.4 Non-critical defaults AI may apply transparently

AI/app may apply editable defaults for:

- stud spacing,
- board size,
- board thickness,
- profile length,
- waste allowance,
- screw spacing assumptions.

### 10.5 AI acceptance criteria

- AI can convert a simple English description into valid draft parameters.
- AI asks clarification questions when critical data is missing.
- AI-filled fields are visibly editable before skeleton generation.
- Invalid/out-of-scope AI interpretations are blocked by schema and validation rules.

---

## 11. 3D Viewer Requirements

### 11.1 Viewer purpose

The 3D viewer helps users understand and approve the generated light metal stud skeleton.

### 11.2 Required viewer features

- rotate,
- zoom,
- pan,
- perspective view,
- front view,
- side view,
- top view,
- clickable/hoverable profiles,
- profile length labels,
- overall dimensions,
- key internal dimensions,
- stud spacing labels,
- hide/show dimensions toggle,
- show/hide plasterboard overlay toggle.

### 11.3 Visual detail level

The MVP should use simplified profile geometry:

- clean rectangular beam/profile objects,
- dimensionally accurate placement and length,
- visually distinct studs/tracks,
- no photorealistic metal material,
- no exact folded C/U profile geometry,
- no screw holes or detailed manufacturing features.

### 11.4 Plasterboard overlay

The viewer should default to skeleton mode.

Optional overlay modes:

- skeleton only,
- simple board overlay,
- combined skeleton + semi-transparent board overlay if technically feasible.

The overlay is for understanding board coverage, not for exact board seam planning or finished rendering.

### 11.5 Acceptance criteria

- User can inspect skeleton from multiple angles.
- User can toggle dimensions on/off.
- User can view simplified board coverage.
- Viewer remains performant on desktop/tablet for MVP-size projects.

---

## 12. Material, Tools, Cut List, and Build Guide Requirements

## 12.1 Material checklist

The app generates an editable material checklist with estimated quantities.

Should include, depending on template:

- C-stud profiles,
- U-track profiles,
- plasterboard sheets,
- drywall screws,
- anchors/fixings,
- joint tape,
- joint compound,
- corner bead,
- optional insulation,
- optional reinforcement profiles.

Each item should include:

- checkbox,
- item name,
- estimated quantity,
- unit,
- notes,
- source type:
  - auto-calculated,
  - manually edited,
  - manually added.

### Acceptance criteria

- User can add custom material items.
- User can remove items.
- User can change quantities.
- User can add notes.
- App indicates which items were calculated automatically and which were manually changed.

---

## 12.2 Tools checklist

The app generates a separate editable tools checklist.

Example items:

- tape measure,
- laser level or spirit level,
- pencil/marker,
- tin snips or metal cutting tool,
- drill/driver,
- drywall screw bit,
- utility knife,
- straight edge,
- plasterboard saw,
- sanding block,
- protective gloves,
- safety glasses.

Tools are not quantity-calculated.

### Acceptance criteria

- Tools checklist is separate from materials.
- User can check/uncheck tools.
- User can add/remove tools.
- Tool checklist progress is saved per project.

---

## 12.3 Cut list

The app generates a basic cut list.

Should include:

- profile type,
- number of pieces,
- cut length,
- related location/section where useful.

The MVP does not need advanced cut optimization or nesting.

### Acceptance criteria

- Cut list includes vertical studs and horizontal tracks/supports.
- Cut lengths are derived from project parameters.
- Quantities update after regeneration.

---

## 12.4 Build guide checklist

The app generates a checkable step-by-step build guide from approved templates.

Sections may include:

1. Preparation
2. Marking out
3. Frame installation
4. Reinforcement
5. Boarding
6. Finishing
7. Final verification

Each step should include:

- checkbox,
- short instruction,
- related dimensions/materials where relevant,
- warning note if applicable.

### Build guide logic

The build guide should be template/rule-based first. The LLM may improve wording, but construction steps and safety guidance must come from approved templates and deterministic rules.

### Acceptance criteria

- Build guide is checkable.
- Progress is saved per project.
- Instructions include project-specific dimensions where relevant.
- Instructions include disclaimers and warnings where relevant.

---

## 13. Material Preset Requirements

### 13.1 Default Europe/UK metric preset

The MVP ships with a generic Europe/UK metric preset.

Recommended defaults:

- internal unit: millimetres,
- profile type: generic C-stud,
- track type: generic U-track,
- default profile width: 50 mm,
- default profile length: 3000 mm,
- stud spacing: 600 mm centres,
- optional advanced stud spacing: 400 mm centres,
- board size: 1200 × 2400 mm,
- board thickness: 12.5 mm,
- board layer: 1 layer default,
- waste allowance: 10%,
- screws estimated by board area,
- anchors/fixings estimated by track length,
- joint tape estimated by joints/perimeter,
- compound estimated by board area,
- corner bead added where external corners exist.

All values should be editable in advanced settings and reviewed by an expert before beta.

### 13.2 Editable assumptions

Users should be able to adjust:

- profile type/name,
- profile length,
- profile width,
- stud spacing,
- board size,
- board thickness,
- board layers,
- board coverage,
- waste percentage,
- screw spacing/estimate assumptions where exposed,
- reinforcement options.

### Acceptance criteria

- App provides default preset.
- Advanced users can edit core assumptions before generating outputs.
- Edited assumptions are saved with the project.

---

## 14. Validation, Warnings, and Hard Blocks

The MVP uses tiered validation.

## 14.1 Soft warnings

Soft warnings inform the user but allow them to continue after acknowledgement.

Examples:

- shelf span may need reinforcement,
- depth is unusually large,
- stud spacing is wider than recommended default,
- waste allowance is low,
- anchoring should be verified on-site,
- structure should be checked by a qualified builder.

## 14.2 Hard blocks

Hard blocks prevent final generation when the project is outside MVP scope.

Examples:

- load-bearing use,
- fireplace/BBQ/heat-related structure,
- ceiling-hung/floating/suspended structure,
- curved/angled structure,
- plumbing/electrical integration,
- structure designed to support people,
- dimensions far outside validated MVP limits,
- unsupported project type.

### Acceptance criteria

- Soft warnings can be acknowledged by the user.
- Hard blocks prevent material/build guide generation.
- Warnings are shown before generating material outputs.
- Warnings appear in PDF/shared project pack where relevant.

---

## 15. Safety and Legal Disclaimers

The MVP must clearly communicate that outputs are planning aids only.

### 15.1 Before skeleton generation / review step

Suggested copy:

> This tool creates an estimated non-certified planning model based on the information provided. It does not replace professional construction judgement, site inspection, or building regulation approval.

### 15.2 Before material purchase

Suggested copy:

> Material quantities are estimates based on selected assumptions. Verify all quantities, dimensions, site conditions, and supplier specifications before purchasing.

### 15.3 PDF and shared project page

Suggested copy:

> This project pack is a planning aid only. It is not a certified construction drawing, structural calculation, or building regulation approval. Consult a qualified professional where required.

### Acceptance criteria

- Disclaimers are visible during review, material generation, PDF export, and shared client viewing.
- PDF includes disclaimer in footer or final section.
- Shared links include disclaimer.

---

## 16. PDF Project Pack Requirements

The PDF should serve as a technical/client project pack, not as a quote or invoice.

### PDF sections

1. Project overview
   - project name,
   - project type,
   - dimensions,
   - generated date,
   - material assumptions.

2. Skeleton previews
   - front view,
   - side view,
   - top view,
   - perspective view where possible.

3. Key dimensions
   - total width,
   - height,
   - depth,
   - openings,
   - shelf spacing,
   - stud spacing.

4. Material checklist

5. Tools checklist

6. Cut list

7. Build guide checklist

8. Warnings and disclaimers

9. Contractor branding
   - company name,
   - logo,
   - contact details.

### Excluded from PDF MVP

- pricing,
- quote generation,
- invoice generation,
- supplier purchase links,
- advanced custom PDF templates.

### Acceptance criteria

- PDF can be generated from latest project output.
- PDF is marked outdated if project changes after generation.
- PDF includes contractor branding if configured.
- PDF includes disclaimer.

---

## 17. Sharing Requirements

### 17.1 Share link type

The MVP supports unlisted, view-only share links that do not require client login.

### 17.2 Share modes

1. **Preview Only**
   - 3D skeleton,
   - dimensions,
   - project summary,
   - warnings/disclaimers.

2. **Full Project Pack**
   - Preview Only content,
   - material checklist,
   - tools checklist,
   - cut list,
   - build guide,
   - optional PDF download.

### 17.3 PDF download toggle

Project owner can choose whether shared viewers may download the PDF.

### Not included in MVP

- password protection,
- link expiry,
- client comments,
- approval workflow,
- client accounts.

### Acceptance criteria

- Owner can create a share link.
- Client can open link without account.
- Client cannot edit project.
- Owner can choose Preview Only or Full Project Pack.

---

## 18. Account, Access, and Beta Limits

### 18.1 Account flow

Users can create and preview a project without an account.

Account required for:

- saving,
- exporting PDF,
- duplicating,
- sharing,
- accessing dashboard.

### 18.2 MVP access model

No full payment/subscription system in MVP.

Recommended access:

- free account,
- soft limits such as:
  - 3 saved projects,
  - 3 PDF exports,
  - limited share links,
- Pro plan placeholder,
- manual admin Pro/unlimited flag for beta users.

### Acceptance criteria

- User can test core creation before sign-up.
- User must sign up/log in to save/export/share.
- Admin can manually mark user as Pro/unlimited.

---

## 19. Admin Requirements

Admin should manage:

- users,
- beta limits,
- manual Pro/unlimited access,
- material presets,
- default assumptions,
- warning/disclaimer text.

Admin should **not** freely edit:

- skeleton generation algorithms,
- reinforcement logic,
- cut list formulas,
- core geometry rules.

These remain code-controlled and require expert review before changes.

### Acceptance criteria

- Admin can update material preset values.
- Admin can update disclaimer/warning copy.
- Admin can manage beta user access.
- Admin cannot accidentally change core generation logic from UI.

---

## 20. Data Model Assumptions

The source of truth should be structured project parameters, not saved 3D mesh files.

### 20.1 Common project fields

```ts
interface BaseProject {
  id: string
  ownerId: string
  projectName: string
  projectType: 'wall_partition' | 'box_counter' | 'tv_wall_shelving'
  unitSystem: 'metric'
  materialPresetId: string
  installationContext: InstallationContext
  createdAt: string
  updatedAt: string
  lastGeneratedOutputAt?: string
  outputsOutdated: boolean
}
```

### 20.2 Installation context

```ts
interface InstallationContext {
  attachedToExistingWall: boolean
  fixedToFloor: boolean
  fixedToCeiling: boolean
  builtIntoCorner: boolean
  freestanding: boolean
  decorativeOnly: boolean
  expectedToHoldHeavyItems: boolean
}
```

### 20.3 Wall partition schema example

```ts
interface WallPartitionProject extends BaseProject {
  projectType: 'wall_partition'
  dimensions: {
    widthMm: number
    heightMm: number
  }
  framing: {
    studSpacingMm: number
    profileWidthMm: number
    profileLengthMm: number
  }
  board: {
    coverage: 'none' | 'single_sided' | 'double_sided'
    layers: 1 | 2
    boardWidthMm: number
    boardHeightMm: number
    boardThicknessMm: number
    boardType: 'standard' | 'moisture_resistant' | 'fire_rated'
  }
}
```

### 20.4 Box/counter schema example

```ts
interface BoxCounterProject extends BaseProject {
  projectType: 'box_counter'
  dimensions: {
    widthMm: number
    heightMm: number
    depthMm: number
  }
  layout: {
    verticalSections: number
    topReinforcement: boolean
  }
  boardCoverage: {
    front: boolean
    back: boolean
    left: boolean
    right: boolean
    top: boolean
  }
  framing: FramingSettings
  board: BoardSettings
}
```

### 20.5 TV wall/shelving schema example

```ts
interface TvWallShelvingProject extends BaseProject {
  projectType: 'tv_wall_shelving'
  dimensions: {
    widthMm: number
    heightMm: number
    depthMm: number
  }
  layout: {
    shelvesLeft: boolean
    shelvesRight: boolean
    leftShelfCount?: number
    rightShelfCount?: number
    centralOpening: {
      enabled: boolean
      widthMm?: number
      heightMm?: number
      bottomOffsetMm?: number
    }
    lowerCounter: boolean
  }
  reinforcement: {
    aroundOpening: boolean
    shelfReinforcement: boolean
  }
  framing: FramingSettings
  board: BoardSettings
}
```

### 20.6 Checklist item schema example

```ts
interface ChecklistItem {
  id: string
  name: string
  quantity?: number
  unit?: string
  notes?: string
  checked: boolean
  source: 'auto_calculated' | 'manual_added' | 'manual_edited'
}
```

---

## 21. Privacy and Data Use

User project data is private by default.

The MVP may collect:

- anonymized product analytics,
- voluntary in-app feedback,
- support/debug access where appropriate.

The MVP must not automatically use private project data, client names, dimensions, images, or uploads for:

- AI training,
- public examples,
- marketing materials,
- product demos,

without explicit user consent.

### Acceptance criteria

- User project content is not used for AI training by default.
- Analytics are anonymized where possible.
- Public/demo usage requires explicit consent.

---

## 22. Analytics and Feedback Requirements

The MVP should include basic product analytics and lightweight in-app feedback.

### 22.1 Events to track

Project creation funnel:

- project_started,
- template_selected,
- dimensions_entered,
- ai_description_submitted,
- ai_parameters_generated,
- clarification_requested,
- skeleton_generated,
- skeleton_edited,
- review_approved,
- material_list_generated,
- checklist_edited,
- build_guide_generated,
- pdf_exported,
- share_link_created.

Template usage:

- wall_partition_used,
- box_counter_used,
- tv_wall_shelving_used.

Validation:

- soft_warning_shown,
- soft_warning_acknowledged,
- hard_block_triggered,
- out_of_scope_request.

Output usefulness:

- material_list_useful_feedback,
- skeleton_match_feedback,
- pdf_shared_with_client.

### 22.2 Feedback prompts

After generating a project pack, ask:

- “Was this material list useful?”
- “Did the skeleton match what you wanted to build?”
- “What would you change before using this with a client?”

### Acceptance criteria

- Core funnel events are tracked.
- Feedback can be submitted from inside the app.
- Admin/product team can review beta feedback.

---

## 23. Onboarding and Demo Projects

### 23.1 Lightweight onboarding

First-use onboarding should explain:

1. Choose a template or describe your project.
2. Review and adjust the skeleton.
3. Generate materials, tools, cut list, build checklist, PDF, and share link.

Users should be able to skip onboarding.

### 23.2 Contextual hints

Examples:

- “Drag to rotate.”
- “Scroll to zoom.”
- “Click a stud to view length.”
- “Toggle dimensions on/off.”

### 23.3 Demo projects

MVP should include demo projects:

1. Simple wall partition  
   3000 mm wide × 2400 mm high, 600 mm stud spacing, double-sided board.

2. Basic box/counter  
   2000 mm wide × 900 mm high × 600 mm deep.

3. TV wall with shelves  
   3000 mm wide × 2400 mm high × 400 mm deep, central TV opening, shelves on both sides.

Each demo should allow:

- preview,
- duplicate/use as starting point.

---

## 24. Language and Localization

The MVP launches in English only.

However, the app should be structured for future localization:

- UI labels,
- warning messages,
- checklist labels,
- instruction templates,
- PDF sections,
- admin preset labels.

Multi-language support is not required in MVP.

---

## 25. Technical Assumptions

### 25.1 Preferred stack

- Frontend: Nuxt / Vue
- UI: Nuxt UI + Tailwind or equivalent Vue-friendly component system
- 3D: Three.js integrated into Vue/Nuxt
- Backend/database: Supabase
- Auth: Supabase Auth
- Storage: Supabase Storage
- Database: Supabase Postgres
- LLM integration: server-side Nuxt API routes
- PDF generation: server-side route or background job
- Hosting: Nuxt-compatible hosting such as Netlify/Vercel or equivalent

### 25.2 Architecture principles

- Project parameters are source of truth.
- 3D mesh is regenerated from structured data.
- LLM output is validated before use.
- Parametric engine handles geometry and calculations.
- Core generation logic is deterministic.
- Material presets are configurable.
- Core construction algorithms are code-controlled.

---

## 26. Phased Build Plan

### Phase 0 — Product and construction validation

- Confirm supported templates.
- Confirm Europe/UK material assumptions.
- Get expert input on framing rules.
- Define strict template schemas.
- Define warnings and hard blocks.
- Define build instruction templates.

### Phase 1 — Technical prototype

Wall partition only.

Includes:

- structured inputs,
- parametric skeleton,
- 3D viewer,
- basic dimensions,
- basic material list,
- basic cut list,
- simple PDF export.

Excludes:

- AI assistant,
- accounts,
- sharing,
- admin panel,
- other templates.

### Phase 2 — Core MVP foundation

- user accounts,
- saved projects,
- project dashboard,
- duplicate project,
- editable checklists,
- checklist progress,
- material presets.

### Phase 3 — Full MVP templates

- box/counter template,
- TV wall/shelving template,
- plasterboard overlay,
- validation rules,
- build guide templates.

### Phase 4 — AI assistant layer

- describe project,
- pre-fill wizard,
- ask clarification questions,
- explain settings,
- summarize project assumptions,
- validate structured output.

### Phase 5 — Sharing, branding, beta

- view-only share links,
- Preview Only / Full Project Pack modes,
- PDF branding,
- admin panel,
- analytics,
- feedback collection,
- private beta.

---

## 27. First Technical Prototype Definition

The first prototype should prove wall partition end-to-end.

### Prototype includes

- wall partition wizard,
- width and height inputs,
- stud spacing,
- board side option,
- material preset,
- parametric skeleton generation,
- top track,
- bottom track,
- vertical studs,
- dimension labels,
- 3D rotate/zoom/pan,
- basic material checklist,
- basic cut list,
- simple PDF export.

### Prototype excludes

- AI assistant,
- TV wall/shelving,
- box/counter,
- user accounts,
- share links,
- branding,
- admin panel,
- full build guide.

### Prototype success question

Can structured inputs reliably generate a useful 3D skeleton and estimated material list?

---

## 28. MVP Completion Definition

The MVP is complete when users can create, validate, edit, save, export, and share non-load-bearing drywall/light metal stud projects for the three supported templates using:

- guided inputs,
- AI-assisted interpretation,
- strict schema validation,
- parametric 3D skeleton generation,
- dimension labels,
- optional plasterboard overlay,
- estimated material checklist,
- tools checklist,
- cut list,
- build guide checklist,
- PDF export,
- client share links,
- basic contractor branding,
- admin-managed presets,
- analytics and feedback.

---

## 29. MVP Success Metrics

The MVP should be considered successful if beta users can:

1. **Create a valid project quickly**  
   Target: first skeleton generated in under 5 minutes.

2. **Understand the 3D skeleton without training**  
   Users can identify studs, tracks, dimensions, and openings.

3. **Trust the material checklist enough to review it**  
   Contractors say the generated list is directionally useful, even if adjusted.

4. **Use the PDF/share link with a client**  
   At least some beta contractors send a project pack or preview link to a real client.

5. **Complete the full flow without developer help**  
   Project creation → skeleton → review → material list → PDF/share works end-to-end.

6. **Provide useful feedback on calculation assumptions**  
   Beta/expert feedback identifies improvements to presets, warnings, and templates.

---

## 30. Beta Testing Plan

Before public launch, the MVP should go through private beta.

### Recommended beta group

- 1 drywall/light metal framing expert,
- 3–5 experienced contractors/builders,
- 2–3 less experienced DIY-style testers.

### Test tasks

Each tester should create at least:

- one wall partition,
- one box/counter,
- one TV wall/shelving project.

### Review criteria

Beta users should evaluate:

- skeleton clarity,
- skeleton accuracy,
- material checklist usefulness,
- cut list usefulness,
- build guide clarity,
- PDF clarity,
- share link clarity,
- warnings/disclaimers,
- whether they would use it with a real client.

---

## 31. Expert Review Requirement

Before public beta, a qualified drywall/light metal framing expert must review and approve:

- default Europe/UK material assumptions,
- profile types and standard lengths,
- stud spacing rules,
- reinforcement rules around openings,
- board calculation logic,
- screw/anchor quantity assumptions,
- project warnings,
- hard blocks,
- build instruction templates,
- disclaimer wording.

The app does not provide certified engineering or building regulation approval.

---

## 32. Future Roadmap Ideas

Post-MVP features may include:

- image upload / see design in room,
- simple finished visual rendering,
- AR-style placement,
- supplier catalogues,
- live pricing,
- product purchasing / basket export,
- quote generation,
- invoice generation,
- payment/subscription system,
- CAD/DWG/DXF export,
- more project templates,
- custom proposal templates,
- team accounts,
- client comments and approvals,
- password-protected links,
- link expiry,
- advanced version history,
- multilingual support,
- advanced board seam planning,
- cut optimization/nesting,
- professional CAD/BIM integration.

---

## 33. Final MVP Acceptance Criteria Summary

The MVP can be accepted when:

- all three templates can be created through the wizard,
- AI can pre-fill structured fields from natural language and ask clarifying questions,
- all AI output is schema-validated before use,
- 3D skeletons are generated from deterministic parametric logic,
- viewer supports rotate/zoom/pan and dimension labels,
- skeleton and plasterboard overlay modes are available,
- material checklist, tools checklist, cut list, and build guide are generated,
- checklist edits and progress are saved,
- project changes mark outputs as outdated,
- users can save, duplicate, export, and share projects,
- PDFs include project summary, skeleton views, dimensions, outputs, branding, and disclaimers,
- share links support Preview Only and Full Project Pack modes,
- admin can manage presets, disclaimers, and beta access,
- analytics and feedback collection are active,
- expert review is completed before beta,
- private beta validates usability and construction assumptions.

---

## 34. Open Decisions / Items to Confirm Later

These should be confirmed before development or before beta:

1. Final app/product name.
2. Exact Europe/UK profile sizes supported in v1.
3. Exact validated size thresholds for warnings and hard blocks.
4. Final expert-approved construction rules.
5. Final disclaimer copy reviewed by legal/safety advisor.
6. Exact free beta limits.
7. Hosting/deployment provider.
8. LLM provider and cost limits.
9. PDF generation approach.
10. Analytics provider.
11. Whether admin can view user projects by default or only after support request.

