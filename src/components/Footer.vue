<template>
    <div>
        <span>Doube click to edit a todo</span>
        <span>Created by petehunt</span>
        <span>Part of TodoMVC</span>
    </div>
</template>
<script>
export default {
    name:'Footer'
}
</script>
<style scoped>
div {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
}
span {
    color: #c3bfbf;
    font-size: 15px;
    margin-top: 20px;
}
</style>