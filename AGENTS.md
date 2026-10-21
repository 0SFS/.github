# Agent instructions

These rules apply to every repository in the 0sfs organization. Each
repository's own AGENTS.md points here, and its README says what it does and
how to build and test it.

When given a previous agent's local JSONL conversation, use the shared
[conversation reader](https://github.com/foss-earth/docs/blob/main/docs/agent-conversations.md):
`node ~/gh/foss-earth/docs/scripts/read-agent-conversation.mjs <file> --prompts --all`,
then search or read a bounded tail. It supports Claude and Codex logs without
dumping snapshots or reasoning. Verify historical claims against today's code.

- You cannot have AI as a co-author, or your contributions will be rejected.
  Never add AI author, committer or co-author attribution to commits (see
  [CONTRIBUTING.md](CONTRIBUTING.md)).
- Versions follow [CONTRIBUTING.md](CONTRIBUTING.md): `YY.MM.DD#N` for
  commits and `YY.MM.DD LTS` for long-term support releases.
- Keep scratch files, logs and screenshots in the repository's gitignored
  `build/` directory, not in system temp folders.
- Don't discard uncommitted work you didn't make.
- **Google Maps key:** before asking for a key, check `FOSS_EARTH_GOOGLE_KEY`
  in the environment and ignored `.env.local` files in `~/gh/foss-earth/app`,
  `~/gh/UMN-VR/tour`, and `~/gh/0sfs/fly`. Read only the named variable; never
  print the key or commit the file. Build-time photo height preparation uses
  Google 3D geometry first; another source is a recorded fallback only.
- **Prefer build-time work over runtime work.** Prepare stable placement heights
  explicitly, record their source, and consume fixed scene values at runtime.
  Never move photos as map LOD changes. Populate and validate every consuming
  scene before removing a legacy placement path; do not leave orbs unplaced.
- Don't deploy, rewrite published history or change repository settings
  unless asked.
- Don't send personal data, accounts or credentials to another service without
  consent.
- **Explanation on demand:** use a compact **?** button by default for
  supplementary information, diagnostics and rationale, rather than a wordy
  Details/More info action. Keep it last and available on collapsed components.
  Keep only essential terse state, errors/fallbacks,
  pending/apply feedback and decision-critical instructions visible by default.
  Do not hide information needed to understand the current state or avoid mistakes.
- **Readable control phrases:** choose label/control order by grammatical
  sense, usually `Implementation [TS / WASM] ?`. Prefix/suffix text is allowed;
  do not impose a universal slider-first or label-first order. Keep help last.
- **Paragraph grouping:** each logical component in a paragraph grid has its
  own compact rounded rectangle by default, including collapsed component
  overrides. Keep a choice's segments together inside one track within its group.
  Expanded component/group titles are the first naturally sized item in the
  same wrapping paragraph grid as their controls, not a separate header row.
  Full section headings are the exception and can occupy their own row.
  Paragraph grids with expandable items show expanded items first, then
  minimized items, using an order override that preserves relative order
  within each group and retains focus/control state.
- **Compact controls:** arrange content as compactly as practical, using natural
  widths and wrapping paragraph grids where useful. Discrete choices use one
  rounded segmented slider with short text buttons (digits for counts: 1
  worker), selected by fill/outline; no visible radio circles. Use **Global /
  Auto / Manual**. The **?** button is last; source-link icons belong inline at
  the end of its tooltip text, never in another row button. Prefer existing
  recognizable icons over verbose action text, with accessible names. Reuse the
  shared UI factory and follow the full [control design
  spec](https://github.com/foss-earth/docs/blob/main/docs/ui-layout.md#compact-segmented-choices).
- **Light testing on the laptop:** the maintainer works on a fanless Apple M5
  laptop. Keep automated testing as short as the decision allows: one quick
  configuration first, then stop once the result is clear. Don't start browser
  or benchmark sessions that run longer than a few minutes; defer them. If a
  long run is really necessary, write a handoff doc for a cloud agent instead,
  with exact commands, expected duration and what to compare. On a VM without a
  GPU, compare only paired differences, not absolute frame times. Say what the
  maintainer can test by hand. Prefer the work that ships the most measured
  improvement per hour.
- **Stranded Chrome clones:** a run of the installed Google Chrome that is
  killed instead of closed leaves a copy of the app, about 2 GB by `du`, under
  `/private/var/folders`. After a Chrome run you stopped, that timed out or that
  crashed, and whenever disk space comes up, run
  `~/gh/foss-earth/browser-testing/scripts/chrome-clones.sh --clean`. It keeps
  the clones of running browsers.
  [chrome-code-sign-clones.md](https://github.com/foss-earth/docs/blob/main/docs/validation/chrome-code-sign-clones.md)
  says why they appear.
