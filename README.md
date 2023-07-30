# d2gl-custom-shader-presets
Additional slang shader presets for D2GL

## Scaling in D2GL

Recently **bayaraa** introduced support for multi-pass shaders in [D2GL](https://github.com/bayaraa/d2gl). [cnc-ddraw](https://github.com/FunkyFr3sh/cnc-ddraw) had basic support for single-pass shaders for quite some time, so what really changed? *D2GL* offers HD text, which means that text is rendered separately. This means we aren't concerned with text readability and shaders can be pushed a bit harder without sacrifices. Moreover due to multi-pass support combining shaders gives more options.

## Challanges of scaling D2

[Libretro shaders](https://github.com/libretro/slang-shaders) are mostly oriented toward scaling older systems, where resolution is pretty low (common resolution for *SNES* is 256x224 as an example). Those shaders are also typically created with integer scaling in mind: 2x, 3x, 4x of original size and so on. On the other hand, common resolution for *Diablo 2* is 1068x600 (when used with [SGD2FreeRes](https://github.com/mir-diablo-ii-tools/SlashGaming-Diablo-II-Free-Resolution) for wide resolution support) and that means fractional scaling, when upscaling to something like 1080p (1920x1080). This means that most shaders will look bad (mostly due to artifacts). Prevously something like *windowed/jinc2* gave decent results, but now most players will probably switch to new addition: *FSR*.

## Beyond FSR

[FSR 1.0](https://gpuopen.com/fidelityfx-superresolution/#howitworks) is made out of two shaders: *EASU* (Edge-Adaptive Spatial Upsampling) and *RCAS* (Robust Contrast-Adaptive Sharpening). Basically first one is responsible for edge detection and upscaling, second one is used for sharpening. Sharpening shader can be additionally tuned with some parameters, which is great since if sharpening is too aggresive it can create [ringing artifacts](https://en.wikipedia.org/wiki/Ringing_artifacts). Which is the case with default settings that are used inside *D2GL* - here is showcase (first row) with different values (default is 0.2):

![FSR RCAS vs fishku RCAS](./screenshots/comparison1.png)

Currently *D2GL* ignores parameters inside slang presets (*.slangp* extension) and that means they can be changed only directly in slang shader files (*.slang* extension). If you using *FSR* I would recommend changing `FSR_SHARPENING` inside `data/shaders/fsr/shaders/fsr-pass1.slang` to value between 0.4 and 1.0. So for example with 0.7, line would look like this:

`#pragma parameter FSR_SHARPENING "FSR RCAS Sharpening Amount (Lower = Sharper)" 0.7 0.0 2.0 0.1`

Lets go back previous image and look at second row. This is re

![FSR EASU+RCAS vs AA+RCAS vs AA+UNIFORM NN+RCAS](./screenshots/comparison2.png)
![FSR EASU+RCAS vs AA+RCAS vs AA+UNIFORM NN+RCAS](./screenshots/comparison3.png)
![FSR EASU+RCAS vs AA+RCAS vs AA+UNIFORM NN+RCAS](./screenshots/comparison4.png)

## Usage

## Screenshots

[![Screenshot006](./screenshots/Screenshot006s.png)](./screenshots/Screenshot006.png) [![Screenshot009](./screenshots/Screenshot009s.png)](./screenshots/Screenshot009.png)
[![Screenshot014](./screenshots/Screenshot014s.png)](./screenshots/Screenshot014.png) [![Screenshot025](./screenshots/Screenshot025s.png)](./screenshots/Screenshot025.png)
[![Screenshot029](./screenshots/Screenshot029s.png)](./screenshots/Screenshot029.png) [![Screenshot033](./screenshots/Screenshot033s.png)](./screenshots/Screenshot033.png)

## Credits

**Hyllian** and **fishku** for providing useful tips.
