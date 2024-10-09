## flake.nix
```nix
{
  inputs = {
    # other stuff

    potatofox = {
      url = "git+https://codeberg.org/awwpotato/PotatoFox";
      flake = false;
    };
  };
}
```

## firefox.nix:
```nix
{ potatofox, ... }:
let
  profile = "default";
in
{
  programs.firefox = {
    profiles.${profile} = {
      settings = {
        "toolkit.legacyUserProfileCustomizations.stylesheets" = true;
        "svg.context-properties.content.enabled" = true;
        "layout.css.has-selector.enabled" = true;
        "browser.urlbar.suggest.calculator" = true;
        "browser.urlbar.unitConversion.enabled" = true;
        "browser.urlbar.trimHttps" = true;
        "browser.urlbar.trimURLs" = true;
        "widget.gtk.rounded-bottom-corners.enabled" = true;
        "browser.compactmode.show" = true;
        "widget.gtk.ignore-bogus-leave-notify" = 1;
        "browser.uidensity" = 1;
      };
    };
  };

  home.file.".mozilla/firefox/${profile}/chrome" = {
    source = "${potatofox}/chrome";
    recursive = true;
  };
}
```
