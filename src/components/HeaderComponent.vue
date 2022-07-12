<template>
    <header>
        <h1>BOOLFLIX</h1>
        
    <div class="search">
        <input type="text" placeholder="Cosa volgio Guardare?">
    </div>
        
    </header>

    
    
</template>

<script>
export default {
    name: 'HeaderComponent',
    data(){
        return{
            
        }
    }
}
</script>

<style lang="scss" scoped>
header{
    background-color: black;
    display: flex;
    align-items: center;
    justify-content: space-between;

    h1{
        color: red;
        padding: 20px;
    }
    .search{
        padding:30px;

        input{
            padding: 5px;
        }
    }
}

</style>