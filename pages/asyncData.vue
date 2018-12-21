<template>
   <div>
       <h1>姓名： {{info.name}}</h1>
       <h1>年龄： {{info.age}}</h1>
       <h1>兴趣： {{info.hobby}}</h1>
    </div> 
</template>
<script>
import axios from 'axios'
export default {
    data() {
        return {
            name: "Hello word"
        }
    },
    // 方法二
    async asyncData(){
       let {data} = await axios.get('https://api.myjson.com/bins/11gze0')
       return {info: data}
    }
    // 方法一
    // asyncData(){
    //     return axios.get('https://api.myjson.com/bins/11gze0')
    //             .then((res)=>{
    //                 return {info:res.data}
    //             })
    // }
}
</script>

