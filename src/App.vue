<template>
  <div id="app" class="container mx-auto space-y-3 py-24">
    <div>
      <h3 class="text-2xl font-bold">Toast UI Image Editor</h3>
    </div>
    <div class="flex w-full space-x-3">
      <div class="w-2/3 space-y-3">
        <tui-image-editor
          ref="tuiImageEditor"
          :include-ui="useDefaultUI"
          :options="options"
        >
        </tui-image-editor>
        <button
          @click="crop"
          class="
            bg-gray-800
            text-white
            px-8
            py-2
            rounded
            flex
            items-center
            justify-center
            space-x-3
          "
        >
          <svg
            class="h-5 w-5 text-white"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M8 17a5 5 0 01-.916-9.916 5.002 5.002 0 019.832 0A5.002 5.002 0 0116 17m-7-5l3-3m0 0l3 3m-3-3v12"
            />
          </svg>
          <span>Upload</span>
        </button>
      </div>
      <div class="w-1/3">
        <div class="bg-gray-100 shadow-md space-y-3 p-8 rounded-md">
          <h3 class="text-xl font-bold">Preview Image</h3>
          <img :src="image" class="w-auto h-auto" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "tui-color-picker/dist/tui-color-picker.css";
import "tui-image-editor/dist/tui-image-editor.css";
import { ImageEditor } from "@toast-ui/vue-image-editor";

export default {
  name: "App",
  components: {
    "tui-image-editor": ImageEditor,
  },
  data() {
    return {
      useDefaultUI: true,
      options: {
        cssMaxWidth: 700,
        cssMaxHeight: 1200,
        includeUI: {
          loadImage: {
            path: "http://localhost:8080/img/sample.jpg",
            name: "Bottle",
          },
        },
      },
      image: null,
    };
  },
  methods: {
    crop() {
      const image = this.$refs.tuiImageEditor.invoke("toDataURL");
      this.image = image;
      console.log({ image });
    },
  },
  mounted() {
    this.$nextTick(() => {
      this.crop();
    });
  },
};
</script>

<style>
</style>
