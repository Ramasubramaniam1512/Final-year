<template>
<form @submit.prevent="sendFile" enctype="multipart/formdata">
    <div v-if="message"
    :class="`message ${error ?'is-danger':'is-sucess'}`">
     <div class="message-body">{{ message }}</div>
</div>
    <div class="field">


        <div class="file is-boxed is-primary">
            <label class="file-label">
                <input 
        ref="files"
        type="file"
        accept="application/vnd.ms-excel, text/csv, application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
        @change="selectFile"
        class="file-input"/>
         <span class="file-cta">
        <span class="file-icon">
            <i class="fas fa-upload"></i>
        </span>
        <br>
        <span class="file-label">
            choose a file
        </span>
    </span>
            </label>
        
        </div>
      
    </div>

    
    <div class="field">
        <button class="button is-info">Send</button>
    </div>
</form>
</template>
<script>
import axios from 'axios';
export default{
    name:"simple-upload",
    data() {
        return {
            file:"",
            message:"",
            error:false
        }
    },
    methods:{
        selectFile(){
            this.file=this.$refs.files.files[0];
            this.error = false;
            this.message="";
        },
        async sendFile () {
          const formdata = new FormData();
          formdata.append('file',this.file);
          try{
          await axios.post('/upload',formdata);
          this.message="File has been uploaded";
          this.file="";
          this.error= false;
          }catch(err){
            this.message="Something went wrong";
            this.error= true;
          }

        }
    }
    
}
</script>
<style>
/* @import "bourbon";
@import url(https://fonts.googleapis.com/css?family=Lato:400,700,300); */
body{
    
    /* background-color: #002a3f; */
    padding: 0 ;
    margin: 0;

}
input[type="file"]{
    display: none;
}

label{
    color: white;
    height: 60px;
    width: 250px;
    background-color: #f5af09;
    position: absolute;
    margin: auto;
    top:0;
    bottom: 0;
    left: 0;
    right: 0;
    font-size: 20px;
    display: flex;
    justify-content: center ;
    align-items: center;
    font-family: "Montserrat", sans-serif;
}
</style>