# Gravl Maestro E2E Suite

Standalone Maestro suite for validating Gravl critical mobile workflows.

## Current Status

- YAML syntax validation passes for all Maestro files.
- Local emulator is available as `emulator-5554`.
- Functional execution is currently blocked because the target Android package is not installed:
  - expected package: `com.liteup.getgains`

## Run Commands

Run the default suite:

```bash
maestro --device emulator-5554 test .maestro
```

Run smoke-tagged workflows:

```bash
maestro --device emulator-5554 test .maestro --include-tags=smoke
```

Run stateful workflows:

```bash
maestro --device emulator-5554 test .maestro --include-tags=stateful
```

Run the reset-account workout completion workflow explicitly:

```bash
maestro --device emulator-5554 test .maestro/reset-account-flows/gravl-workout-completion.yaml
```

## Validation Performed

YAML validation:

```bash
ruby -e 'require "yaml"; Dir[".maestro/**/*.yaml"].sort.each { |f| YAML.load_file(f); puts "OK #{f}" }'
```

Smoke execution attempted:

```bash
maestro --device emulator-5554 test .maestro --include-tags=smoke
```

Result:

```text
2/2 flows failed because Maestro could not launch app com.liteup.getgains.
```

## Next Requirement

Install a Gravl Android build on the emulator before functional validation:

```bash
adb install path/to/gravl.apk
```

Then rerun:

```bash
maestro --device emulator-5554 test .maestro --include-tags=smoke
```
