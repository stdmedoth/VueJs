<template>
  <div class="conversor">
    <h2> {{moedaA}} para {{moedaB}} </h2>
    <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
    <input type="button" v-on:click="converter" value="Converter">
    <h2>{{moedaB_value}}</h2>
  </div>
</template>


<script>
  export default{
    name: "conversor",
    props: ["moedaA", "moedaB"],
    data(){
      return {
        moedaA_value: "",
        moedaB_value: 0
      };
    },
    methods:{
      converter(){
        let de_para = this.moedaA + "_" + this.moedaB;
        let url = "https://free.currconv.com/api/v7/convert?apiKey=4466dea03154c810fa69&q=" + de_para + "&compact=y";
        fetch(url)
        .then( res=>{ return res.json() } )
        .then(json=>{
          let cotacao = json[de_para].val;
          this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2);
        })
      }
    }

  };
</script>


<style>
  .conversor{
    max-width: 300px;
    padding: 20px;
    box-shadow: 0 4px 8px 0;
  }
</style>
