CLC AI
CLC is a CLI that installs reusable Copilot capabilities around OpenSpec 1.16.0. It requires Node.js 22.12 or newer. This repository contains the 6.0 migration implementation; release remains gated by real rollout and quality evidence.

Start
Install the CLI from your organization's configured npm registry, then run:

clc-ai list
clc-ai install dev-workflow
clc-ai doctor
Invoke clc-requirement-analysis to prepare requirements, design and tasks together, then clc-development to implement the approved plan. Use clc-development-feedback for remediation and clc-review for independent review. Installed domain workflow skills can also be invoked directly or selected from matching requests. Skills use OpenSpec internally and delegate to clc.workflow when the host supports it; otherwise the current agent follows the skill. Native /opsx-* entry points remain available. Review scope, requirements and tasks once, then let the lead implement, check and remediate. A separate agent invocation or human reviews the current revision. Explicitly archive verified work with clc-ai archive. Publication is a separate authorized action.

Spec-driven development with OpenSpec
OpenSpec owns proposal, specifications, design, task progression and archive. CLC adds entry skills, domain guidance, reviewed-plan fingerprints, acceptance evidence, independent review and guarded verification around the pinned OpenSpec integration. Upstream generated skills and prompts remain unchanged.

Start here	Use it for
What CLC adds to OpenSpec	Present the OpenSpec foundation, CLC additions and shared lifecycle.
Development walkthrough	Install, analyze requirements, approve a plan, develop, review and remediate, with copyable requests and artifacts to show.
Development + frontend walkthrough	Add component mapping, UI behavior, accessibility, localization and visual verification to the same change.
Frontend-only entry	Use clc-frontend with core planning and review when dev-workflow is absent.
For the combined workflow, also run clc-ai install frontend-workflow. In chat, begin with Use clc-requirement-analysis to plan <change-id> from these requirements: .... Review the complete plan, then request clc-development; request clc-review for independent review of the current result. Use clc-frontend for bounded UI work in the same change. Skill names are assistant entry points; clc-ai commands run in the terminal.

Verification and migration
clc-ai verify <change-id> --inspect
clc-ai verify <change-id> --json
clc-ai migrate openspec --dry-run
clc-ai migrate openspec --apply
clc-ai migrate openspec --rollback <migration-id>
Configure actual build/lint/test commands in .github/clc-ai/quality.json. Add clc.json and current acceptance/review evidence to the change. Missing tools, skipped required checks, scope violations and stale reviews cannot pass. Installation stages changes and preserves modified consumer files. Migration preserves legacy evidence and resets imported completion claims.

See the workflow and evidence contract, bundle catalog, architecture decision, and release verification status.

Development
npm ci
npm run validate:ci
npm run typecheck
npm test
npm run test:installer
npm run validate:bundles
npm run validate:openspec
npm run check:upstream
npm run build
npm run check:package
npm run security
npm run validate:ci checks workflow commands and npm-script chains for undefined scripts, missing Node entry files and empty test globs. It also runs before local builds, in both CI jobs and in mandatory release verification. Diagnostics identify the workflow, job, step and script chain; malformed YAML includes line and column. The validator reads files without executing commands or expanding variables. Dynamic references, paths outside the repository and unsupported Node/npm options are reported as not statically checked and still require CI execution. Regression fixtures run with npm run test:installer.

npm run evals:release requires actual matched old/new runs plus platform/host migration and rollback evidence; it fails when evidence is absent. Immutable earlier bundle archives remain available for rollback. OpenSpec stays external to the CommonJS build and is pinned in both publishable package layouts.
