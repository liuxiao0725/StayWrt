# StayWrt# RE-CP-03 ImmortalWrt 25.12 builder

This repository is a GitHub Actions build scaffold for JDCloud 百里 / RE-CP-03 (MediaTek Filogic, MT7986A). It requests an ITB sysupgrade image and includes Argon, iStore, Nikki, DDNSTO, and Simplified Chinese LuCI translations.

## Important

- This workflow builds from the `openwrt-25.12` branch of ImmortalWrt. That is a moving branch, not a pinned, reproducible release. Check the build log and image metadata before flashing.
- The workflow is **not a prebuilt firmware image**. It must be uploaded to a GitHub repository and run using Actions. The resulting artifact is only safe to flash after the workflow succeeds and the generated image is verified for the RE-CP-03 board and your bootloader.
- Third-party package feeds can change or break. iStore's own README warns that it supports only x86_64 and arm64 repository architectures and that firmware builders must resolve dependencies. The workflow stops on feed/configuration/build errors instead of pretending success.
- Argon is sourced from upstream; Nikki from nikkinikki-org; iStore from linkease; DDNSTO from linkease/nas-packages.

## Run it

1. Create a new empty GitHub repository and upload the contents of this folder.
2. Open **Actions**, enable workflows if prompted, choose **Build RE-CP-03 ImmortalWrt 25.12**, and click **Run workflow**.
3. Wait for the job to finish. Download the `re-cp-03-immortalwrt-itb` artifact.
4. Confirm the output filename contains `jdcloud_re-cp-03` and ends in `.itb`. Do not flash if the build failed, the output is missing, or the target/profile is different.

## Included packages

- `luci-theme-argon`
- `luci-app-store` (iStore)
- `nikki`, `luci-app-nikki`, `luci-i18n-nikki-zh-cn`
- DDNSTO packages when found in the current `linkease/nas-packages` tree
- `luci-i18n-base-zh-cn`, `luci-i18n-firewall-zh-cn`

If the DDNSTO packages are no longer present at the paths searched by the workflow, the workflow fails rather than silently omitting them.
