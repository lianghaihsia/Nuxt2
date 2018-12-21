<template>
    <div>
        <h2>new-list</h2>
         <ul>
            <li>
                <a href="/">home</a>
                <a href="/news/123">new-1</a>
                <a href="/news/456">new-2</a>
            </li>
            <li><nuxt-link 
                :to="{name:'news-id',params:{id: 123,title:'lianghaihsia'}}">NEWS</nuxt-link></li>

        </ul>
    </div>
</template>

<script>
export default {
    transition:'test'
};
</script>

<style scoped>
</style>