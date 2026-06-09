# Gravl Maestro E2E Suite

Standalone Maestro suite for validating Gravl critical mobile workflows.

## Current Status

- YAML syntax validation passes for all Maestro files.
- Play Store emulator is available as `emulator-5556`.
- Gravl is installed from Google Play.
- Smoke suite passes locally against package `com.liteup.getgains`.

## Run Commands

Run the default suite:

```bash
maestro --device emulator-5556 test .maestro
```

Run smoke-tagged workflows:

```bash
maestro --device emulator-5556 test .maestro --include-tags=smoke
```

Run stateful workflows:

```bash
maestro --device emulator-5556 test .maestro --include-tags=stateful
```

Run the reset-account workout completion workflow explicitly:

```bash
maestro --device emulator-5556 test .maestro/reset-account-flows/gravl-workout-completion.yaml
```

## Validation Performed

YAML validation:

```bash
ruby -e 'require "yaml"; Dir[".maestro/**/*.yaml"].sort.each { |f| YAML.load_file(f); puts "OK #{f}" }'
```

Smoke execution attempted:

```bash
maestro --device emulator-5556 test .maestro --include-tags=smoke
```

Result:

```text
2/2 flows passed in 1m 56s.
```

## Device Requirement

Use a Play Store-enabled emulator with Gravl installed from Google Play.
