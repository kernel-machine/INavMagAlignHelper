# INAV Magnetometer alignment helper

This software is an helper for set the magnetometer alignment in [INAV](https://github.com/iNavFlight/inav),
this operation is not easy for a beginner users, the purpose of this software is to make this operation easier.

### How to use

- Move the sliders until you get the right configuration in the 3D model
- Paste the commands on the bottom in INAV Configurator
- Enter `save` to save the configuration

### KNOWN ISSUES
Some GPS modules which have a different orientation of the usual **CW 270 FLIP** don't work with this software. 

Known modules with strange orientation:
- [HGLRC M80 PRO](https://it.banggood.com/custlink/vvvYnWKpCs)

### How to run

The software is a web page, so just click [here](https://kernel-machine.github.io/INavMagAlignHelper/) to access to the page

### Development

The project uses [Three.js](https://github.com/mrdoob/three.js/), [Vue](https://vuejs.org/) and
[Element Plus](https://element-plus.org/en-US/), feel free to make your contributions making a pull request

### How to run for development

Install dependencies

```
npm install
```

Compiles and hot-reloads for development

```
npm run serve
```

Compiles and minifies for production

```
npm run build
```

Lints and fixes files

```
npm run lint
```

