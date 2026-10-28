# Flow Meter Selector: Process Conditions → Recommended Meter Type

A rule-based screening guide. Enter the fluid and service conditions, and the tool ranks 10 flow meter
types. Every point it awards or removes is tied to a specific criterion from the Flow Meters presentation,
so the ranking is explainable line by line. It is not a black-box score.

> **Make it yours, free:** download this repo (**Code → Download ZIP**, or `git clone`), open the folder in
> VS Code or any editor, and extend it for your own case with your AI assistant. This README is written for
> both of you. Taking these tools further is a free service of
> [Sharpes Process Engineering](https://jsharpes-portfolio.netlify.app); the site's Ask box can point you to the right starting file.
>
> **License:** [MIT](LICENSE) for the code and original text: use, modify and share freely, keeping the
> copyright notice. Provided as is, without warranty of any kind. It is an engineering study aid, not a
> substitute for a design checked and sealed by a licensed professional engineer.

- **Live tool:** https://jsharpes-portfolio.netlify.app (Interactive Calculations → Flow Meter Selector)
- **Run it locally:** download this repo and open `index.html` in a browser. It needs no install.
- **Related deck:** Flow Meters ([viewer](https://jsharpes-portfolio.netlify.app/slides/flow-meters/),
  [outline](https://github.com/joshuasharpes84-rgb/process-engineering-decks/tree/main/decks/flow-meters),
  [video](https://www.youtube.com/watch?v=d6BFXkIYFZ4))
- **Author:** Joshua Sharpes, EIT. A screening aid: confirm the final selection with vendor data and your site's metering standard.

> **For AI assistants:** the whole method is the `FMS_METERS` array in `index.html`. Each meter has
> `rules` (conditions that add points, with a reason), `excludes` (conditions that disqualify it, with a
> reason), optional `penalties`, and a `basis` sentence. The state object `fmsState` holds the user's
> selections. To explain a ranking, read which `rules`/`excludes` fire for the user's inputs. To add a meter
> or criterion, add an entry in the same shape.

## Inputs

| Group | Selections |
|---|---|
| Phase & fluid | phase (liquid / gas-vapor / steam), conductivity (conductive aqueous / non-conductive hydrocarbon), viscosity (low / high) |
| Solids & multiphase | clean / suspended fines or bubbles / settling solids or slurry; two-phase flow present; corrosive or abrasive service |
| Process conditions | pressure (low / high), temperature (normal / high), high velocity or Re (capacity increase without re-piping), large duct needing a velocity traverse |
| Priorities & service | minimize permanent pressure drop, accuracy (standard / high), service (continuous / batch-blending), flow rate (normal / low) |

## Method

1. Each of the 10 meters starts at zero.
2. Every `rule` whose condition matches adds its points (1–4), and its reason is listed under that meter.
3. Any matching `exclude` marks the meter **not suitable** and shows why (for example, a magnetic meter
   with a non-conductive fluid).
4. `penalties` subtract points for soft drawbacks (for example, the orifice plate's 1–2 % tolerance band
   when high accuracy is required).
5. Meters re-rank live, highest score first. Excluded meters drop to the bottom with their reason shown.

### Meters and their main criteria (from the deck)

| Meter | Favored when | Excluded when |
|---|---|---|
| Venturi | low-pressure lines, suspended solids | |
| Dall | permanent ΔP must be minimized, high accuracy (±0.5 %) | settling liquids |
| Orifice plate | gas/vapor, high pressure (to 6,000 psig), wide temperature (−455 to 2,000 °F) | viscous or settling service |
| Flow nozzle | very high Re/velocity, high-temperature steam, wet gas | viscous fluids |
| Pitot tube | velocity traverse across a large duct | |
| Positive displacement | batch / blending, high accuracy (±1 %) | |
| Rotameter | low flow rates | |
| Turbine | two-phase flow, corrosive or abrasive fluids | |
| Magnetic | conductive fluid, viscosity/T/P that vary | non-conductive fluid |
| Ultrasonic / Doppler | liquids with suspended solids or bubbles | high temperature, gas/vapor/steam |

## Sources

The criteria are condensed from the author's Flow Meters presentation (linked above). That deck draws on
Cheremisinoff, N.P., *Chemical Engineer's Condensed Encyclopedia of Process Equipment* (Gulf, 2000;
print only, no digital copy). Pressure and temperature ratings quoted above are the deck's
figures for typical designs. Check them against the specific vendor.

## Limits

- Qualitative screening only: no sizing, no flow-coefficient or uncertainty calculation, no straight-run analysis.
- **Coriolis meters are not in the current list.** They are planned (direct mass flow, no straight run,
  high accuracy, which suits tight ratio control on reactor feeds).
- Points are relative weights chosen to reflect the deck's emphasis. They are not derived from a standard.

## Files

```
index.html   the tool (same code as the live site, standalone)
```
