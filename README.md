# storymodeplayer

Public demos of [pixterm-engine](https://github.com/Yuncun/pixterm-engine) characters running in the browser.

Each character is a self-contained static bundle: the TypeScript port of pixterm's dimensional-state-graph simulator + a tiny Vue shell + the character's graph + node images + edge clips.

## Live demos

- [flf_elf_girl](https://yuncun.github.io/storymodeplayer/flf_elf_girl/) — elf girl character with 44 poses, 95 edges, 11 animation clips. Click the **Signals** buttons to fire `claude_session.active` / `claude_session.idle` and watch her behavior shift.

## How a demo works

The simulator ticks at 10 Hz, picking outgoing edges from the current pose based on weights, integrators, and signal effects declared in the character's `graph.json`. When an edge is picked it plays the corresponding clip; when no clip exists, the source pose's poster stays up for the simulated clip duration. Signal buttons fire `pending_signals` into the simulator, which the next tick consumes — `on_signal` declarations on integrators shift the weight surface and the character's path follows.

## How to add a character

From the [pixterm-engine](https://github.com/Yuncun/pixterm-engine) repo:

```sh
make build-standalone CHAR=<character_name>
```

Then copy `apps/standalone/dist/<character_name>/` into this repo as `<character_name>/` and push. GitHub Pages serves it at `https://yuncun.github.io/storymodeplayer/<character_name>/`.

## License

Source for the engine and player is in the parent [pixterm-engine](https://github.com/Yuncun/pixterm-engine) repo. Generated assets per character.
