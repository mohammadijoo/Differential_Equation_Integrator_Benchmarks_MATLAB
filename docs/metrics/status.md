# `status`

## Meaning

`status` records the outcome of a method/benchmark run.

## Typical values

Common values include:

- `success`
- `failure`
- `not_applicable`
- `method_planned_not_implemented`
- `benchmark_planned_not_runnable`
- `blow_up`
- `non_converged`

## Interpretation

`status` prevents failed, skipped, or non-applicable runs from being interpreted as valid numerical results.

## Recommended use

When comparing methods, filter or group by status before computing summary plots:

```matlab
valid = strcmp({records.status}, 'success');
records_success = records(valid);
```

## Limitations

A successful run is not necessarily accurate or physically meaningful. Always inspect numerical metrics and qualitative plots.
