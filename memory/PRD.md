# PotionRH
Original request: pull https://github.com/Dostarki/potionrh and just run it. Later: remove start questions; then convert the game into an isometric 3D-block (Minecraft + Clash of Clans + Stardew feel) web game keeping original colors/character/sky; big map, mouse zoom; island enlarged 3x.

## Architecture
- `/` -> React iframe -> `frontend/public/game.html` (single file, Three.js from `/assets/three.module.min.js`, r160).
- `/admin` admin panel, `/api/*` FastAPI + MongoDB (unused by the new game view).
- game.html: instanced voxel world on a floating sky island (local coords X -36..132, Z 0..112), orthographic isometric camera, wheel/pinch zoom to cursor, drag/WASD pan, +/-/TÜM buttons. Static shadows (rendered once).

## Implemented (2026-06)
- Repo pulled and running; start gate removed.
- Old side-scroller fully replaced by isometric voxel island: roads, 3 lakes, dock, 3 farms, market stalls, potion shop, cottages, camp, pink hills, portal (COMING SOON), stone wall + dark forest, idle voxel characters (Potion Kid, Wick, Tallow, Fenna, Moss, Reed, Ember), hovering dragon, clouds, original sky bands.
- Characters are idle on purpose (user: cards will later give them jobs). No quests/gate/allowlist UI in game view.

- Potion Works (ambient, non-interactive sim around local 60..99 x 55..79): giant glass potion tank with rising/draining liquid + bubbles, mine shaft with 5 miners carrying glass backpacks, 3 pumpjacks + 1 drill tower pumping through hoses into the tank, farmer SAGE (tank -> waters farm2 crops which grow -> harvest -> sells at MARKET stall, +25 gold), potion veins in island underside, HUD potion/gold counters + tank bar, potion button focuses the site. Game opens focused on this site.
- Note: bash writes to /app are blocked by the harness; edit files with search_replace/create_file only.

- Realism pass: Elixir-Storage style tank (glass sphere, magenta liquid, gold straps, dark pillars), glass hoses with scrolling liquid texture, elixir collectors with valve wheels, pumpjacks with crank/pitman, lattice drill derrick, miners climb ladders (down west wall, up north wall), hand drills, glass backpack empty going down / full coming up, spacing rule between miners, farmer hands crate to MARKET and receives coins.
- 3 mines (MINES const) with random trip per miner (8 miners); ROBINHOOD castle at local 44..58 x 55..69 with label + hand-drawn feather badge (not the official logo file).

- Mines: 1 at the tank (4 miners carry to tank) + 7 scattered over the island (deterministic placement loop after RESERVED; each has 2 local miners pouring into a local collector with a pipe into the ground). ROBINHOOD text is now a waving flag (animated plane) on the keep's pole. All in-game UI text is English.

## Backlog
- P1: Cards system: buy a card -> character performs a job (user said "not now").
- P2: Character movement, building interaction, day/night.
