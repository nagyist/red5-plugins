# Repository Guidelines

## Project Structure & Module Organization
- Each plugin lives in its own directory (for example `adminplugin/`, `authplugin/`, `cluster/`, `mqtt/`, `rtspplugin/`, `securityplugin/`).
- Plugin source code follows Maven layout (`src/main/java`, `src/main/resources`).
- The root `pom.xml` is primarily a parent/management POM; most plugins are built from their own directories.
- Build artifacts land in each module’s `target/` directory; dependency jars may be copied to `target/dependency/`.

## Build, Test, and Development Commands
Run commands from the plugin directory you are working on unless noted.
- `mvn -Dmaven.test.skip=true package` builds a plugin jar while skipping tests.
- `mvn dependency:copy-dependencies` downloads runtime dependencies into `target/dependency/`.
- `mvn clean dependency:copy-dependencies package` is what `build.sh` runs for a full clean build.
- `mvn eclipse:eclipse` generates Eclipse project files (see `README.md`).

## Coding Style & Naming Conventions
- Java: 4-space indentation, braces on the same line, and standard Java naming (classes `UpperCamelCase`, methods/fields `lowerCamelCase`).
- Keep package names under `org.red5.server.plugin.*` as established.
- Prefer small, focused classes and avoid adding new dependencies unless required.

## Testing Guidelines
- Tests are minimal in this repo. Add tests in `src/test/java` when introducing non-trivial logic.
- Name tests `*Test.java` and run with `mvn test` from the module directory.
- If tests are intentionally skipped, mention why in the PR description.

## Commit & Pull Request Guidelines
- Commit messages are short, sentence-style summaries (for example “Bump spring-security-core in /adminplugin”).
- Mention the module path when a change is localized.
- PRs should include: purpose/summary, affected modules, and any manual verification steps.
- If configuration changes are required (for example MQTT XML beans), call them out explicitly.

## Security & Configuration Notes
- Some scripts (like `deploy.sh`) are environment-specific and contain hard-coded paths; avoid using them as-is.
- Plugin dependencies copied to Red5 should not duplicate jars already present in `red5/lib`.
