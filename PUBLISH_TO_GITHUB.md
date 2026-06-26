# Publish docs.tradeark.ai

This directory is the standalone GitHub repository for the TradeArk documentation site:

```text
https://github.com/tradeark/docs.tradeark.ai.git
```

## Local checks

Run from the parent workspace:

```powershell
cd C:\code\signal_executor
pip install -r docs.tradeark.ai/requirements.txt
mkdocs build --strict -f docs.tradeark.ai/mkdocs.yml
```

Or run from this repository:

```powershell
pip install -r requirements.txt
mkdocs build --strict --clean
```

## Publish

```powershell
git status --short
git add .
git commit -m "Update docs site"
git push origin main
```

GitHub Pages is deployed by `.github/workflows/docs.yml` using GitHub Actions. The custom domain is configured by `docs/CNAME` and should contain:

```text
docs.tradeark.ai
```
