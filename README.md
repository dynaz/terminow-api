# TermiNow:API

The API plugin for [TermiNow](https://terminow.online), adapted from
[Termux:API](https://github.com/termux/termux-api).

It exposes Android features — notifications, clipboard, sensors, telephony, storage and the rest —
to programs running in TermiNow, through the `termux-api` style commands.

## Why a separate build is needed

TermiNow looks for its plugin under its own package name. In the app's
`TermuxConstants.java`:

```java
public static final String TERMUX_API_PACKAGE_NAME = TERMUX_PACKAGE_NAME + ".api"; // com.terminow.api
```

The Termux:API builds published on Google Play and F-Droid are `com.termux.api`, so TermiNow can
never find them. This repository holds the plugin rebuilt as `com.terminow.api`.

## Signing

The plugin is reached through a permission derived from the app's package name, and the app
checks the signing certificate of the packages that call it. **The plugin must be signed with the
same certificate as the TermiNow app.** With Play App Signing that means releasing it through the
same Play account, so Play signs both with the same app signing key. A plugin signed with any
other key installs but is refused at runtime.

## The commands

The `termux-api` command-line programs are a package, not part of this app. They are built for
`com.terminow` in [`dynaz/terminow-package`](https://github.com/dynaz/terminow-package). This
repository is only the Android plugin that those commands talk to.

## Status

The upstream source has not been imported yet, so this repository holds only this README.

Porting it means: setting `applicationId` to `com.terminow.api`, signing with the TermiNow
certificate, and updating the constants in the app that still name Termux:API and link to
`termux/termux-api`.

## License

Released under [GPLv3 only](https://www.gnu.org/licenses/gpl-3.0.html), as a fork of
[`termux/termux-api`](https://github.com/termux/termux-api).
