# seed

Seed is a simple 2d game engine for node.js and the browser.

 - behavior driven game objects inspired by unity3d
 - a `pixi.js` based renderer
 - a json dsl for describing game objects by attaching behaviors
 - a game object previewer
 - a game object designer
 - a simple animation previewer

## defining game objects

The following example is a module that exports a game object definition.

```js
var seed = require('seed');
var behaviors = seed.behaviors;

module.exports = {
  "camera": {
    "behaviors": [{
      "type": behaviors.camera,
      "zoom": 1
    }]
  },
  "server network controller": {
    "serverOnly": true,
    "behaviors": [{
      "type": require('./controllers/server-networking')
    }]
  },
  "client network controller": {
    "clientOnly": true,
    "behaviors": [{
      "type": require('./controllers/client-networking')
    }]
  },
  "asteroid": {
    "behaviors": [
      {
        "type": seed.transform,
        "position": {"x": 0, "y": 0}
      },
      {
        "type": require('./behaviors/pixel-renderer'), // custom renderer
        "size": {"x": 3, "y": 3},
        "pixels": [
          0, 0,
          1, 1,
          2, 2
        ]
      },
      {
        "type": behaviors.Animation,
        "name": "float"
        "keyFrames": [
          "rotation", "+=", 10
        ]
      },
      {
        "type": behaviors.RigidBody,
        "shape": "circle"
      }
    ]
  },
  "ship": {
    "behaviors": [{
      "type": require('./ship'), // custom ship behavior
      {
        "type": behaviors.RigidBody,
        "shape": "circle"
      }
    }]
  }
}
```

## previewing

## using game objects at runtime

## writing a behavior

 - you must inherit from the `seed.Behavior` class.
 - override any of the `Behavior` class methods.
 - `this` will always be the `GameObject` the `Behavior` is attached to

Below is an example of a simple behavior. This will log the position of the game object every time it changes.

```js

exports.onPositionChanged = function(old, new) {
  // old and new are Vec2
  console.log(this.name, 'traveled', old.distanceTo(new));
}

```

