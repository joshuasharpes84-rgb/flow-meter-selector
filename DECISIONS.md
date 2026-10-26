# Engineering Decisions — Plant Resources (Flow Meter Selector)

The calls that shaped the Flow Meter Selector. Sources are in `SOURCES.md`.

*Built by Joshua Sharpes, EIT, with AI assistance (Claude) for drafting and coding. Scope, method
selection and validation criteria are his.*

**Explainable rules, not a black-box score.** Each of the 10 meters gains points only from named
criteria in the *Flow Meters* deck, loses them only through stated drawbacks, and is excluded only
for a stated reason (for example, a magnetic meter with a non-conductive fluid). Every ranking can be
explained line by line from the inputs.

**Screening, not sizing.** The tool recommends a meter type. It does no sizing, flow-coefficient,
uncertainty or straight-run calculation, and tells the user to confirm against vendor data and the
site's metering standard.

**Weights are judgment, stated as such.** Point values reflect the deck's emphasis; they are not
taken from a standard, and the README says so.

**Known gap: Coriolis.** Coriolis meters (direct mass flow, high accuracy, no straight run) are not
in the deck, so they are not in the tool yet. Planned.
