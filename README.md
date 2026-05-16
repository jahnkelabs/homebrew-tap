# jahnkelabs homebrew tap

A shared **[Homebrew tap](https://docs.brew.sh/Taps)** for managing formulas belonging to the `jahnkelabs` organization.

## Publishers

Publishers are other repositories belonging to the `jahnkelabs` organization that write their formulas to this repository. To write formulas to this repository, a publisher can configure a GitHub Workflow that authenticates using the `HomebrewTap` GitHub App installed for the organization. Organization-wide credentials for authenticating a Workflow have been configured as follows:

| Kind | Name | Purpose |
|------|------|--------|
| Variable | `HOMEBREW_TAP_GH_APP_ID` | Numeric GitHub App ID for the `HomebrewTap` app. |
| Secret | `HOMEBREW_TAP_GH_APP_SECRET_KEY` | PEM private key for the `HomebrewTap` app. |

### Minting a tap token in Actions

Use `actions/create-github-app-token` with the shared organization credentials to mint a short-lived access token. The access token can be accessed via `steps.tap-token.outputs.token`:

```yaml
- uses: actions/create-github-app-token@v2
  id: tap-token
  with:
    app-id: ${{ vars.HOMEBREW_TAP_GH_APP_ID }}
    private-key: ${{ secrets.HOMEBREW_TAP_GH_APP_SECRET_KEY }}
    owner: jahnkelabs
    repositories: |
      homebrew-tap
    permission-contents: write
```
