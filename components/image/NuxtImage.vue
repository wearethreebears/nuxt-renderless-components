<template>
  <div class="relative h-0" :style="`padding-top: ${height}`">
    <picture>
      <source :data-srcset="image.sizes.xs" ref="imageXS" />
      <source
        :data-srcset="image.sizes.sm"
        :media="`(min-width: ${breakpoints.sm})`"
        ref="imageSM"
      />
      <source
        :data-srcset="image.sizes.md"
        :media="`(min-width: ${breakpoints.md})`"
        ref="imageMD"
      />
      <source
        :data-srcset="image.sizes.lg"
        :media="`(min-width: ${breakpoints.lg})`"
        ref="imageLG"
      />
      <source
        :data-srcset="image.sizes.xl"
        :media="`(min-width: ${breakpoints.xl})`"
        ref="imageXL"
      />
      <source
        :data-srcset="image.sizes.xxl"
        :media="`(min-width: ${breakpoints.xxl})`"
        ref="imageXXL"
      />
      <img
        :data-src="image.sizes.lg"
        :alt="image.alt"
        :height="image.height"
        :width="image.width"
        class="absolute top-0 left-0 object-cover w-full overflow-hidden transition-opacity duration-500 ease-in-out opacity-0"
        ref="imageDefault"
      />
    </picture>
  </div>
</template>

<script lang="ts">
import Vue, { PropOptions } from "vue";

import { Image } from "~/interfaces/Image";
import { Breakpoints } from "@/tailwind.config.js";

export default Vue.extend({
  props: {
    image: {
      required: true,
      type: Object,
    } as PropOptions<Image>,
  },

  data() {
    return {
      observer: {} as IntersectionObserver,
      breakpoints: Breakpoints,
    };
  },

  computed: {
    height(): string {
      let percentage = (this.image.height / this.image.width) * 100;
      return `${percentage}%`;
    },
  },

  mounted() {
    this.observer = new IntersectionObserver(
      (images: IntersectionObserverEntry[]): void => {
        let { isIntersecting } = images[0];

        const elXS = this.$refs.imageXS as HTMLElement,
          elSM = this.$refs.imageSM as HTMLElement,
          elMD = this.$refs.imageMD as HTMLElement,
          elLG = this.$refs.imageLG as HTMLElement,
          elXL = this.$refs.imageXL as HTMLElement,
          elXXL = this.$refs.imageXXL as HTMLElement,
          elDefault = this.$refs.imageDefault as HTMLElement;

        const srcXS = elXS.getAttribute("data-srcset") as string,
          srcSM = elSM.getAttribute("data-srcset") as string,
          srcMD = elMD.getAttribute("data-srcset") as string,
          srcLG = elLG.getAttribute("data-srcset") as string,
          srcXL = elXL.getAttribute("data-srcset") as string,
          srcXXL = elXXL.getAttribute("data-srcset") as string,
          srcDefault = elDefault.getAttribute("data-srcset") as string;

        if (isIntersecting) {
          elXS.setAttribute("srcset", srcXS);
          elSM.setAttribute("srcset", srcSM);
          elMD.setAttribute("srcset", srcMD);
          elLG.setAttribute("srcset", srcLG);
          elXL.setAttribute("srcset", srcXL);
          elXXL.setAttribute("srcset", srcXXL);
          elDefault.setAttribute("src", srcDefault);
          elDefault.addEventListener("load", () => {
            elDefault.classList.remove("opacity-0");
            elDefault.classList.add("opacity-1");
            return elDefault.setAttribute("data-lazy", "loaded");
          });
        }
      }
    );

    this.observer.observe(this.$el);
  },

  destroyed() {
    this.observer.disconnect();
  },
});
</script>

<style>
.absolute {
  position: absolute;
}

.relative {
  position: relative;
}

.top-0 {
  top: 0;
}

.left-0 {
  left: 0;
}

.w-full {
  width: 100%;
}

.h-0 {
  height: 0;
}

.opacity-0 {
  opacity: 0;
}

.opacity-1 {
  opacity: 1;
}

.overflow-hidden {
  overflow: hidden;
}
.transition-opacity {
  transition-property: opacity;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 150ms;
}

.ease-in-out {
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}

.duration-500 {
  transition-duration: 500ms;
}

.object-cover {
  object-fit: cover;
}
</style>
