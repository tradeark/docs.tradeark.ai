# docs.tradeark.ai

This folder contains the standalone documentation site for TradeArk, published at `https://docs.tradeark.ai/`.

## Local preview

```powershell
pip install -r docs.tradeark.ai/requirements.txt
mkdocs serve -f docs.tradeark.ai/mkdocs.yml
```

Open the local preview URL printed by MkDocs, usually `http://127.0.0.1:8000`.

## Strict build check

```powershell
mkdocs build --strict -f docs.tradeark.ai/mkdocs.yml
```

## GitHub Pages

The workflow at `.github/workflows/docs.yml` builds this folder and deploys it to GitHub Pages.

GitHub Pages only hosts the static manual. The TradeArk backend, installers, and release artifacts still need to be hosted elsewhere, such as `tradeark.ai` or GitHub Releases.
