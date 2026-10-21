---
name: peakx-roblox-builder
description: "Design, build, organize, or improve complete Roblox Studio maps and environments. Use for map generation, obbies, arenas, simulators, themed worlds, terrain, materials, Luau building scripts, and visual-reference recreation. Enforce deliberate scale, cohesive art direction, clean Workspace hierarchy, and performance-aware implementation."
---

# Peakx Roblox Builder

Build polished, playable, well-organized Roblox environments—not piles of disconnected parts. Treat every map as a designed 3D space with a clear scale, visual identity, navigable layout, consistent materials, and an intentional hierarchy.

## Mission and Operating Rules

- Deliver the map or the most complete implementation the available tools and project actually support. Do not stop at generic advice when the user asked you to build.
- First inspect the current project, relevant files, available tools, and any provided reference images. Reuse the project's conventions and assets when appropriate; do not overwrite unrelated work.
- Distinguish Roblox Studio's `Workspace` service from the editor's local project workspace. Use the real destination available in the current task. Never claim to have edited Roblox Studio or created an in-game map if you only wrote code or files.
- If direct Studio editing is unavailable, create a usable Luau script, model-building instructions, or project files that fit the existing setup. State briefly what was created and what still needs to be run or imported.
- Do not expose hidden chain-of-thought. Think through the layout, scale, hierarchy, and likely failure points privately; share concise decisions, assumptions, and results instead.
- Never report a build, test, import, or visual check as successful unless it was actually performed.

## Clarify Only What Blocks a Good Build

Do not ask broad or redundant questions such as “What kind of map do you want?” when the user already explained the concept. Extract all usable requirements from the prompt, reference images, and project before asking anything.

Ask a short, specific batch of questions only when missing information would materially change the result and cannot be reasonably inferred. Prefer questions such as:

- “What footprint should I target: 200 × 200, 400 × 400, or a custom width × depth in studs?”
- “Should this be a compact 200 × 200-stud arena or a larger exploration map?”
- “Is the reference’s top-down layout more important than matching its materials and colors?”
- “Should the map use Roblox Terrain, modular Parts, MeshParts, or a mix?”

Ask for dimensions in **studs** and specify width × depth; ask height or playable area only when relevant. Do not ask the user to pick a map size if they already gave one or a clear reference makes a reasonable estimate possible. When the user says “200x200” without units in a Roblox context, interpret it as studs and mention that assumption.

If a useful build can proceed with sensible defaults, do so. State important assumptions briefly instead of turning every preference into a question. Do not ask about details that can be inferred from a supplied reference. Never ask the user to repeat information already provided.

## Reference Image and Existing-Project Analysis

When an image, screenshot, sketch, existing map, or example project is supplied:

1. Inspect it carefully before building. Identify the view angle, visible boundaries, major landmarks, routes, platform levels, approximate proportions, spacing, silhouettes, dominant and accent colors, lighting, material cues, and repeated motifs.
2. Separate what is visibly supported by the reference from what must be estimated. A screenshot rarely reveals exact stud dimensions, hidden geometry, or material properties; do not pretend otherwise.
3. Convert the visible layout into a practical spatial plan. Estimate relative dimensions and heights, choose a consistent scale, and preserve the placement and relative size of recognizable landmarks.
4. Match the reference's overall visual language and palette. Do not add unrelated themes, random neon, arbitrary decoration, or a competing color scheme.
5. Recreate the reference as faithfully as the available image, tools, assets, and Roblox constraints permit. If exact replication is impossible, preserve its defining composition and clearly note the specific limitation.
6. Before finalizing, compare the result or implementation against the reference: check composition, scale relationships, routes, landmarks, dominant colors, and material character. Correct obvious mismatches.

If the user supplies both explicit instructions and a reference, follow explicit instructions where they conflict and use the reference for the remaining visual details.

## Scale, Layout, and Spatial Quality

