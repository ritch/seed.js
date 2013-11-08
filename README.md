# seed

Seed is a simple 2d game engine.

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
  "network controller": {
    "behaviors": [{
      "type": require('./controllers/networking')
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

