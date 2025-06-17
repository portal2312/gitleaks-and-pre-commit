# README

## Set up

Install [`gitleaks`](https://github.com/gitleaks/gitleaks):

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

Scan directory commits:

```bash
gitleaks dir -v
```

Scan git commits:

```bash
gitleaks git -v
```

### Set up pre-commit

Install `pre-commit`:

```bash
brew install pre-commit
```

Go to your repo. Then, edit `.pre-commit-config.yaml`:

```yml
# See https://pre-commit.com for more information
# See https://pre-commit.com/hooks.html for more hooks
repos:
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.27.2
    hooks:
      - id: gitleaks
        name: gitleaks dir
        entry: gitleaks dir
        args: ["--verbose", "--redact=0"]
        pass_filenames: false
```

`pre-commit install` 을 실행하여 git hook 에 `pre-commit` 을 설치합니다:

```bash
pre-commit install
```

> [!NOTE]
> hook 이 추가 및 변경되는 경우만 다시 실행해야 합니다.  
> hook 을 아에 사용하지 않는 경우, `pre-commit uninstall` 을 실행해야 합니다.

Test:

```bash
pre-commit run --all-files
```

Try `git commit`:

```bash
git commit -v -m 'Update README.md'
```
