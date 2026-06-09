# Gravl Maestro Suite

Run every Gravl workflow:

```bash
maestro --device emulator-5554 test .maestro
```

Run only smoke-tagged workflows:

```bash
maestro --device emulator-5554 test .maestro --include-tags=smoke
```

Run only workflows that create and clean up test data:

```bash
maestro --device emulator-5554 test .maestro --include-tags=stateful
```

Run the reset-account workout completion workflow explicitly:

```bash
maestro --device emulator-5554 test .maestro/reset-account-flows/gravl-workout-completion.yaml
```

## Structure

- `config.yaml`: workspace discovery rules.
- `flows/`: executable Gravl workflows. Every YAML flow added here is included in the full suite.
- `subflows/`: reusable setup and cleanup helpers. These are excluded from workspace discovery.
- `reset-account-flows/`: automated workflows that are excluded from the full suite because their effects cannot be fully reversed.
- `examples/`: excluded proof-of-concept files.

Keep each workflow runnable on its own. Prefer stable IDs over translated text selectors when the app exposes them.

## Coverage

- Logged-in Home smoke checks.
- Home next-workout options visibility.
- Bottom navigation across Home, Feed, Library, and Profile.
- Feed tab switching and grouping options.
- Library sections and exercise search filters.
- Workout preview entry.
- Workout start and cancellation with cleanup.
- Profile overview visibility and scrolling.
- Profile settings visibility and scrolling.
- Read-only health profile, weight unit, distance unit, and exertion-rating settings.
- Gym profile creation and deletion with cleanup.
- Gym equipment bulk-save using a temporary gym profile with cleanup.
- Workout completion, Save Workout validation, and Feed activity deletion in a reset-account workflow.

The suite assumes an existing logged-in testing account. Fresh Google authentication and onboarding are intentionally deferred because they require a disposable account or a reliable account reset path.

## Reset-Account Workflows

`reset-account-flows/gravl-workout-completion.yaml` completes a workout and deletes the generated Feed activity. Gravl restores the weekly completion count after deletion, but it does not restore the previous next-workout schedule. Run this workflow only against disposable or resettable account state.
