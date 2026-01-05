# 🐺 3D Interactive Portfolio (Dogstudio Clone)

![Project Preview](https://wolf3d-5uz8h9joj-premdeshmane-01s-projects.vercel.app/)
Hey! 👋 This is a project I built to push my skills in **React Three Fiber** and **WebGL**.

I decided to reverse-engineer their core interaction: a 3D character that follows your scroll and morphs its texture when you hover over project titles.

## 💡 What I Built

It’s a mix of a standard HTML UI and a 3D Canvas scene that interact seamlessly.

* **Scroll-Linked Animation:** As you scroll down the page, the 3D model rotates, moves, and scales in sync with the DOM content using **GSAP ScrollTrigger**.
* **Custom Shader Injection:** This was the tricky part. Instead of writing a raw shader from scratch, I hooked into Three.js's standard `MeshMatcapMaterial` using `onBeforeCompile`. This allowed me to inject my own GLSL logic to smoothly blend between two different Matcap textures based on a `progress` variable.
* **Dynamic Backgrounds:** I used the modern CSS `:has()` pseudo-class to handle the background image transitions purely in CSS, keeping the JS focused on the 3D logic.

## 🛠️ The Stack

* **React** (Vite)
* **@react-three/fiber** & **@react-three/drei** - For the 3D scene.
* **GSAP** - For the complex timeline animations and ScrollTrigger.
* **GLSL** - For the custom texture blending logic.

## 🧠 The "Cool" Code Bit

The most interesting part of this build was making the texture transition smooth. I had to replace parts of the default shader string to accept two textures (`uMatcapTexture1`, `uMatcapTexture2`) and mix them using a `smoothstep` function driven by a GSAP animation.

```javascript
// A snippet from my Dog.jsx
shader.fragmentShader = shader.fragmentShader.replace(
  "vec4 matcapColor = texture2D( matcap, uv );",
  `
    vec4 matcapColor1 = texture2D( uMatcapTexture1, uv );
    vec4 matcapColor2 = texture2D( uMatcapTexture2, uv );
    float progress = smoothstep(uProgress - transitionFactor, uProgress, ...);
    vec4 matcapColor = mix(matcapColor2, matcapColor1, progress );
  `
)
🚀 How to Run It
Clone the repo:

Bash

git clone [https://github.com/premdeshmane-01/3d_wolfie.git](https://github.com/premdeshmane-01/3d_wolfie.git)
Install the dependencies:

Bash

npm install
Start the dev server:

Bash

npm run dev
📬 Connect
Prem Deshmane

GitHub: @premdeshmane-01
