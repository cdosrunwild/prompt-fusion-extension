# Fusion

Fusion is an [auto1111 webui extension](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Developing-extensions) that adds more possibilities to the native prompt syntax. Among other additions, it allows to interpolate between the embeddings of different prompts, continuously:

```
# linear prompt interpolation
[night light:magical forest: 5, 15]

# catmull-rom curve prompt interpolation
[night light:magical forest:norvegian territory: 5, 15, 25:catmull]

# linear attention interpolation
(fire extinguisher: 1.0, 2.0)

# prompt-editing-aware attention interpolation
[(fire extinguisher: 1.0, 2.0)::5]
```

The prompt interpolation feature is similar to [Prompt Travel](https://github.com/Kahsolt/stable-diffusion-webui-prompt-travel), which allows to create videos of images generated by navigating the latent space iteratively. Unlike Prompt Travel however, instead of generating multiple images, Fusion allows you to travel during the sampling process of *a single image*. Also, instead of interpolating the latent space, it uses the embedding space to determine intermediate embeddings. 

Prompt interpolation is also similar to the [Prompt Blending](https://github.com/amotile/stable-diffusion-backend/tree/master/src/process/implementations/automatic1111_scripts). The main difference is that this extension calculates a new embedding for every step, as opposed to calculating it once and using that same one embedding for all the steps. 

The attention interpolation feature is similar to [Shift Attention](https://github.com/yownas/shift-attention), which allows to generate multiple images with slight variations in the attention given to certain parts of the prompt. Unlike Shift Attention, instead of generating multiple images, Fusion allows to shift the attention of certain parts of a prompt during the sampling process of *a single image*.

## Examples

### 1. Influencing the beginning of the sampling process

Interpolate linearly (by default) from `lion` (step 0) to `bird` (step 7) to `girl` (step 10), and stay at `girl` for the rest of the sampling steps:

```
[lion:bird:girl: , 6, 9]
```

![curve1](https://user-images.githubusercontent.com/32277961/214725976-b72bafc6-0c5d-4491-9c95-b73da41da082.gif)

### 2. Influencing the middle of the sampling process

Interpolate using a bezier curve from `fireball monster` (step 0) to `dragon monster` (step 12, because 30 steps * 0.4 = step 12), while using `seawater monster` as an intermediate control point to steer the curve away during interpolation and to get creative results:

```
[fireball:seawater:dragon: , .1, .4:bezier] monster
```

![curve2](https://user-images.githubusercontent.com/32277961/214941229-2dccad78-f856-42bb-ae6b-16b65b273cda.gif)

## Features
- [Prompt interpolation using a curve function](https://github.com/ljleb/prompt-fusion-extension/wiki/Prompt-Interpolation)
- [Attention interpolation aware of contextual prompt editing](https://github.com/ljleb/prompt-fusion-extension/wiki/Attention-Interpolation)
- Complete backwards compatibility with prompt syntax from https://github.com/AUTOMATIC1111/stable-diffusion-webui

## Webui supported releases

The following webui releases are officially supported:
- `v1.0.0-pre`

## Installation
1. Visit the **Extensions** tab of Automatic's WebUI.
2. Visit the **Install from URL** subtab.
3. Copy and paste `https://github.com/ljleb/prompt-fusion-extension` in the **URL for extension's git repository** textbox.
4. Press the **Install** button. 


## Usage
- Check the [wiki pages](https://github.com/ljleb/fusion/wiki) for the extension documentation.

## Similar projects

- https://github.com/Kahsolt/stable-diffusion-webui-prompt-travel
- https://github.com/yownas/shift-attention
