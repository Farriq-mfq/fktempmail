<template>
<div v-if="show">
  <div class="header__mail1">
        <div class="profil_img_mail">
            <b-skeleton type="avatar"></b-skeleton>
        </div>
        <div class="profil__ket">
            <span> <b-skeleton animation="wave" width="100px"></b-skeleton></span>
            <span>loading...</span>
        </div>
    </div>
    <div class="header__mail2 skle1">
        <span>Tanggal :</span>
        <span class="skle"><b-skeleton animation="wave" width="200px" ></b-skeleton></span>
    </div>
    <div class="header__mail2 skle1">
        <span>attachments :</span>
        <span class="skle"><b-skeleton animation="wave" width="200px" ></b-skeleton></span>
    </div>
    <div class="body__mail__re">
        <b-card>
            <b-skeleton animation="wave" width="85%"></b-skeleton>
            <b-skeleton animation="wave" width="55%"></b-skeleton>
            <b-skeleton animation="wave" width="70%"></b-skeleton>
            <b-skeleton animation="wave" width="40%"></b-skeleton>
            <b-skeleton animation="wave" width="54%"></b-skeleton>
            <b-skeleton animation="wave" width="50%"></b-skeleton>
            <b-skeleton animation="wave" width="80%"></b-skeleton>
        </b-card>
    </div>
</div>
</template>

<script>
export default {
    name:'Sk',
    props:['show']
}
</script>

<style>

</style>