# VS Code Extenstion Distribution

This repository gives an example of how to distribute, install and update private VS Code extensions using Homebrew and Homebrew Bundle.

## What problem is this solving?

At the time of writing, VS Code does not provide any way to manage private extensions. Your only option is to package an extension into a `.vsix` file and then ask people to download it and run `code --install-extension $THE_FILE`. You then will need to do that again if you want them to update. This means you have problems of _distribution_, _installation_ and _updates_.

## How does it work?

### Prerequisites

* we assume that you can package your VS Code extension using `vsce` and that you can upload the versioned package to a file server which is accessible by your users.
* we assume that your organization is already using (or wants to use) Homebrew and has a private tap which you use to distribute formulae.
* we assume that your organization makes use of (or wants to  use) Homebrew Bundle – specifically that you install VS Code and VS Code extensions using a Brewfile.

### Distributing the extension

1. **Create the formula**: copy the formula_example.rb to your private tap and change the pieces. For this example let's say it is named `my-extension`
2. **Try insatlling the formula**: Locally you should try `brew install Formula/my-extension.rb` and make sure it installs without erorr. You'll also notice that people can manually install the extenstion by running `install-my-extension`
2. **Update your Brewfile to install the extension**: add two lines to your Brewfile to install the extension:
```ruby
brew "my-extension"
vscode "/opt/homebrew/opt/kiki-copilot/lib/kiki-copilot.vsix"
```
