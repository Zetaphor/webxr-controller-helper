# webxr-controller-helper
Automatically setup models and input mappings for WebXR controllers

### Usage

Install

```bash
$ npm install --save webxr-controller-helper
```

```js
  import { controllerHelper } from 'webxr-controller-helper';

  function onSessionStarted(session) {
    renderer.xr.setSession(session);
    renderer.setAnimationLoop(render);
    controllerHelper.setupControllers(renderer);
  }

  document.addEventListener('controllerHelperReady', function (ev) {
    controllers = ev.detail;
    console.log(`Found ${Object.keys(controllers.hands).length} ${controllers.type} controller(s)`);
    for (const hand in controllers.hands) {
      if (!controllers.hands.hasOwnProperty(hand)) continue;
      console.log(`Setup ${hand} hand controller`);
      playerRig.add(controllers.hands[hand].model);
      playerRig.add(controllers.hands[hand].grip);
    }
  });

  document.addEventListener('controllerHelperStateChange', function (ev) {
    console.log('Controller State Changed:', ev.detail);
  });

  document.addEventListener('controllerHelperValueChange', function (ev) {
    console.log('Controller Value Changed:', ev.detail);
  });

  document.addEventListener('controllerHelperAxisChange', function (ev) {
    console.log('Controller Axis Changed:', ev.detail);
  });

  document.addEventListener('controllerHelperChange', function () {
    console.log('Controller Changed:', ControllerHelper.state);
  });
```