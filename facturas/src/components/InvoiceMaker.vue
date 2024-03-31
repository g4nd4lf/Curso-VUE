<template>
    <h1>Facturas</h1>
    <input type="text" v-model="article.item"/>
    <input type="text" v-model="article.quantity"/>
    <input type="text" v-model="article.price"/>
    <input type="text" v-model="article.totalPrice"/>
    <button @click="addItem()">  Agregar   </button>
    <table>
        <tr>
            <th>Item</th>
            <th>Quantity</th>
            <th>Price</th>
            <th>Total Price</th>
        </tr>
        <tr v-for="(elemArticle,id) in articles" :key="id">
            <th>{{elemArticle.item}}</th>
            <th>{{elemArticle.quantity}}</th>
            <th>{{elemArticle.price}}</th>
            <th>{{elemArticle.totalPrice}}</th>
        </tr>
    </table>
    <div>{{ article.item }}</div> 
    <div>{{ article.price }}</div>
</template>
<script lang="ts" setup>
    import {ref, type Ref, type ComputedRef, computed} from 'vue'
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
    const addItem=()=>{
        articles.value.push({
          item: article.value.item,
          quantity: article.value.quantity,
          price: article.value.price,
          totalPrice: (parseFloat(article.value.quantity)*parseFloat(article.value.price)).toString()
        })
    }
    const totalPrice=computed
</script>
<style>
</style>