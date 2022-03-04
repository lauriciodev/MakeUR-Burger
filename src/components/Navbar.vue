<template>
    <nav id="nav">
        <router-link to="/">
            <img id="logo" :src="logo" :alt="alt">
        </router-link>
        <router-link to="/">Home</router-link> 
        <router-link to="/Pedidos">Pedidos</router-link>
    </nav>
</template>
<script>
export default {
    name: "Navbar",
    props: ["logo", "alt"]

}
</script>

<style scoped>
#logo{
    width: 50px;
    position: relative;
}
#nav{
    box-shadow: 1px 2px 5px yellow;
    background-color:rgb(0, 0, 0);
    display: flex;
    justify-content: center;
    gap: 30px;
    align-items: center;
    padding: 10px;
    width: 100vw;
}
#nav a{
    color: rgb(255, 187, 0);
    text-decoration: none;
    font-size: 1.4rem;
    transition: .1s ease-in;
}

#nav a:hover{
    color: rgb(255, 255, 255);
    
}

</style>
