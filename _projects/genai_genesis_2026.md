---
layout: page
title: SyntheSpace
description: AR furniture placement tool using 2D-to-3D model generation
img: assets/img/SyntheSpace_editor.png
importance: 2
category: projects
related_publications: false
---

Built at GenAI Genesis 2026, SyntheSpace lets you point your phone at a product image, generate a 3D model of it, and place it in your room through AR to see how it looks before buying. The motivation was the obvious problem with online furniture shopping: photos lie about scale, color, and how something fits in a specific space. We wanted to skip the guesswork.

<div style="text-align: center; margin-top: 1.5rem; margin-bottom: 1.5rem;">
  <iframe width="640" height="360" src="https://www.youtube.com/embed/Z2ziiTBzbic" title="SyntheSpace Demo" frameborder="0" allowfullscreen style="max-width: 100%;"></iframe>
</div>

The core pipeline: upload a 2D product photo, send it to Hunyuan3D which generates a GLB mesh, then load that mesh into a Three.js scene where it can be placed onto real-world surfaces via WebXR. The AR side uses hit-testing to anchor objects to detected planes, so furniture sits on the floor rather than floating mid-air.

The backend is a Python FastAPI service with Celery handling async task processing. Most of the AI work (3D generation, room reconstruction) takes too long to block on synchronously, so tasks get queued and the frontend polls for results. Hunyuan3D in particular can take a while to spin up since we used the Hugging Face Space endpoint and had to manage it as a singleton to avoid re-initialization overhead on every request.

We also built a room reconstruction flow using DepthAnything V2: upload six photos from different angles, and the backend estimates the room dimensions to pre-populate the AR scene. A separate Gemini-powered endpoint scrapes product URLs, parses out dimensions, and auto-populates the model metadata so you do not have to measure anything manually.

The frontend is React 19 with React Three Fiber wrapping Three.js, and WebXR for the actual AR session. Getting the AR working reliably on mobile required exposing the dev server over a tunnel since WebXR requires HTTPS, and we had to disable Vite's HMR to keep it stable through the tunnel.

[View on GitHub](https://github.com/freq1062/genai-genesis-2026)
