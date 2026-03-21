# ESPHome Custom Component <a href="https://www.paypal.com/donate?hosted_button_id=6K9UYUZ4SZMVC"><img style="vertical-align:middle" src="https://www.paypalobjects.com/en_GB/i/btn/btn_donate_SM.gif"></a>

With the release of ESPHome 2025.2.0, custom components were removed from the ESPHome core.

This component brings back support for such components.

## DISCLAIMER

I lifted the custom component code from ESPHome 2024.10.0 as-is. It seems to work for me, but I only have a single project that has a custom component, so YMMV.

## USAGE

You need to add the custom components to your YAML. How to do that depends on which version of ESPHome you use.

Before ESPHome v2026.3.0:
```
external_components:
  - source: github://robertklep/esphome-custom-component@v1.0.0
    components: [ custom, custom_component ]
```

After ESPHome v2026.3.0:
```
external_components:
  - source: github://robertklep/esphome-custom-component
    components: [ custom, custom_component ]
```

#### Using ESPHome v2026.3 or later

ESPHome v2026.3.0 changed component registration, which means that any calls to `App.register_component()` will cause compilation errors. This may require some changes to your YAML.

If you had something like this before:
```
custom_component:
  - lambda: |-
      auto my_component = new MyComponent();
      App.register_component(my_component);
      return { my_component };
```

It should now look like this:
```
custom_component:
  - lambda: |-
      auto my_component = new MyComponent();
      return { my_component };
    components:
      - id: my_component
```

## LICENSE

The ESPHome license (mixed GPL3/MIT) applies. See [the LICENSE file](LICENSE) for more information.
