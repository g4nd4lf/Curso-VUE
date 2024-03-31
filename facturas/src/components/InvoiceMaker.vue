<template>
    <h1>Invoice</h1>
    <div class="form">
        <label>Item</label>
        <label>Quantity</label>
        <label>Price</label>
        <div></div>
        <input ref="itemInput" type="text" v-model="article.item" @keydown.enter="addItem"/>
        <input type="text" v-model="article.quantity" @keydown.enter="addItem"/>
        <input type="text" v-model="article.price" @keydown.enter="addItem"/>
        <button @click="addItem()">  Add   </button>
    </div>
    <table v-show="notEmpty">
        <tr>
            <th>Item</th>
            <th>Quantity</th>
            <th>Price</th>
            <th>Total Price</th>
        </tr>
        <tr v-for="(elemArticle,id) in articles" :key="id">
            <td>{{elemArticle.item}}</td>
            <td>{{elemArticle.quantity}}</td>
            <td>{{elemArticle.price}}</td>
            <td>{{elemArticle.totalPrice}}</td>
        </tr>
    </table>

</template>
<script lang="ts" setup>
    import {ref, type Ref, type ComputedRef, computed} from 'vue'
    const itemInput = ref<HTMLInputElement | null>(null); // Ref for the item input element

    interface IArticle {
        item: string,
        quantity: string,
        price: string,
        totalPrice: string
    }
    let article:Ref<IArticle> =ref({
        item: "",
        quantity: "",
        price: "",
        totalPrice: ""
        }
        )
    let articles:Ref<Array<IArticle>> =ref([])
    
    const notEmpty = computed(() => articles.value.length)

    const addItem=()=>{
        articles.value.push({
          item: article.value.item,
          quantity: article.value.quantity,
          price: article.value.price,
          totalPrice: (parseFloat(article.value.quantity)*parseFloat(article.value.price)).toString()
        })
        article.value={item:"",quantity:"",price:"",totalPrice:""}
        if (itemInput.value){
            itemInput.value.focus();
        }
    }
</script>
<style scoped>
.form{
    color: rgb(28, 15, 50);
    display: grid;
    grid-template-columns: repeat(4,100px);
}
table {
  border-collapse: collapse;
  width: 100%;
}

th, td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #DDD;
}

tr:hover {background-color: #D6EEEE;}
</style>