<template>
    <footer>
        <div class="footer">
             &copy; 
        </div>
    </footer>
</template>

<script setup>
    import { ref, reactive } from 'vue'
    let Date = new Date()
    console.log(Date)
</script>

<style lang="less" scoped>
    *{
        margin: 0;
        padding: 0;
        font-family: "Ma Shan Zheng", "Caveat", cursive;
    }
    .footer{
        text-align: center;
    }

</style>