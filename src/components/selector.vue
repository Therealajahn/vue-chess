<template>
    <div id="selector">
        <div id="shape" />
    </div>
</template>

<script>
export default {
    name: "selector",
    
}
</script>

<style scoped>

    #shape{
        position: absolute;
        width: 50px;
        height: 50px;
        border: 10px solid yellow;
        margin-left: 40px;
        /* square coordinates - border width =  cursor coor */
        margin-top: 40px;
        z-index: 2;
    }
</style>