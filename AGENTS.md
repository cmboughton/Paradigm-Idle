# Repository Guidelines

## Project Baseline

- Project: **Paradigm**, located at `D:\Paradigm\Paradigm`; descriptor: `Paradigm.uproject`.
- Locally source-built engine: `D:\Unreal Source Code\UnrealEngine`. `Engine/Build/Build.version` reports **5.8.3**, branch `UE5`. The descriptor's engine GUID resolves to this directory through the Windows registry.
- Runtime module: `Paradigm`, loaded in the `Default` phase. `Source/Paradigm/Paradigm.cpp` registers `FDefaultGameModuleImpl`; `Paradigm.h` includes `CoreMinimal.h`. No project gameplay classes or automated tests exist yet.
- `Paradigm.Build.cs` uses explicit/shared PCHs, with public dependencies `Core`, `CoreUObject`, `Engine`, `InputCore`, and `EnhancedInput`; private dependencies are empty.
- `ParadigmTarget` (Game) and `ParadigmEditorTarget` (Editor) use build settings V7, Unreal5_8 include ordering, and the `Paradigm` module. No dedicated server target exists yet.
- Explicitly enabled plugin: engine-provided `ModelingToolsEditorMode`, editor targets only. No project `Plugins/` directory exists; engine-default plugins may also load.
- Initial inspection: clean Git working tree on `main`, tracking `origin/main`. Recheck status before changes.

## Architecture

Follow Unreal C++ conventions and Unreal Header Tool requirements, including reflection macros and placing `.generated.h` last among header includes. Match existing tab indentation and brace style. Use reflection, garbage collection, and replication correctly; ensure UObject references have appropriate lifetime tracking.

Prefer modular, reusable, maintainable systems and data-driven implementations where appropriate. Design gameplay with multiplayer and server authority in mind. Avoid unnecessary complexity and dependencies.

## Development Workflow

Create an implementation plan before modifying files for substantial features. Wait for approval before implementing major features. Explain architectural decisions and tradeoffs; keep changes small and testable.

Obtain approval before modifying plugins or project configuration, deleting or overwriting existing assets, or committing, pushing, merging, or switching Git branches.

## Validation

Use the locally source-built engine and verify C++ changes through Unreal Build Tool. From the project directory, build the editor with PowerShell:

```powershell
& 'D:\Unreal Source Code\UnrealEngine\Engine\Build\BatchFiles\Build.bat' ParadigmEditor Win64 Development 'D:\Paradigm\Paradigm\Paradigm.uproject' -WaitMutex
```

Report build errors and warnings. Never claim successful compilation without an actual successful build. Identify Blueprint, asset, and editor changes requiring manual verification, including multiplayer behavior where applicable.

## Project Safety

Treat engine source as read-only; never modify it without explicit permission. Do not modify files outside the project directory without explicit permission. Never bypass approval or sandbox restrictions.

Keep generated build files out of Git, including `Binaries/`, `Intermediate/`, `Saved/`, and `DerivedDataCache/`. Keep gameplay source in `Source/Paradigm/`, assets in `Content/`, and project settings in `Config/`.
