<template>
<div id="main__banner">
    <h1>Faça o seu Burguer</h1>

</div>
    
</template>
<script>
export default{
    name: "Banner"

}
</script>

<style scoped>
#main__banner{
    width: 100vw;
    background-image: url('https://meals.ord.to/products/bd4495407ee9c3e120cda694a3c7e117.png');
    background-position:center;
    background-repeat: no-repeat;
    background-size: contain;
    height: 100vh;
    display: flex;
    align-items: center;
}

#main__banner h1{
    color: white;
    background-color: black;
    text-align: center;
    font-size: 4rem;
    padding: 20px;
}
</style>
