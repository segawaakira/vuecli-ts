<template>
  <div class="home">
    <p> {{greetText}}</p>
    <MyButton :greet="greetText" :text="text" @click="onMyButtonClicked"></MyButton>
  </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';
    import MyButton from "@/components/MyButton.vue";

    @Component({
        components: {
            MyButton,
    },
    })
    export default class Home extends Vue {
        public greetText: string = "Hello";
        public text: string = "ボタンです";
        public onMyButtonClicked(){
            this.greetText = "こんにちは";
        }
    }
</script>