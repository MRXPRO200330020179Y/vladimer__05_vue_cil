<template>
    <div class="card">
        <h3>{{title}}</h3>
        <button class="btn" @click="open">
            {{isNewsOpen ? 'Закрыт':'Открыть'}}
        </button>
        <button class="btn danger" v-if="wasRead" @click="unmark">
            Отметить непрочитанной
        </button>
        <div v-if="isNewsOpen">
            <hr>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Nesciunt, optio aperiam earum tempore quo distinctio tenetur iusto temporibus praesentium, nihil et, unde dolor beatae perferendis quasi laborum! Dolore, quas consectetur!</p>
            <button v-if="!wasRead" class="btn primary" @click="mark">Прочеть новости</button>
        </div>
    </div>
</template>

<script>
export default {
    // props:['title'],
    // emits:['open-news'],
    props:{
        wasRead:Boolean,
        title:{
          type:String,
          required:true
        },
        id:{
            type:Number,
            required:true
        },
        isOpen:{
            type:Boolean,
            required:false,
            default:false,
            validator(value){
                return value === true || value === false
            }
        }
    },

    emits:{
        'open-news':null,
        // 'read-news'(){
        //     if(id){
        //         return true
        //     }
        //     console.log('Нет параметра id для emid read-news')
        //     return false
        // } 
        unmark:null
    },

    data(){
        return{
            isNewsOpen: this.isOpen
        }
    },

    methods:{
        open(){
            this.isNewsOpen = !this.isNewsOpen
            if(this.isNewsOpen){
               this.$emit('open-news') 
            }
        },

        mark(){
            this.isNewsOpen = false
            this.$emit('read-news', this.id)
        },

        unmark(){
            this.$emit('unmark', this.id)
        }
    }
}
</script>