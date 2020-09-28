Projects continuously migrated from PHP to .NET Standard.

---

This repository contains .NET projects compatible with .NET Standard being compiled from unmodified PHP source codes using PeachPie compiler.

## Building projects:

```shell
dotnet build
```

**Release build:**

```shell
dotnet build -c Release -p:VersionSuffix=preview
```

## Providing package readme

Some packages are compiled right from the original repository. To alter or add a readme text, put `readme.md` in a corresponding folder: `{package name}/readme.md` (lowercased).

## Other projects:

- WordPress https://github.com/iolevel/wpdotnet-sdk
- MediaWiki https://github.com/iolevel/peachpie-mediawiki
- Responsive File Manager https://github.com/gordon-matt/peachpie-responsive-file-manager
- ASCIIMath2TeX.Net https://github.com/cannorin/ASCIIMath2TeX.Net
