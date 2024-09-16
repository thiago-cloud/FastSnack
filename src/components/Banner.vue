<template>
    <div id="main-banner">
        <h1>Faça seu hamburguer </h1>
    </div>
</template>
<script>
    export default{
        name: 'Banner',
        components:{

        }
    }
</script>
<style scoped>
    #main-banner{
        background-image: url('../../public/img/hamburguer.jpg');
        background-position: center;
        background-size:cover;
        height:500px;
        background-repeat: no-repeat;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #main-banner h1{
        color:#fff;
        text-align:center;
        font-size: 60px;
        padding:20px 40px;
    }
</style>
