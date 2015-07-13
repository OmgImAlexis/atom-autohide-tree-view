# autohide-tree-view package

Hide the tree view, show it on hover.

![Image inserted by Atom editor package auto-host-markdown-image](https://raw.githubusercontent.com/olmokramer/atom-autohide-tree-view/master/screencast.gif)

## Config

| setting          | type    | unit    | default       | description |
| ---              | ---     | ---     | ---           | --- |
| `showOn`         | string  | none    | hover + touch | The type of event that should trigger show/hide of the tree view. `Hover`, `Click`, `Touch`, `None` or any combination. |
| `animate`        | boolean | none    | true          | Enable/disable the animation when showing the menu |
| `showDelay`      | number  | seconds | 0.2           | The delay before the tree view will show when hovered |
| `hideDelay`      | number  | seconds | 0.2           | The delay before the tree view will hide when hovered |
| `hiddenWidth`    | integer | pixels  | 1             | The width of the hidden tree view |
| `pushEditor`     | boolean | none    | false         | Push the editor when showing the tree view |
| `touchAreaSize`  | integer | pixels  | 50            | Size of the area at the edge of the screen where touch events can be used to show or hide of the tree view.
| `maxWindowWidth` | integer | pixels  | 0             | Max window width for which autohide should be enabled. If on a resize the window width crosses this threshold, autohide will automatically be enabled or disabled. Set to 0 to always have autohide enabled. |

## Touch events

Show/hide the tree view with swiping gestures. For touch events, the [atom-touch-events](https://atom.io/packages/atom-touch-events) package is required. You'll have to re-enable autohide-tree-view, or reload Atom, after installing atom-touch-events for the touch events to work.

## Services provided

autohide-tree-view provides a service for Show, Hide, Enable and Disable actions. To consume the service, put the following in your package's `package.json`:

```json
"consumedServices": {
  "autohide-tree-view": {
    "versions": {
      // refers to the consumer method in your package's main module
      "^0.20.0": "consumeAutohideTreeViewService"
    }
  }
}
```

And in your package's main module, put this:

```coffee
consumeAutohideTreeViewService: (service) ->
  # show/hide the tree view
  # @param delay: delay in ms before starting the animation
  service.show(delay)
  service.hide(delay)

  # enable/disable autohide behaviour
  service.enable()
  service.disable()
```

All methods return a promise that will be resolved once the tree view animation is done. It's resolved value is a boolean, indicating if the animation was finished (`true`) or cancelled (`false`). The promise is rejected if an error occurs during the animation.

## Issues/suggestions

Please file issues or suggestions on the [issues page on github](https://github.com/olmokramer/autohide-tree-view/issues/new), or even better, [submit a pull request](https://github.com/olmokramer/atom-autohide-tree-view/pulls)

## License

&copy; 2015 Olmo Kramer <br> [MIT License](LICENSE.md)
