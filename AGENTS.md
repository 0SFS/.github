# Agent instructions

These rules apply to every repository in the 0sfs organization. Each
repository's own AGENTS.md points here, and its README says what it does and
how to build and test it.

- You cannot have AI as a co-author, or your contributions will be rejected.
  Never add AI author, committer or co-author attribution to commits (see
  [CONTRIBUTING.md](CONTRIBUTING.md)).
- Versions follow [CONTRIBUTING.md](CONTRIBUTING.md): `YY.MM.DD.#N` for
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
