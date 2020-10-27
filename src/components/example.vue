<template>
  <div class="my-div">
      <button @click="hienThongBao()" class="btn btn-primary">Click</button>
  </div>
</template>

<script>
export default {
    name: 'example',
    data(){
        return{
            alert: "Thong bao",
        }
    },
    methods:{
        hienThongBao(){
            alert(this.alert);
        }
    }
}
</script>
<style>

</style>