---
author: IngridAtMicrosoft
ms.service: azure-media-services
ms.topic: include
ms.date: 01/28/2019
ms.author: inhenkel
---

## Use CLI Shell

### Sign in

Using a local install of the CLI requires signing in to Azure. This step is not required for Azure Cloud Shell. Sign in with the `az login` command.

If the CLI can open your default browser, it will do so and load a sign-in page. Otherwise, you need to open a browser page and follow the instructions on the command line to enter an authorization code after navigating to https://aka.ms/devicelogin in your browser.

### Specify location of files

Many Media Services CLI commands allow you to pass a parameter with a file name. If you are using **Cloud Shell**, you can upload your file to your clouddrive (using Bash or PowerShell).

![Upload files]

Whether you are using a local CLI or **Cloud Shell**, you need to specify the file path according to the OS or Cloud Shell (Bash or PowerShell) that you are using. Below are some examples:

Relative path to the file (all OS)

* `@"mytestfile.json"`
* `@"../mytestfile.json"`

Absolute file path on Linux/Mac and Windows OS

* `@ "/usr/home/mytestfile.json"`
*    `@"c:\tmp\user\mytestfile.json"`

Use `{file}` if the command is asking for a path to the file. For example, `az ams transform create -a amsaccount -g resourceGroup -n custom --preset .\customPreset.json`. <br/>
Use `@{file}` if the command is going to load the specified file. For example, `az ams account-filter create -a amsaccount -g resourceGroup -n filterName --tracks @tracks.json`.
