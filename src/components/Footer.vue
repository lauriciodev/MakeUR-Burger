<template>
    <footer id="footer">
        <p>MakeUR Burger &copy; 2022</p>
        <p>Desenvolvido por <a href="#">Lauricio De Souza</a></p>
    </footer>
</template>
<script>
export default {
    name: "Footer"
}
</script>
<style scoped>
#footer{
   height: 200px;
    background-color:rgb(0, 0, 0);
    border: 3px solid ;
    display: flex;
    align-items: center;
    flex-direction: column;
    gap: 10px;
    justify-content: center;
    width: 100vw;
    
}

#footer p {
    color: rgb(255, 187, 0);
    font-size: 1.4rem;
    
}

#footer p a{
    color: white;
    text-decoration: none;
}

#footer p a:hover{
    color: rgb(255, 187, 0);
}



</style>
