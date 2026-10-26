# Task-specific agent guidance

Read only the sections selected by [AGENTS.md](AGENTS.md). These are the
full organization rules, moved out of the always-read entry point.

## History

When given a previous agent's local JSONL conversation, use the shared
[conversation reader](https://github.com/foss-earth/docs/blob/main/docs/agent-conversations.md):
`node ~/gh/foss-earth/docs/scripts/read-agent-conversation.mjs <file> --prompts --all`,
then search or read a bounded tail. It supports Claude and Codex logs without
dumping snapshots or reasoning. Verify historical claims against today's code.

## Contributions

- You cannot have AI as a co-author, or your contributions will be rejected.
  Never add AI author, committer or co-author attribution to commits (see
  [CONTRIBUTING.md](CONTRIBUTING.md)).

- Versions follow [CONTRIBUTING.md](CONTRIBUTING.md): `YY.MM.DD#N` for
  commits and `YY.MM.DD LTS` for long-term support releases.

## Workspace

- Keep scratch files, logs and screenshots in the repository's gitignored
  `build/` directory, not in system temp folders.

- Don't discard uncommitted work you didn't make.

- Don't send personal data, accounts or credentials to another service without
  consent.

## Checks

- **Light testing on the laptop:** the maintainer works on a fanless Apple M5
  laptop. Keep automated testing as short as the decision allows: one quick
  configuration first, then stop once the result is clear. Don't start browser
  or benchmark sessions that run longer than a few minutes; defer them. If a
  long run is really necessary, write a handoff doc for a cloud agent instead,
  with exact commands, expected duration and what to compare. On a VM without a
  GPU, compare only paired differences, not absolute frame times. Say what the
  maintainer can test by hand. Prefer the work that ships the most measured
  improvement per hour.

## Maps and prepared data

- **Google Maps key:** before asking for a key, check `GOOGLE_3D_TILES_KEY`
  in the environment and ignored `.env.local` files in `~/gh/foss-earth/app`,
  `~/gh/UMN-VR/tour`, and `~/gh/0sfs/fly`. `FOSS_EARTH_GOOGLE_KEY` remains a
  legacy fallback. Either environment name beats files; the new name beats the
  legacy name across files. Read only these named variables; never
  print the key in agent logs or commit the file. The user-facing `npm run dev`
  startup intentionally includes `gkey` in its local/network URLs and QR; agents
  use `npm run llm-dev` to omit it. Build-time photo height preparation uses
  Google 3D geometry first; another source is a recorded fallback only.

- **Prefer build-time work over runtime work.** Prepare stable placement heights
  explicitly, record their source, and consume fixed scene values at runtime.
  Never move photos as map LOD changes. Populate and validate every consuming
  scene before removing a legacy placement path; do not leave orbs unplaced.

## Publishing

- Don't deploy, rewrite published history or change repository settings
  unless asked.

## UI

- **Explanation on demand:** use a compact **?** button by default for
  supplementary information, diagnostics and rationale, rather than a wordy
  Details/More info action. Keep it last and available on collapsed components.
  Keep only essential terse state, errors/fallbacks,
  pending/apply feedback and decision-critical instructions visible by default.
  Do not hide information needed to understand the current state or avoid mistakes.

- **Promotional artwork credits:** put provider/model attribution, creator names,
  licence links, provenance and modification notices behind the card's compact
  **?**, at the bottom right. Preserve the complete credits and working links
  inside accessible help. Apply this when adding artwork without waiting for a
  separate request; handoff documents must follow the same rule instead of
  proposing permanent credit paragraphs on the card. Do not invent third-party
  model credits for artwork built in this project's own code; credit external
  content shown within it separately.

- **Readable control phrases:** choose label/control order by grammatical
  sense, usually `Implementation [TS / WASM] ?`. Prefix/suffix text is allowed;
  do not impose a universal slider-first or label-first order. Keep help last.

- **Paragraph grouping:** each logical component in a paragraph grid has its
  own compact rounded rectangle by default, including collapsed component
  overrides. Keep a choice's segments together inside one track within its group.
  Show what a part holds by nesting its parts' rounded rectangles inside its
  own, as matryoshka dolls hold each other, never by indentation
  ([rule](https://github.com/foss-earth/docs/blob/main/docs/ui-layout.md#nested-rectangles-show-what-holds-what)).
  An item's thumbnail, name and actions share one visible enclosure; a paragraph
  grid alone is not a boundary. Reuse its existing gallery card for its actions
  instead of repeating its identity in another summary.
  Expanded component/group titles are the first naturally sized item in the
  same wrapping paragraph grid as their controls, not a separate header row.
  Full section headings are the exception and can occupy their own row.
  Paragraph grids with expandable items show expanded items first, then
  minimized items, using an order override that preserves relative order
  within each group and retains focus/control state.

- **Card actions:** when an item card has one primary action, make the whole
  card its native button/link target, including its image, title, status,
  padding and compact action label. A selected/current item stays actionable:
  open its settings/editor when available. Selection alone never disables it.
  Keep the label inside that same control; never nest interactive controls.
  Preserve separate controls for genuinely distinct secondary actions.

- **Compact controls:** arrange content as compactly as practical, using natural
  widths and wrapping paragraph grids where useful. Discrete choices use one
  rounded segmented slider with short text buttons (digits for counts: 1
  worker), selected by fill/outline; no visible radio circles. Use **Global /
  Auto / Manual**. The **?** button is last; source-link icons belong inline at
  the end of its tooltip text, never in another row button. Prefer existing
  recognizable icons over verbose action text, with accessible names. Reuse the
  shared UI factory and follow the full [control design
  spec](https://github.com/foss-earth/docs/blob/main/docs/ui-layout.md#compact-segmented-choices).

## Browser testing

- **Screenshots for UI changes:** after a visible UI change, look at it in
  screenshots before saying it works, and give the person the new and changed
  images, or `build/shots/index.html`, to review. Take them with
  `node ~/gh/foss-earth/browser-testing/scripts/shots.mjs`: put every shot in
  one list in `build/` and run it once against a dev server for that test session,
  stopping any server you started before returning unless the user asked otherwise;
  crop each shot to what changed with `selector`, wait for conditions rather
  than fixed times, and hide live parts such as the frame rate and the map.
  Open only the shots it reports `new` or `changed`, and read values with a
  `print` step rather than from an image. A changed shot's old image moves to
  `build/shots/archive/<UTC time>/`. The FOSS Earth app is ready for input
  once `.foss-earth-overlay-root` exists; its frame rate shows sooner. See
  [docs/screenshots.md](https://github.com/foss-earth/browser-testing/blob/main/docs/screenshots.md).

- **Stranded Chrome clones:** a run of the installed Google Chrome that is
  killed instead of closed leaves a copy of the app, about 2 GB by `du`, under
  `/private/var/folders`. After a Chrome run you stopped, that timed out or that
  crashed, and whenever disk space comes up, run
  `~/gh/foss-earth/browser-testing/scripts/chrome-clones.sh --clean`. It keeps
  the clones of running browsers.
  [chrome-code-sign-clones.md](https://github.com/foss-earth/docs/blob/main/docs/validation/chrome-code-sign-clones.md)
  says why they appear.
