<template>
<div>
    <div
        class="new-post-container"
        ref="newPost">
        <div
            class="new-post-toolbar"
            v-bind:class="{'hide-toolbar': mouseDown}">
            <button>
                <i class="mdi mdi-format-font"></i>
                <i class="mdi mdi-menu-down"></i>
            </button>
            <ul class="dropdown-menu">
                <li
                    class="dropdown-menu-item"
                    v-for="(font, index) in fonts"
                    :key="index"
                    v-bind:style="{'font-family': font}">
                    {{ font }}
                </li>
            </ul>
            <button>
                <i class="mdi mdi-format-size"></i>
                <i class="mdi mdi-menu-down"></i>
            </button>
            <ul class="dropdown-menu">
                <li
                    class="dropdown-menu-item"
                    v-for="(size, index) in fontSizes"
                    :key="index">
                    {{ size }}
                </li>
            </ul>
            <button @click="openColorPicker">
                <i class="mdi mdi-palette"></i>
                <i class="mdi mdi-menu-down"></i>
            </button>
            <input
                type="color"
                class="element-display-none"
                id="colorPicker"
                ref="colorPicker">
            <!-- <div id="font-picker"></div> -->
            <!-- <v-select
                :items=fontSizes
                v-model="selectedFontSize"
                solo>
            </v-select>
            <input
                type="color"
                v-model="selectedFontColor"
                @change="test"> -->
            <v-btn
                outlined>
                Post
            </v-btn>
        </div>
        <div
            @mousedown="pointerDown"
            class="new-post-input-container">
            <v-textarea
                class="new-post-input apply-font"
                id="new-post-input"
                v-model="text"
                rows="1"
                auto-grow
                outlined
                :style="{'font-size': selectedFontSize, 'color': selectedFontColor + '!important'}">
            </v-textarea>


        </div>
    </div>
</div>
</template>

<script>
// import axios from "axios";
// import FontPicker from "font-picker";
// import WebFont from "webfontloader";

export default {
    name: "NewPost",
    data() {
        return {
            text: null,
            pos1: 0,
            pos2: 0,
            pos3: 0,
            pos4: 0,
            mouseDown: false,
            fontSizes: ['small', 'medium', 'large'],
            selectedFontSize: 'small',
            selectedFontColor: '#000000',
            fonts: ['Roboto', 'Pacifico'],
        }
    },
    computed: {
        fontStyle(fontName) {
            return "font-family: " + fontName;
        }
    },
    methods: {
        test() {
            console.log(this.selectedFontColor);
        },
        pointerDown: function(event) {
            event = event || window.event;
            event.preventDefault();
            this.mouseDown = true;
            // get the mouse cursor position at startup:
            this.pos3 = event.clientX;
            this.pos4 = event.clientY;

            document.onpointerup = this.pointerUp;
            // call a function whenever the cursor moves:
            document.onpointermove = this.dragElement;

        },
        pointerUp: function() {
            this.mouseDown = false;
            // stop moving when mouse button is released:
            document.onpointerup = null;
            document.onpointermove = null;
        },
        dragElement: function(event) {
            let element = this.$refs.newPost;
            event = event || window.event;
            event.preventDefault();
            // calculate the new cursor position:
            this.pos1 = this.pos3 - event.clientX;
            this.pos2 = this.pos4 - event.clientY;
            this.pos3 = event.clientX;
            this.pos4 = event.clientY;

            // set the element's new position:
            element.style.top = (element.offsetTop - this.pos2) + "px";
            element.style.left = (element.offsetLeft - this.pos1) + "px";
        },
        openColorPicker() {
            this.$refs.colorPicker.click();
        },
    },
    mounted() {
        this.$refs.newPost.style.left = "50vw";
        this.$refs.newPost.style.top = "50vh";
        // const api_key = "AIzaSyArcqIdXZv6-F2LCQ0Mam6aBJ0X7Xzbhd0";
        // const fontPicker = new FontPicker(  // eslint-disable-line no-unused-vars
        //     api_key, // Google API key
        //     "Open Sans", // Default font
        //     { limit: 250 }, // Additional options
        // );
        // console.log(fontPicker.getFonts());
        // this.fonts = fontPicker.getFonts();
        // console.log(this.fonts[0]);
        // WebFont.load({
        //     google: {
        //         families: ['Roboto', 'Pacifico']
        //     }
        // });
    },
}
</script>

<style>
.new-post-container {
    position: fixed;
    z-index: 15;
    /* border: dashed black 1px; */
}
.new-post-input-container {
    padding: 8px 8px 0 8px;
    cursor: move;
    /* border: dashed red 1px; */
}
.hide-toolbar {
    visibility: hidden;
}

.element-display-none {
    display: none;
}

.dropdown-menu {
  list-style: none;
  border: 1px solid black;
  border-radius: 5px;
  width: 100px;
  padding: 0;
  margin-top: 5px;
  max-height: 100px;
  overflow-y: scroll;
  /* display: none; */
}

.dropdown-menu-item {
  padding: 5px;
  cursor: pointer;
}

.dropdown-menu-item:hover {
    background-color: lightgrey;
}
</style>
