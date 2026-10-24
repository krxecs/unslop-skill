# Unslop

Unslop is a skills-only plugin for ChatGPT and Codex. It gives non-code, user-visible writing a plainer, less AI-sounding style.

## What it can and cannot do

The skill is eligible for implicit selection when the request calls for drafting, rewriting, editing, or explaining in natural language. If the host loads it, its rules apply to all user-visible non-code text produced for that task.

A plugin skill cannot force ChatGPT or Codex to load it for every reply. Implicit invocation is a relevance-based model decision. Use explicit invocation when this style must apply to a particular request:

- In ChatGPT, type `@Unslop` and write the request.
- In Codex, type `$unslop` and write the request.

Unslop does not rewrite code, commands, identifiers, paths, verbatim quotations, or text that the user asks to preserve.

## Install

### ChatGPT and ChatGPT Work

Install the plugin from the Plugins directory when it is available to your account or workspace. Start a new chat after installation. Use `@Unslop` for a guaranteed selection on a request, or make a writing request and allow implicit selection.

Plugins work in Chat and Work on ChatGPT web, desktop, and mobile. Availability still depends on the account and workspace plugin controls.

### Codex desktop app and Codex CLI

Add this repository as a marketplace, then install the `unslop` plugin. In the CLI:

```text
codex plugin marketplace add krxecs/unslop-skill
```

Open the plugin browser, install Unslop, and start a new session. Use `$unslop` when the style must apply.

The Codex IDE extension does not support plugins. The standalone skill layout is separate from the plugin path and has different surface support.

## Test status

| Check | Result | Notes |
| --- | --- | --- |
| Portable manifest JSON | Passed | Parsed and checked for required identity, version, license, and OpenAI metadata. |
| Package paths | Passed | `plugin.json`, `skills/unslop/SKILL.md`, `skills/unslop/agents/openai.yaml`, and the icon paths are present. |
| Marketplace source | Passed by inspection | The marketplace now uses a Git URL to the plugin root. The previous `./` source resolved to `.agents/plugins/`, not the plugin root. |
| Implicit invocation configuration | Passed by inspection | `allow_implicit_invocation: true` permits relevance-based implicit selection. It does not guarantee activation. |
| Explicit invocation | Supported by product docs | Use `@Unslop` in ChatGPT and `$unslop` in Codex. |
| Installed-plugin behavior in ChatGPT or Codex | Not run | This repository cannot drive an authenticated Plugins Directory session from CI or the GitHub connector. Run the manual checks below before public submission. |
| GitHub release | Not created | No GitHub release write capability is available in the connected GitHub integration. The package version is `0.2.0`; create a matching tag and release in GitHub when release access is available. |
| Public Plugins Directory | Not published | Public distribution requires an upload and review through the OpenAI plugin submission portal. |

## Manual acceptance checks

After installing version 0.2.0 in a new ChatGPT or Codex session, run these checks and record the result:

1. Explicit: invoke Unslop and ask for a short project update. Confirm that the generated prose follows the skill.
2. Implicit positive: ask for a rewrite without naming the skill. Confirm whether the host selects Unslop.
3. Negative: ask for a code-only change. Confirm that Unslop does not alter code.
4. Boundary: ask for a verbatim quote. Confirm that quoted text remains unchanged.
5. Follow-up: after an Unslop response, ask for another prose edit. Confirm that the loaded instructions continue to apply to the task.

## Release process

1. Run the manual acceptance checks above in each supported surface you plan to claim.
2. Update `plugin.json` and this README with the results.
3. Create a Git tag and GitHub release that match the manifest version.
4. Zip the complete plugin package and submit it through the OpenAI plugin submission portal for review.
5. Publish only after the package version is approved.

The plugin is licensed under the existing [MIT License](LICENSE).
