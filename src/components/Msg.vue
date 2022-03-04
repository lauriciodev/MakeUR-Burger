<template>
    <div class="msg">
     <p> {{ msg }} </p>
    </div>
</template>

<script>
export default{
    name: "Msg",
    props: {
        msg: String
    }


}
</script>
<style scoped>

.msg{
    text-align: center;
    width: 100%;
    max-width: 600px;
    background-color: black;
    height: 40px;
    padding: 10px;
    color: rgb(255, 208, 0);
    margin: 20px auto;
    font-size: 1.3rem;
    transition: .3s;

    
}


</style>
