<template>
  <div>
    <p>郵便番号</p>
    <input type="text" id="js-zipcode" :value="defaultZip" />
    <button @click="onClick">適用</button>
    <p>都道府県</p>
    <input type="text" id="js-pref" value="※郵便番号入力で自動反映されます" />
    <p>住所</p>
    <input type="text" id="js-address" value="※郵便番号入力で自動反映されます" />
  </div>
</template>

<script lang="ts">
    import {Component, Emit, Prop, Vue} from "vue-property-decorator";

    @Component
    export default class MyButton extends Vue {

        @Prop()
        public defaultZip?: string;

      public onClick(){
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

        const inputZipCode:HTMLInputElement = <HTMLInputElement>document.getElementById("js-zipcode");
        const inputPref:HTMLInputElement = <HTMLInputElement>document.getElementById("js-pref");
        const inputAddress:HTMLInputElement = <HTMLInputElement>document.getElementById("js-address");
        const xhr = createCORSRequest('GET', 'https://api.zipaddress.net/?zipcode=' + inputZipCode.value);
        if (!xhr) {
            throw new Error('CORS not supported');
        }
        xhr.onload = function(){
          const responseArr = JSON.parse(xhr.response);
          inputPref.value = responseArr.data.pref;
          inputAddress.value = responseArr.data.address;
        };
        xhr.onerror = function(error){
          console.log(error);
        };
        xhr.send();
      }
    }
</script>
