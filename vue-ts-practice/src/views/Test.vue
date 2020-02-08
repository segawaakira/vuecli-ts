<template>
  <div class="about">
    <h1>郵便番号から住所反映します</h1>
    <Address
      :defaultZip = "1670053"
    ></Address>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator';
  import Address from "@/components/Address.vue";

  @Component({
    components: {
      Address,
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