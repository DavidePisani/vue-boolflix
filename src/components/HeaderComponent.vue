<template>
    <header>
        <h1>BOOLFLIX</h1>
        
    <div class="search">
        <input  @keyup.enter="$emit('FilmsText',filterText),$emit('SeriesText',filterText)" v-model="filterText" type="text" placeholder="Cosa volgio Guardare?">
        <button @click="$emit('FilmsText',filterText),$emit('SeriesText',filterText) "> CERCA </button>
    </div>
        
    </header>

</template>

<script>
export default {
    name: 'HeaderComponent',
    data(){
        return{
            filterText:''  
            
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
    height: 80px;

    h1{
        color: red;
        padding: 10px;
        padding-left: 30px;
        font-size: 60px;
    }
    .search{
        padding:30px;

        input{
            padding: 5px;
            outline: none;
        }

        button{
            background-color: black;
            color: red;
            padding: 5px;
            margin-left: 3px;
            border: 1px solid red;
        }
    }
}

</style>