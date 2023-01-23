  <template>
    <div class="section">
      <div class="container">
        <simple-upload/>
      </div>
    </div>
  </template>
  <script>
  import SimpleUpload from'./simple-upload.vue';
  export default{
    name:"App",
    components:{SimpleUpload}
  }
  </script>