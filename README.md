# Blackjack

A synced multiplayer Blackjack table for up to 7 players. Made for **SideQuest / AltspaceVR** worlds, and it also works in **Banter**.

There is no server: players stay in sync through the space's shared state, and the game is plain static files served from <https://blackjack.firer.at>.

To try it, open <https://blackjack.firer.at> in Altspace or Banter.

## Features

- Hit, stand, double down and split
- Chips and bets per player
- Host migration and disconnect handling

## Add it to an Altspace world (snippet)

In a Creator SDK world, add an empty GameObject at the origin, click **Add Component > BS > Snippet** and type `blackjack`. Or paste this into `Assets/WebRoot/index.html`, between the snippet section comments:

```html
<!-- snippet section -->
<bs-snippet name="blackjack" title="Blackjack"
  description="Synced multiplayer Blackjack table with seats for up to 7 players."
  script="https://blackjack.firer.at/snippet.js"
  room=""
  position="0 0 3"
  rotation="0 0 0"
  debug="false">
  <bs-gizmo type="position" attribute="position"/>
  <bs-gizmo type="plane" attribute="position" size="3.6 3.6" rotation="90 0 0"/>
</bs-snippet>
<!-- end snippet section -->
```

- Each placement is its own game. Its sync id is `room`, or the placement's own id when `room` is empty. Give placements the same `room` to share one game.
- `position` and `rotation` are Unity world values. The other settings are listed under [Settings](#settings). An empty setting uses the default.
- The Scene-view gizmo shows the table footprint.
- Unity reads the snippet section as XML: quote every attribute, close every element, and write `&` as `&amp;`.

## Add it with a script tag

This works in an Altspace world's `Assets/WebRoot/index.html` (outside the snippet section) and in a Banter space's HTML:

```html
<script src="https://blackjack.firer.at/blackjack.js" position="0 0 2" rotation="0 180 0" instance="lobby-bj"></script>
```

For more than one table in a space, give each one its own `instance`:

```html
<script src="https://blackjack.firer.at/blackjack.js" instance="table1" position="-4 0 0"></script>
<script src="https://blackjack.firer.at/blackjack.js" instance="table2" position="4 0 0"></script>
```

## Settings

| Setting | Also accepted | Default | Description |
| :--- | :--- | :--- | :--- |
| `instance` |  | `blackjack_game` | Sync id. Tables with the same id share one game. In a snippet, use `room` instead. |
| `position` |  | `0 0 2` | Table position (x y z). |
| `rotation` |  | `0 0 0` | Table rotation in degrees (x y z). |
| `debug` |  | `false` | `true` logs extra detail to the console. |

## How to play

1. Click **JOIN** to take a seat.
2. Place your bet, then play your hand: hit, stand, double down or split.
3. The dealer plays by standard rules once everyone is done.

## Files

- `blackjack.js`: the game.
- `Assets/`: sounds.
- `snippet.js`, `snippet.html`: the Creator SDK snippet and its definition.
- `index.html`: a test page with a floor and the game.

## Credits

- Original Holograms Against Humanity for AltspaceVR: Derogatory, falkrons, schmidtec
- Ported to Banter: Shane
- Improved, fixed and ported from A-Frame: FireRat

The sounds come from the original Holograms Against Humanity project.

## License

GPL-3.0. See [LICENSE](LICENSE).
