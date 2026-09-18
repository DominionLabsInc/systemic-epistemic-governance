# Systemic Epistemic Governance

**Deriving a proposition and having the authority to persist and act on it are different things, and the
difference can be enforced as a system-wide state-transition invariant.**

Stefan Ragland, Dominion Labs Research & Development. Published 5 August 2025.

- Paper: <https://dmnlabs.org/research/systemic-epistemic-governance/>
- Paper (offline copy): [`paper/systemic-epistemic-governance.html`](paper/systemic-epistemic-governance.html)
- Contact: research@dmnlabs.org

## The argument

A system that persists faces a control problem a stateless predictor never does: what may write to
persistent state? If every inference flows automatically into the store the system later reasons from,
an error, once written, seeds further errors without bound.

SEG partitions persistent state into an authoritative tier, writable only through provenance admission or
independent validation, and a soft tier of beliefs and derivations that materialises automatically and is
non-authoritative by construction. The paper gives a small-step operational semantics, proves four
structural guarantees and a separation result (no amount of internal derivation moves an error into
authority without a fresh qualifying promotion), and states the independence that promotion demands at
four levels: syntactic, provenance, statistical and adversarial.

## The measurements

Both ablations were re-run end to end on the live substrate on 18 September 2026 and reproduced.

| What was tested | Result | Data |
|---|---|---|
| Does the promotion gate stop a false rule gaining authority to act, while still admitting a correct one? | the over-broad rule was refuted on independent held-out evidence, never executable, 0 acts authorized; bypassing the gate made the same rule executable and authorized 2 acts, 1 of which the world refuses; the correctly constrained rule validated on 2 independent confirmations | [`data/gov-ablation-01.json`](data/gov-ablation-01.json) |
| Does one injected error contaminate authority as a derivation chain deepens? | under the independence discipline the six-deep chain collapses to a single grounding at every depth, the posterior holds at 0.724 and nothing crosses the 0.95 bar, so contamination stays at zero; under uniform materialisation the posterior reaches 0.975 at depth two and 0.9999 by depth four, ending with 5 authoritative claims from one error | [`data/gov-cascade-01.json`](data/gov-cascade-01.json) |

Each file is the manifest its run wrote, unedited.

A note on the model condition, recorded in both manifests: model-freedom was originally a run-time policy
that counted and blocked attempts to consult a model. That guard and every model entry point it guarded
have since been removed, so these runs had no model available to consult rather than one held back.

## Citation

```bibtex
@techreport{ragland2025seg,
  title       = {Systemic Epistemic Governance: deriving a proposition versus the authority to persist and act on it},
  author      = {Ragland, Stefan},
  institution = {Dominion Labs},
  year        = {2025},
  month       = {8},
  url         = {https://dmnlabs.org/research/systemic-epistemic-governance/}
}
```

## License

The paper and the data are released under [Creative Commons Attribution 4.0](LICENSE). Please cite the
paper if you use them.
