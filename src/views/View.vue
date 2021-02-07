<template>
    <div id="view__mail">
        <div class="card">
            <div class="card-header">
                <router-link to="/" class="btn btn-dark"><b-icon icon="arrow-left"></b-icon> Kembali</router-link>
            </div>
            <div class="card-body">
                <Sk :show=show />
                <div v-if="sw">
                    <div class="header__mail1">
                     <div class="profil_img_mail">
                        <img src="@/assets/logo.png" class="img-thumbnail rounded">
                    </div>
                    <div class="profil__ket">
                        <span>{{views.subject}}</span>
                        <span>{{views.from}}</span>
                    </div>
                </div>
                <div class="header__mail2">
                    <span>Tanggal :</span>
                    <span>{{views.date}}</span>
                </div>
                <div class="header__mail2" v-if="views.attachments !='' ">
                    <span>attachments :</span>
                    <span class="download_attc" @click="download(attc.filename)" v-for="attc in views.attachments" :key="attc.id">
                       <b-icon icon="bookmark"></b-icon> ( {{attc.filename}},{{attc.contentType}} )
                        &nbsp;
                    </span>
                </div>
                <div class="body__mail__re">
                    <div  v-html="views.body"></div>
                </div>
                </div>
            </div>      
        </div>
    </div>   
</template>

<script>
import axios from 'axios';
import Sk from '@/components/Sk.vue'
export default {
    name:'View',
    components:{
        Sk
    },
    data(){
        return{
            views:[],
            show:true,
            sw:false,

        }
    },
    methods:{
        loader(){
            let self = this;
            setTimeout(() => {
                self.show = false;
                self.sw = true;
            }, 1000)
            
        },
        download(file){
            const mail = localStorage.getItem('email').split('@');
            const username = mail[0];
            const domain = mail[1];
            const id = this.$route.params.id;
            const url = `https://www.1secmail.com/api/v1/?action=download&login=${username}&domain=${domain}&id=${id}&file=${file}`;
            axios.get(url).then(function(res){
                window.location.href = res.config.url
            })

        }
    },
    mounted(){
        let self = this;
        let mail = localStorage.getItem('email').split('@');
        const username = mail[0]
        const domain = mail[1]
        const id = this.$route.params.id;
        const url = `https://www.1secmail.com/api/v1/?action=readMessage&login=${username}&domain=${domain}&id=${id}`;
        axios.get(url).then(function(res){
            self.loader();
            self.views = res.data;

        }).catch(e=>{
            console.log(e)
        })
    }
}
</script>

<style>

</style>