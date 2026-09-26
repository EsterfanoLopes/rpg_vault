# Lopest Shared Data

This folder contains the Foundry VTT module. Releases are built by the GitHub Actions workflow at `.github/workflows/release.yaml` in the repository root. The workflow packages only this folder's `module.json`, `assets/`, and `packs/`; other repository content is not included.

## Releasing a new version

1. **Update the module content.** Make and commit the intended changes under `lopest-shared-data/`, including any compendium pack changes. Check that the pack folders and asset paths referenced by the manifest exist.
2. **(Optional) Update the version in the tracked `module.json`.** The workflow automatically patches the release copy of `module.json` using the tag, including `version`, `manifest`, and `download`; you do not need to edit these fields for the release to work. You may update the tracked `version` if you want the repository's source manifest to reflect the latest release.
3. **Commit the release changes** to the branch/commit you intend to release.
4. **Create and push a matching version tag** from that commit. Tags must use `vMAJOR.MINOR.PATCH`, such as `v1.0.3`:

   ```bash
   git tag -a v1.0.3 -m "Release v1.0.3"
   git push origin v1.0.3
   ```

   Replace `1.0.3` with the version being released. The tag is the source of truth for the published version.
5. **Check the workflow run** in the repository's GitHub Actions tab. It validates the tag format, patches the release copy of `module.json`, creates the zip, and publishes a GitHub Release. Wait for the run to succeed before considering the release available.
6. **Verify the release assets.** The GitHub Release for the tag should contain `module.json` and `module.zip`. The zip has `module.json` at its root, alongside `assets/` and `packs/`.

## Foundry installation and updates

The release manifest has a stable URL ending in `/releases/latest/download/module.json`. Its `download` URL points to the version-specific `module.zip` for the tag. Foundry can use the stable manifest URL to check for and install newer versions; users can also install by entering that manifest URL in Foundry's module installer.

For a package listed in Foundry's official package browser, configure the package's version entry in Foundry's Package Management page to use the appropriate release manifest URL and version. Publishing a GitHub Release alone does not add the module to Foundry's official package listing.

## Important notes

- Push a **new tag for each release**. Avoid moving/reusing an existing tag; although the workflow can update an existing GitHub Release and replace its assets, changing an already published version can leave users with inconsistent files or update behavior.
- The workflow accepts only three-part numeric tags, such as `v1.2.3`; tags like `1.2.3`, `v1.2`, and `v1.2.3-rc.1` fail validation.
- The repository must allow GitHub Actions to run and the workflow's `GITHUB_TOKEN` must have permission to create releases (`contents: write`). GitHub Release assets need to be publicly accessible for Foundry to download them without authentication.
- The release zip includes only `module.json`, `assets/`, and `packs/`. If the module later needs additional runtime files, update the packaging step in `.github/workflows/release.yaml` as well.
