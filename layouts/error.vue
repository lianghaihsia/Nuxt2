<template>
    <div>
        <h2 v-if="error.statusCode == 404">404 你需要的页面没有找到</h2>
        <h2 v-else-if="error.statusCode == 500">500 服务错误</h2>
    </div>
</template>
<script>
export default {
    props:['error']
}
</script>