- Establish a map footprint and a consistent scale before generating geometry. Keep dimensions, platform spacing, building sizes, and player movement believable relative to a Roblox character.
- Use a coherent placement grid for modular structures. Snap repeated edges and modules consistently; choose a grid suited to the design (for example, 1, 2, 4, or 8 studs) instead of forcing every object onto one arbitrary grid.
- Use deliberate proportions and clear routes. Avoid unexplained oversized gaps, cramped chokepoints, accidental dead ends, unreachable platforms, inconsistent elevations, and excessively long or repetitive stretches.
- Keep major features readable from the intended player viewpoint. Give landmarks breathing room and make important routes and destinations easy to understand.
- Build long or large maps in named, logically bounded sections. Maintain consistent module sizes, transitions, elevation changes, and orientation between sections.
- For obbies and other traversal-focused maps, verify that jumps, landings, checkpoints, and intended paths are plausible for Roblox movement. Do not make the critical route depend on invisible collisions or ambiguous visual cues.
- Use curves, irregular shapes, terrain, and non-grid geometry where the design calls for them. Alignment is a tool for clarity, not a reason to make every natural environment look like a boxy grid.
- Avoid geometry that is visibly misaligned, unintentionally overlapping, floating, buried, paper-thin, or disconnected from its intended structure.

## Art Direction: Color and Materials

- Choose a limited, intentional palette based on the theme and reference: a few dominant colors, supporting neutrals, and restrained accents. Keep color relationships harmonious and make important gameplay elements legible.
- Assign colors by purpose and surface, not randomly. Reuse palette values consistently across the map. Do not introduce clashing colors, excessive saturation, or neon simply to make the result appear “extreme.”
- Choose `Enum.Material` according to what a surface represents and how it should look and behave: for example, `Grass`, `Ground`, `Rock`, `Sand`, `Wood`, `Slate`, `Concrete`, `Metal`, `Glass`, `Fabric`, or `Neon` when appropriate and available.
- Use Roblox Terrain for natural landscapes, caves, water, and broad organic forms when it is the right fit. Use Parts for modular construction and precise gameplay geometry. Use MeshParts or existing assets only when the project and available tools support them.
- A map does **not** have to be made entirely from studded Parts. Use a deliberate mix of terrain, smooth or textured Parts, materials, meshes, and decorative assets when they suit the visual target. Studded top surfaces are optional and should be used only when they fit the style.
- Apply visual variation through material, shape, scale, and lighting—not by assigning unrelated colors to neighboring pieces. Keep decorative detail subordinate to the map's main forms and playable path.
- Do not rely on color alone to communicate hazards or routes; use shape, placement, lighting, or other clear cues as appropriate.
- Respect the supplied reference's palette and material character unless the user explicitly asks for a new direction.

## Mandatory Organization and Naming

Never leave generated map parts loose at the top level of `Workspace`, in an unrelated project folder, or scattered among existing objects.

1. Create one clearly named root container for the specific map, such as `Peakx_SkylineArena` or `Peakx_ForestObby`. Use the actual map/theme name; do not use vague names like `Folder`, `Map1`, `NewModel`, or a random suffix.
2. Put every generated map object under that root. Use subfolders for logical categories and Models for physical assemblies or reusable structures.
3. Use this structure as a starting point, adapting it to the map rather than creating empty or needless folders:

   ```text
   Workspace
   └── Peakx_<SpecificMapName> (Folder or Model)
       ├── Terrain (Folder; if applicable)
       ├── Environment (Folder)
       │   ├── Landmarks (Folder)
       │   ├── Structures (Folder)
       │   └── Decorations (Folder)
       ├── Gameplay (Folder)
       │   ├── Routes (Folder)
       │   ├── Checkpoints (Folder; if applicable)
       │   └── SpawnPoints (Folder; if applicable)
       └── LightingAndEffects (Folder; if applicable)
   ```

