# README

## Set up

Install `gitleaks`:

```bash
brew install gitleaks
```

Edit `.gitleaks.toml`:

```toml
[[rules]]
id = "korean-phone-number"
description = "Korean Phone Number"
regex = '''01[016789][-]?\d{3,4}[-]?\d{4}'''
tags = ["PII"]
```
