<template>
  <div>
    <p>郵便番号</p>
    <input type="text" v-model="inputZipCode" />
    <button @click="onClick()">{{inputZipCode}}</button>
    <p>都道府県</p>
    <input type="text" :value="inputPref" />
    <p>住所</p>
    <input type="text" :value="inputAddress" />
  </div>
</template>

<script lang="ts">
    import {Component, Emit, Prop, Vue} from "vue-property-decorator";

    @Component
    export default class MyButton extends Vue {

      // @propで、親コンポーネントから取得
      @Prop()
      public defaultZip?: string;

      // 通常のvueでいうdata
      inputZipCode: any = this.defaultZip;
      inputPref: string = "※郵便番号入力で自動反映されます";
      inputAddress: string = "※郵便番号入力で自動反映されます";

      public onClick(){
        alert(this.inputZipCode);
        function createCORSRequest(method: string, url: string) {
          let xhr = new XMLHttpRequest();
            if ("withCredentials" in xhr) {
                xhr.open(method, url, true);
            //@ts-ignore
            } else if (typeof XDomainRequest != "undefined") {
              //@ts-ignore
                xhr = new XDomainRequest();
                xhr.open(method, url);
            } else {
                // xhr = null;
            }
            return xhr;
        }

        const _this = this;
        const xhr = createCORSRequest('GET', 'https://api.zipaddress.net/?zipcode=' + this.inputZipCode);
        if (!xhr) {
            throw new Error('CORS not supported');
        }
        xhr.onload = function(){
          const responseArr = JSON.parse(xhr.response);
          _this.inputPref = responseArr.data.pref;
          _this.inputAddress = responseArr.data.address;
        alert('ssss');
        };
        xhr.onerror = function(error){
          console.log(error);
        };
        xhr.send();
      }

    }
</script>
