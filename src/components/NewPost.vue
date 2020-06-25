<template>
<div class="container">
    <div @mousedown="pointerDown" class="new-post-container" ref="newPost">
        <p class="new-post-text">{{ text }}</p>
        <v-btn
        fab
        x-small
        class="button-info"
        @click="toggleInfo">
            <v-icon>mdi-information-outline</v-icon>
        </v-btn>

        <div v-if="infoBox" class="info-box">
            <p>Mouse Down: {{ mouseDown }}</p>
            <p>Position 1: {{ pos1 }}</p>
            <p>Position 2: {{ pos2 }}</p>
            <p>Position 3: {{ pos3 }}</p>
            <p>Position 4: {{ pos4 }}</p>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: "NewPost",
    data() {
        return {
            text: "New Post",
            pos1: 0,
            pos2: 0,
            pos3: 0,
            pos4: 0,
            mouseDown: false,
            infoBox: false
        }
    },
    methods: {
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
        toggleInfo() {
            this.infoBox = !this.infoBox
        },
    },
    mounted() {
        this.$refs.newPost.style.left = "50vw";
        this.$refs.newPost.style.top = "50vh";
    // transform: translate(-50%, -50%);
    }
}
</script>

<style>
.new-post-container {
    position: fixed;
    z-index: 10;
}
.new-post-text {
    padding: 15px;
    border: dashed black 1px;
    cursor: move;
}
.container {
    margin-top: 100px;
}
.info-box {
    margin-top: 16px;
}
.button-info {
    margin-right: 0;
    padding-right: 0;
}
</style>
