# RPG Vault

This repository includes the **Lopest Shared Data** Foundry VTT module in `lopest-shared-data/`. The root repository also contains campaign notes and other files; only the module folder is packaged for module releases.

## FAQ

### A new version was released. How do I get it in Foundry?

For the Lopest Shared Data manual refresh procedure, install/update it again from the stable module manifest URL, as if installing it for the first time:

`https://github.com/EsterfanoLopes/rpg_vault/releases/latest/download/module.json`

In Foundry's Setup screen, open **Add-on Modules → Install Module**, paste the URL into the manifest URL field, and install/update the package. Then open the world and check **Game Settings → Manage Modules**. Make sure **Lopest Shared Data** is enabled; enable it again if it is inactive.

The manifest URL stays the same between releases. The workflow publishes a new versioned zip and updates the stable manifest to point to the latest release. Wait for the GitHub Actions release workflow to finish successfully before refreshing Foundry.

> **Do not manually delete the module folder first.** Foundry's documented package update process compares the installed version with the manifest and downloads a newer package when one is available. Normal Foundry updates are generally in-place and do not inherently require uninstalling/reinstalling or re-enabling a module; the steps above describe this project's recommended manual refresh and activation check. See Foundry's [Package Management documentation](https://foundryvtt.com/article/package-management/) for its standard update process.

### Where are the release instructions?

See [lopest-shared-data/README.md](lopest-shared-data/README.md) for how to prepare and publish a new version tag.
