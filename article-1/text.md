# Buttery smooth animatons

I’m almost amazed what animations can bring on the table for a visitor on your webpage. When you look around at all the amazing websites featured on [Awwwards](https://www.awwwards.com/), [Tympanus/Codrops](https://tympanus.net) or [Cssdesignawards](https://www.cssdesignawards.com/). Just for an example what people can create with just a bit for code. But creating that ‘wow’ moment for users is sometimes harder to achieve than you might think. There goes so much under the hood by creating an animation. They are some complex creatures that can be tamed when doing right. It this small serie of 3 articles to try to give a little insight in animating on the web.

## Animations

Well first of all you have to get an idea of animations in general. On the web most of the animation or transitions however you wanna call it is tweening an element between to properties. The properties can be whatever you want. So let’s say for example you have an element and you wanna make it grow on an mouseover event. If you just put in a static value it sometimes create a kinda weird illusion that it’s just magically increased in front of your eyes. Without a transition it almost feels it almost feels like weird unexpected behaviour. But you can tackle that behaviour by adding a small transitions to the element. When a user is than mouseovering the element it starts growing in front of their eyes. It gives so much more depth to the experience, although this was just a box increasing in size.

All possible with little no css magic. That’s the beauty of it and it enhances the experience so much more. But for every animation there no great rule on animation, it all comes down to personal taste and just feel that vibe from it. There are dozens of way to achieve an animation in the browser where you can use regular tweening, keyframe animations or a full blown out library where we come back to later in article 3. But it is worth nothing if you wanna use the `canvas` attribute in html you can use a library like [Three.js](https://threejs.org/) or [Pixi.JS](https://www.pixijs.com/) (and trust me they are more technical than you might think).

## When is something buttery smooth

Well previously we talked about what animations are, most of you know it already but it is nice to start on the same page together. So let’s dive now a little deeper in how it actually works. When you are doing some animation in the browser it has to actually recalculate every pixel on the screen where it’s needed. So when you are doing some heavy animation work it can feel a little bit laggy or chunky when you dropping some frames, it is bad for the overall experience because you wanna enhance it for the user not make it feel bad.

Most devices today have a refresh rate of 60 screens per second to shorten 60FPS. If the browser is running an animation it want to match the screen refresh rate with your device or machine. You can actually calculate how much time each frame has to calculate before it needs to get rendered, you have (1 second / 60 = **16.66 MS**) time to do it. But in reality most of the work needs be completed before 10 MS per frame. If it needs more time than that an animation can drop a frame and continue to the next one and than it starts to get a little messy overall. So in a nutshell buttery smooth just means that the animation is constantly running close to 60FPS.

### The timeline in which order a browser handles things

When creating a website the browser needs to render and calculate everything on the screen. There are 5 major parts in the process what you should know about, also these areas you have some control. We call it the pixel pipeline, where as a developer you have the most control of some of the areas.

![Performance steps](frame-full.jpg "Layer")

So the first step is the **JavaScript execution** on the ladder. Adding DOM elements and actually compiling the code but doesn’t have to be always a visual changed.

Than the browser needs to do **style calculations**. So it looks at the DOM tree and figuring out which CSS rules it needs to apply for what element. When all the styles are applied the browser can start calculating the final styles for each element, think about cascading and inheriting styles from your parent elements.

Once the browser know which rules it needs to apply each element it needs to calculate how much space each element has on the page, we call that the **layout** part. It a quite complex task where a children with a full width needs to be inherited from their parent width for example. It is busy activity for your browser and asks quite a-lot of power.

After that the browser has to **paint** each pixel what was calculated before in the window. Also CSS-properties like the `box-shadows`, `border-radius` and `background-color`.

After that it needs to map out which layer has to be seen on top of each other. It **composites** those layers together. Children flow on top of their parents, there can be some z-index involved and they need the right overlap.

Each of those steps can be a subject to delay your animation if asks too much from that task. The benefit is that some tasks can be ran on the GPU instead of the CPU what the browser is using. So you can calculate in parallel more tasks and speed up the process. So by taking advantage of it the right way it can smooth up your animations but we talk about that in the next article.
