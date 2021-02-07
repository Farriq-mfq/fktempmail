<template>
    <div class="container">
      <div class="row">
      <div class="col-md-4 col-lg-4 col-sm-4">
        <div class="card mb-3">
          <div class="card-header">
            <h5>Alamat email sementara anda</h5>
          </div>
          <div class="card-body">
           <div class="form-group">
             <input type="text" class="form-control formText" :value="email">
           </div>
           <div class="form-group">
             <button class="btn button" @click="copy()"><b-icon icon="files"></b-icon> {{button}}</button>
           </div>
          </div>
        </div>
      </div>
      <div class="col-md-8 col-lg-8 col-sm-8">
        <div class="card ck">
          <div class="card-header">
            <div class="row align-items-center">
              <div class="col-4">
                <button class="btn" @click="copy()">
                  <b-icon icon="files"></b-icon> 
                  Copy
                </button>
              </div>
              <div class="col-4">
                <button class="btn" @click="remove()">
                  <b-icon icon="trash"></b-icon>
                  Remove
                </button>
              </div>
              <div class="col-4">
                <button class="btn" @click="refresh()">
                  <b-icon icon="bootstrap-reboot"></b-icon>
                  Refresh
                </button>
              </div>
            </div>
          </div>
          <div class="card-body">
            <div v-if="$route.name != 'View'">
                <div class="card-header">
                Kotak masuk
              </div>
              <div class="card-body email_body">
                <div class="email__null" v-if="emailnull">
                  <img src="@/assets/sad.png">
                  <h4 class="text-center">
                  Email kosong
                  </h4>
                </div>
                <List :lists=list />
              </div>
            </div>
            <router-view></router-view>
          </div>
        </div>
      </div>
    </div>
    </div>
</template>

<script>
import axios from 'axios'
import List from '@/components/List.vue'
export default {
  name: "Home",
  components:{
    List
  },
  data(){
    return {
      email:localStorage.getItem('email'),
      button:'Copy',
      username:'',
      domain:'',
      list:[],
      emailnull:false,
    };
  },
  methods:{
    copy(){
      let self = this;
      const text = document.querySelector('.formText');
      text.select();
      text.setSelectionRange(0,99999);
      document.execCommand('copy');
      if(document.execCommand('copy')){
        self.button = 'Copied';
      }
    },
    remove(){
      axios.get('https://www.1secmail.com/api/v1/?action=genRandomMailbox').then(function(res){
      localStorage.setItem('email',res.data[0]);
      const text = document.querySelector('.formText');
      text.value = localStorage.getItem('email');
    })
    },
    setList(data){
      this.list = data;
    },
    refresh(){
      let self = this;
      const mail = self.email;
      const x = mail.split('@');
      self.username = x[0];
      self.domain = x[1];
      axios.get(`https://www.1secmail.com/api/v1/?action=getMessages&login=${self.username}&domain=${self.domain}`).then(function(res){
        if(res.data != ""){
        self.emailnull = false;
        setTimeout(() => {
          self.setList(res.data)
        }, 1000)
        
        }else{
        self.emailnull = true;
      }
    })
    }
  },
  mounted(){
    let self = this;
    axios.get('https://www.1secmail.com/api/v1/?action=genRandomMailbox').then(function(res){
      if(localStorage.getItem('email')===null){
        localStorage.setItem('email',res.data[0])
        self.email = localStorage.getItem('email')
      }
    })
      const mail = self.email;
      const x = mail.split('@');
      self.username = x[0];
      self.domain = x[1];
    axios.get(`https://www.1secmail.com/api/v1/?action=getMessages&login=${self.username}&domain=${self.domain}`).then(function(res){
      if(res.data != ""){
        self.emailnull = false;
        self.setList(res.data)
      }else{
        self.emailnull = true;
      }
    }).catch(e=>{
      console.log(e)
    })
  }
      
};
</script>