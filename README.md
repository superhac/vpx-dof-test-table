# DOF Test

A Visual Pinball X utility table for testing DirectOutput Framework (DOF) toys one event at a time. The flipper buttons step through DOF events E901 to E990. Only the selected event is on, and the backglass shows its number.

## Contents

| File | Purpose |
|---|---|
| `DOF_test.vpx` | The table (script embedded), based on the VPX example table |
| `DOF_test.directb2s` | Backglass: shows the current E number on a 3-digit LED display |

## Installation

1. Download the zip from the [Releases](../../releases) page.
2. Extract it into your tables folder. Keep the `.directb2s` next to the `.vpx`, with the same name.

## Requirements

- DOF installed and configured: the DOF plugin on VPX standalone, or DirectOutput with the B2S Server on Windows.
- `controller.vbs` in the VPX `scripts` folder.
- B2S Server (Windows) or the VPX **B2S plugin** enabled, to show the E number on the backglass.

## How it works

The table sets `cGameName = "pinupmenu"`, so DOF loads the **pinupmenu** table config from your DOF Config Tool export. The E events you test are the ones mapped in that config.

| Input | Action |
|---|---|
| Right flipper | Next event (E900 → E901 → … → E990 → E900) |
| Left flipper | Previous event (wraps around the same way) |

- Each press turns the previous event off (`DOF n, DOFOff`) and the new one on (`DOF n, DOFOn`). The event stays on until you step again.
- **E900** is the start position, with all test events off.
- The current number is shown on the backglass LED display, and in desktop mode on the playfield text box.
- The flippers still flip and fire the normal flipper DOF events. The rest of the table plays like the VPX example table.

To test a different range, edit `FlipperDOFMinEvent` and `FlipperDOFMaxEvent` at the top of the script.

## Troubleshooting

- **Nothing fires:** make sure your DOF config has a **pinupmenu** entry with outputs mapped to E901–E990. Check `DirectOutput.log` in the table folder.
- **No number on the backglass:** make sure the B2S Server is installed, or the B2S plugin is enabled, and that the `.directb2s` has the same name as the `.vpx`.

## Releases

Pushing a tag starting with `v` (for example `v1.0.0`) runs the release workflow. It zips every file in the repository into `DOF_test/` and attaches the zip to a GitHub release. You can also start it from the Actions tab and enter a tag.

## Credits

Based on the VPX example table by fuzzel, jimmyfingers, jpsalas, toxie and unclewilly, with contributions from zany, djrobx, ninuzzu, rothbauerw and arngrim (DOF).
