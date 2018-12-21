<template>
    <div>
        <h2>new-content</h2>
        <p>newsId:{{$route.params.id}}</p>
        <ul>
            <li>
                <nuxt-link :to="{name:'index'}"></nuxt-link>
                <a href="/">home</a>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        // 参数校验
        validate({params}){
            return /^\d+$/.test(params.id);
        },
        data() {
            return {
                title: this.$route.params.title
            }
        },
        // 独立设置head信息
        head(){
            return {
                title:this.title,
                meta:[
                    {hid:'description',name:'news1',content:'this is news page '}
                ]
            }
        }
    }
</script>

<style scoped>

</style>