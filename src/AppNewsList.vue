<template>
    <hr>
    <h4>{{title}}</h4>
    <ul>
        <li v-for="(item,index) in news" :key="index">{{item.title}}</li>
    </ul> 
</template>

<script>
export default {
    inject:['title','news']
}
</script>