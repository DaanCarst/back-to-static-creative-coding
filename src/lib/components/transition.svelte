<script>
    import Jack from "$lib/assets/skeletonjack.png";
    import { gsap } from "gsap/dist/gsap";
    import { onMount } from "svelte";
    onMount(() => {
      gsap.to(".transition .skeleton-jack", {
        opacity: 0,
        duration: 1.5,
        scale: 0,
        rotation: 360,
        onComplete: () => {
          gsap.set(".transition", { display: "none" });
        },
      });
      gsap.to(".transition .back", {
        opacity: 0,
        duration: 0.8,
      });
      document.querySelectorAll("a").forEach((link) => {
        link.addEventListener("click", function (e) {
          e.preventDefault();
          let destination = link.href;
          gsap.set(".transition", { display: "flex" });
          gsap.fromTo(
            ".transition img",
            {
              opacity: 0,
              scale: 0,
            },
            {
              opacity: 1,
              duration: 1,
              rotation: 360,
              scale: 1,
              onComplete: () => {
                window.location = destination;
              },
            }
          );
          gsap.fromTo(
            ".transition .back",
            {
              opacity: 0,
            },
            {
              opacity: 1,
              duration: 0.4,
            }
          );
        });
      });
    });
  </script>
  <div class="transition">
    <img class="skeleton-jack" src={Jack} alt="" />
    <div class="back" />
  </div>
  <style>
    div {
      display: flex;
      justify-content: center;
      align-items: center;
      position: fixed;
      width: 100%;
      height: 100%;
    }
    .back {
      width: 100%;
      height: 100%;
      background-image: url($lib/assets/backgroundblack.avif);
      background-size: cover;
      background-position: center;
    }
    .skeleton-jack {
      width: 20rem;
      z-index: 2;
    }
  </style>