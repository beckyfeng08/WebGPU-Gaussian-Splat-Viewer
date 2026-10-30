# Project5-WebGPU-Gaussian-Splat-Viewer

Rebecca Feng
[LinkedIn](https://www.linkedin.com/in/beckyfeng0803/), [personal website](https://beckyfeng08.github.io/)
* Tested on: Google Chrome Version 155.0.8059.80 (Official Build) (arm64) on Apple M4 Max

https://beckyfeng08.github.io/WebGPU-Gaussian-Splat-Viewer
### Live Demo

[![](img/thumb.png)](https://beckyfeng08.github.io/WebGPU-Gaussian-Splat-Viewer)

### Demo Video/GIF

[![](img/video.mp4)](TODO)

### Overview
This WebGPU based Gaussian splatting application follows the original [3DGS paper](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/), with the following features:
- .ply loading
- rendering point clouds and gaussian splats
- spherical harmonics for view dependent coloring
- preprocess pass to cull gaussians out of camera view, and sort based on depth

To run on your own:

```
git clone https://github.com/beckyfeng08/WebGPU-Gaussian-Splat-Viewer.git
cd WebGPU-Gaussian-Splat-Viewer
npm install
npm run dev
```

### Performance
<!-- Compare your results from point-cloud and gaussian renderer, what are the differences?
For gaussian renderer, how does changing the workgroup-size affect performance? Why do you think this is?
Does view-frustum culling give performance improvement? Why do you think this is?
Does number of guassians affect performance? Why do you think this is? -->

I tested how long it took for a single pass for the gaussian and point cloud rendering methods individually, given our bike and bonsai ply files. The pass includes the preprocess and render passes. These were averaged over 200 frames, starting at the 300th frame:
| Renderer | bonsai (ms) | bike (ms) | cookie (ms) | star cookie (ms) |
|---|---|---|---|---|
| Gaussian | 5.78 | 7.79 | 4.79 | 4.21 |
| Point | 2.18 | 5.31 | 2.31 | 2.91 |

![](images/graph.png)

Overall as we increase the number of points in our scene, it takes a longer amount of time to process it per frame, as expected. Furthermore, it takes a noticeably shorter time to render the points as opposed to the gaussians (since we don't need to do all those calcucations in the fragment shader, and we also don't need two separate passes during each frame).

For our gaussian renderer, changing the workgroup-size affects performance in that blah blah blah.

In our code, we culled gaussians when they are not in our scene so that our scene runs faster. We see that it is the case below for our bike scene... 


### Credits

- [Vite](https://vitejs.dev/)
- [tweakpane](https://tweakpane.github.io/docs//v3/monitor-bindings/)
- [stats.js](https://github.com/mrdoob/stats.js)
- [wgpu-matrix](https://github.com/greggman/wgpu-matrix)
- Special Thanks to: Shrek Shao (Google WebGPU team) & [Differential Guassian Renderer](https://github.com/graphdeco-inria/diff-gaussian-rasterization)
