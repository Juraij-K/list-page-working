<template>
    <h1>Products</h1>
        
        
        <input id="search-box" type="text" v-model="search" placeholder="search for products">
        <div v-if="products.length">
            
                <div v-for="product in filteredProducts" :key="product.id"   class="product">
                    <router-link :to="{ name: 'ProductDetails', params:{ id: product.id }}">
                        <div class="product-thumbnail">
                            
                                
                            <img :src="product.thumbnail" alt="">
                            <h2 class="product-title">{{product.title}}</h2>
                            <h2 class="product-price">USD {{product.price}}/-</h2>
                        </div>
                    </router-link>
                </div>
            
            
        </div>
        <div v-else>
            <p>Loading products...</p>
        </div>
    
    
</template>

<script>

export default {
    
    data(){
        return{
            products:[],
            search: ""
        }
    },
    
    mounted(){
        fetch('http://localhost:3000/products')
        
        .then(res => res.json())
        
        .then(data => this.products = data)
        .catch(err => console.log(err.message))
    },
    computed:{
        filteredProducts: function(){
            return this.products.filter((product) =>{
                return product.title.toLowerCase().match(this.search.toLowerCase())
            });
        }
    }
    
}


</script>

<style>
.container{
    
    margin: 0 auto;
}
.product{
    display: flex;
    float: left;
}
.product .product-thumbnail{
    width: 300px;
    height: 350px;
    background: #f4f4f2;
    color: #fff;
    text-shadow: 3px 3px #000;
    

    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    position: relative;

    border-radius: 10%;
    cursor: pointer;
    float: left;
    margin: 1em;
}
.product .product-thumbnail:hover{
    background: #ddd;
}
.product .product-thumbnail img{
    flex-shrink: 0;
    min-width: 100%;
    min-height: 100%
}
.product-title, .product-price{
    position: absolute;
    left: 30px;
}
.product-title{
    bottom: 45px;
}
.product-price{
    bottom: 15px;
}
.product a{
    text-decoration: none;
}
nav button{
    width: auto;
    height: auto;
    
    border:none;
}
nav button:hover{
 background: #42b983;
}
#search-box{
   width: 300px; 
   height: 30px;
   
}
</style>