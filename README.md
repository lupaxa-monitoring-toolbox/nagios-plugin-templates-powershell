<p align="center">
    <a href="https://github.com/lupaxa-monitoring-toolbox">
        <img src="https://raw.githubusercontent.com/the-lupaxa-project/brand-assets/master/logos/organisations/monitoring-toolbox/readme-logo.png" alt="Organisation Logo" />
    </a>
</p>

<h1 align="center">Nagios Plugin Templates Powershell</h1>

PowerShell templates for Nagios-style plugin checks. Copy a script, put the check in `main`, and keep the status helpers so the plugin prints a prefixed line and exits with the matching code.

## Templates

| Script                                | Purpose                                                               |
| ------------------------------------- | --------------------------------------------------------------------- |
| [basic](src/basic/basic.ps1)          | A check with hard-coded warning and critical levels.                  |
| [advanced](src/advanced/advanced.ps1) | The same check, with `-WarningLevel` and `-CriticalLevel` overrides.  |

Both scripts use four helpers:

| Helper            | Output prefix | Exit |
| ----------------- | ------------- | ---- |
| `handle_ok`       | `OK`          | `0`  |
| `handle_warning`  | `WARNING`     | `1`  |
| `handle_critical` | `CRITICAL`    | `2`  |
| `handle_unknown`  | `UNKNOWN`     | `3`  |

`basic.ps1` calls `main` directly. `advanced.ps1` parses arguments first, then calls `main`. The warning level must stay below the critical level.

## Run

```bash
pwsh src/basic/basic.ps1
pwsh src/advanced/advanced.ps1 -WarningLevel 75 -CriticalLevel 90
```

The sample check draws a random value from 1 to 100 and compares it with the warning and critical levels. Replace that body with the real check.

Requires PowerShell 7 (`pwsh`).

## Development

```bash
make init
make powershell-check
```

<a href="https://github.com/the-lupaxa-project">
    <img src="https://raw.githubusercontent.com/the-lupaxa-project/brand-assets/master/logos/components/footer-for-child-orgs.svg" alt="The Lupaxa Project Footer" width="100%" />
</a>