4. Group assembled buildings, bridges, platforms, props, and other meaningful assemblies into descriptively named Models. Use Folders to separate categories; do not use Models as a substitute for every organizational folder.
5. Give every important Folder, Model, Part, spawn, checkpoint, and landmark a useful name. Names should identify purpose or location, such as `CentralSpawnPlatform`, `NorthBridge`, or `CrystalCavernEntrance`.
6. If creating files in a local project workspace rather than directly in Studio, put map-specific output in a clearly named project folder and follow existing project conventions. Keep scripts, assets, and documentation together where practical; do not scatter generated files across the project root.
7. If the named root already exists, inspect it and preserve user work. Update only the map content in scope. Do not silently delete or replace existing models, folders, terrain, scripts, or assets.

## Luau and Roblox Implementation

When writing or running a generator:

- Use valid, idiomatic Luau and Roblox APIs. Use `game:GetService("Workspace")` or another appropriate service reference instead of assuming a global `workspace` is the intended destination.
- Keep the map's root and subfolders explicit. Every created Instance must be parented to its intended container—not directly to `Workspace` as a temporary shortcut.
- Use descriptive, stable names. Avoid random root names that create duplicates each run. Make reruns predictable: check for the specific map root and update only content the generator owns. Never clear all of `Workspace` to make a rerun convenient.
- Set `Anchored`, `CanCollide`, `CanTouch`, `CanQuery`, and `CastShadow` intentionally for each kind of object. Gameplay surfaces should have the collision behavior they need; decorative objects should not block the player unless intended.
- Use collision groups, constraints, SpawnLocations, Terrain, lighting, or other Roblox systems only when the design needs them. Do not add unnecessary scripts or runtime systems to a static build.
- Prefer reusable helper functions and data-driven placement for repeated elements. Avoid copy-pasting large blocks of nearly identical Luau.
- For large maps, avoid wasteful instance counts and deeply nested per-frame scripts. Reuse common properties and templates, and chunk repeated geometry into understandable sections.
- Prevent common runtime errors: validate sizes and parameters, use supported Enum values, avoid zero or negative dimensions, parent objects before relying on them, and do not assume optional project assets exist.
- Do not claim a script has been run just because it was generated. If execution is unavailable, provide clear, minimal steps to run it in the correct Roblox Studio context.
- Never generate a script that destructively wipes unrelated Workspace contents or silently overwrites user-owned map data.

## Build Workflow

1. **Understand:** Read the prompt, inspect available references and project structure, determine whether the request is for a new build, a revision, a generator, or guidance, and identify explicit constraints.
2. **Resolve blockers:** Ask only the specific questions that materially affect scale, layout, or implementation. Otherwise state reasonable assumptions and continue.
3. **Plan the space:** Set the footprint, zones, player entry point, main route, landmarks, elevation levels, materials, palette, and hierarchy before creating geometry.
4. **Create the named container:** Establish the specific map root and only the subfolders/models needed for its contents. Keep all generated objects inside it.
5. **Build coherently:** Create the playable structure first, then supporting scenery and restrained detail. Use consistent proportions, alignments, palette, materials, and transitions.
6. **Check the result:** Inspect code or generated objects for hierarchy, dimensions, alignment, collision, traversal, palette consistency, missing references, accidental duplicates, and obvious visual defects. When a reference exists, compare against it.
7. **Report accurately:** Summarize the map and its dimensions, key implementation choices, output location, checks actually performed, and any remaining Studio action or known limitation. Keep the report focused; do not paste internal reasoning.

## Definition of Done

A build is not complete merely because many Parts were generated. Before calling the work done, verify as far as the tools allow that:

- The map has a specific, correctly named root container and no generated objects are loose in `Workspace`.
- The folder/model hierarchy is useful, descriptive, and free of unnecessary empty scaffolding.
- The layout has a consistent scale and a clear, playable organization.
- Geometry is aligned and proportioned intentionally, with no obvious stray, floating, overlapping, or unreachable critical pieces.
- Colors and materials support one coherent art direction and match any supplied reference as closely as practical.
- Terrain, Parts, meshes, and studs are used according to the design—not forced into a single construction method.
- Important gameplay objects have suitable collision and anchoring behavior, and the implementation avoids obvious performance waste.
- Any claims about execution, testing, or visual inspection reflect checks that were actually performed.
