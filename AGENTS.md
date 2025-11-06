# Repository Guidelines

## Project Structure & Module Organization
- `project.godot` is the entry point; open it in Godot 4.3+ to inspect scenes and scripts.
- `scene/` stores `.tscn` definitions for maps, prefabs, and UI overlays used in the demo.
- `script/` holds GDScript logic, with `script/ai/` for LLM and memory systems and `script/ui/` for menus. `.gd.uid` files are editor metadata—commit them with their companion scripts.
- `asset/` bundles textures, icons, and promo art. Create focused subfolders (e.g., `asset/audio/`) for new resource families.

## Build, Test, and Development Commands
- `godot4 --editor project.godot` opens the editor with the project preloaded.
- `godot4 --path .` starts the configured main scene for quick playtesting.
- `godot4 --headless --path . --run scene/ChatHistory.tscn` executes dialogue flows without rendering; this is helpful for automation.
- `godot4 --path . --export-release <preset> build/<preset>/Microverse` generates builds using the export preset selected in the editor.

## Coding Style & Naming Conventions
- Follow Godot defaults: tabs for indentation, `snake_case` for identifiers, `UPPER_SNAKE_CASE` constants, and PascalCase for `class_name` types.
- Keep scripts and their primary nodes aligned (e.g., `RoomManager.tscn` ↔ `RoomManager.gd`).
- Prefer Godot signals and `get_tree()` utilities over ad-hoc globals; reuse existing managers.
- Run the built-in GDScript formatter (`Ctrl+Alt+L`) before committing sizable edits.

## Testing Guidelines
- Automated tests are not yet in place; validate features by running relevant scenes in the editor or via `--headless` mode.
- Clear `user://` saves between sessions to avoid state leakage, especially when verifying persistence or memory features.
- Document reproduction and verification steps in PR descriptions to compensate for the lack of CI coverage.

## Commit & Pull Request Guidelines
- Write concise, descriptive commits (e.g., `feat: add siliconflow provider`) and keep resource/script updates together.
- Reference issues in commit bodies when applicable; keep subjects under 60 characters.
- Pull requests should include a problem summary, solution outline, manual test notes, and screenshots or GIFs for UI or scene changes.
- Request review from maintainers tied to the impacted subsystem (`ai`, `ui`, or `scene`) to preserve coherence.

## Security & Configuration Tips
- Never commit API keys or custom endpoints; configure them through Settings > API or local environment overrides.
- Redact sensitive dialogue logs when sharing debugging assets or crash reports.
- When adding a provider, extend `APIConfig.gd` and surface toggles in `SettingsManager.gd` so QA can switch integrations quickly.
