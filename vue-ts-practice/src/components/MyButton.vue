<template>
    <button @click="onClick">{{text}}</button>
</template>

<script lang="ts">
    import {Component, Emit, Prop, Vue} from "vue-property-decorator";

    @Component
    export default class MyButton extends Vue {

        @Prop()
        public greet?: string;
        @Prop()
        public text?: string;

        @Emit()
        public click(){
        }

        public onClick(){
            alert(this.greet);
            this.click();
        }
    }
</script>