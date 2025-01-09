# Contributing

These instructions are for Pakuranga College staff looking to edit this extension.

## Editing

- Clone this repository by running `git clone https://github.com/pakcoldigitech/pcmsvsc.git`, or download it as a zip file.
- Add new `extensionDependencies` to `package.json` by clicking the gear icon on the extension and copying the extension ID.
- Add default settings by copying them from `%AppData%\Code\User\settings.json` to `configurationDefaults` in `package.json`. (Press `Ctrl`+`Shift`+`P` in VSCode and search for `settings.json` to find and open it automatically.)
- Test the new changes by running in VSCode with `F5`, which will open a new VSCode instance with the extension installed.

## Publishing

These instructions mostly repeat what can be found on the [VSCode website](https://code.visualstudio.com/api/working-with-extensions/publishing-extension).

- Install [Node.js](https://nodejs.org) (a runtime for JavaScript; also installs the package manager 'npm', which is like what pip is for Python). ___Requires local admin access___.
- Run `npm install -g @vscode/vsce` (installs the package for publishing VSCode extensions).
- Get a Personal Access Token from the [pakcoldigitech Azure organization page](https://dev.azure.com/pakcoldigitech/_usersSettings/tokens), for 'All accessible organizations' with 'Full access'. If you can't log in to this page with your school account, ask Mr McLeod for the password of the main account, and use that to [add your school account to the Azure organization](https://dev.azure.com/pakcoldigitech/_settings/users).
- Run `vsce login pakcoldigitech` and paste the Personal Access Token.
- Run `vsce publish patch` to automatically publish the new version, change the version number in `package.json` and add the appropriate tag to the git repository. ___NB: `vsce publish` reports permission errors when run from a UNC path, but not when run from H: drive.___
- Alternatively, update the version number in `package.json` manually, run `git tag v0.0.X` to add the tag to git (or `git tag -a v0.0.X -m "Message"` to include a message with the tag), and run `vsce publish` without the word `patch` to publish the new version.
- This extension attempts to follow [Semantic Versioning](https://semver.org/), i.e the minor version number should only be incremented if we make the extension do something new, and the major version number should only change if we intend to release the extension to the general public and functionality has changed incompatibly.
- Run `git push origin --tags` to push the changes and the new tags to GitHub.
- _Optional_: If you want the latest release to show up under [GitHub Releases](https://github.com/pakcoldigitech/pcmsvsc/releases), sign in to the releases page with a GitHub account that has been added as a collaborator to this project (again ask Mr McLeod to do this), click the button to add a new release, and upload the VSIX file that you can create with `vsce package`. ___Warning: Once you've published a release on GitHub, they enforce mandatory 2FA on your account. If there were any warning of this, Mr McLeod certainly wouldn't have done it, because he hates 2FA.___

## Installation

### Setting up to automatically install on a new workstation computer

___Requires local admin access___.

- Copy from `T:\Technology\Computer Studies\pakcoldigitech.pcmsvsc-0.0.1` to `C:\Users\Default\.vscode\extensions\pakcoldigitech.pcmsvsc-0.0.1`, ideally with `.vscode` set to be hidden. This is an old version of the extension, which will be copied from `C:\Users\Default` to each new user account when they first log in for the week. When that user first opens VSCode, it will update the extension and trigger the installation of all dependencies.
- The alternative is to copy your entire `%UserProfile%\.vscode\extensions\` folder, which means the dependencies will already be installed upon first opening VSCode, but this takes prohibitively long to copy.
- It is also useful to copy the following settings to `C:\Users\Default\AppData\Roaming\Code\User\settings.json`, because they can't be changed by an extension:
```json
{
  "security.allowedUNCHosts": ["internal.pakuranga.school.nz"],
  "security.workspace.trust.enabled": false,
  "workbench.welcomePage.walkthroughs.openOnInstall": false
}
```
