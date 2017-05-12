# aframe-heatmap3d
Terrain-like heatmap data viz component for AFrame

![alt text](https://morandd.github.io/aframe-heatmap3d/example/example.png "Example image")

[Demo](https://morandd.github.io/aframe-heatmap3d/example/)
[GitHub](https://github.com/morandd/aframe-heatmap3d/)

This component is totally indebted to [Bryik's terrain component](https://github.com/bryik/aframe-terrain-model-component) and the work by others that went into that. This component is separated from that one because the usage and internals have totally changed, but the basic approach is the same.


# API #

Attribute | Description | Default
--- | --- | ---
src | Data to visualize  | |
srcMobile | Alternative URL to use when viewing on mobile devices | |
palette | Color palette | redblue |
opacityMin | Minimum opacity | 0.2 
opacityMax | Max opacity | 1
ignoreZeroValues | If true, zero values in the data will not be rendered | true
stackBlurRadius | Blur effect. See below. | null
stackBlurRadiusMobile | Blur effect. See below. | =stackBlurRadius
scaleOpacity | Scale opacity of peaks? | true
scaleOpacityMethod | "log" or "linear" scaling of opacity | "linear"
invertElevation | Default: white=1, black=0. If this is true, white=0, black=1 | false
width | width of component, in AFrame units | 1
height | depth of component (on Z axis, not Y axis), in AFrame units. Note that the height (Y axis) is always 1 | =width


### Color Palettes ###
There are a few built-in palettes: `greypurple`, `aquablues`, `reds`, `redblue`, `grass`, `greens`, and `autumn`. These are taken from
[ColorBrewer](http://colorbrewer2.org). You can also specify a palette as a JSON array, as shown in the example.

## Blurring ##
You should generate the heap maps properly and feed them as images to this component to display. However a poor man's way of building heatmaps is to plonk down the data in an image, then blur it.

Health warning: Blurring the data at the client is hacky. It's slow, and if you're displaying scientific data, not so denfensible/transparent. That said, it can be a useful shortcut. To blur we can use the StackBlur javascript library. You can provide a sharp image as the `src` (only works with images, not JSON) then specify a stackBlur value, and the StackBlur library will be invoked. Note it is a bit slow: in the example, blurring takes 0.6s on a modern Macbook Pro, which slows page load time. So it is better to blur the source image. 


# Using #
D3 is required.

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/4.4.1/d3.min.js"></script> 
<script src="aframe-heatmap3d.js"></script>

<!-- Optional: (only needed if you want to use StackBlur) -->
<script src="stackblur.min.js"></script>

```

## TODO ##
- Improve handling of load sequence, use Promises and onload events properly.

