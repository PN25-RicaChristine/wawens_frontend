<template>
<div class="container mt-5 pt-5" id="app">
    <b-jumbotron bg-variant="transparent">WAWEN'S UBE HALAYA : <br>
        <p id="category">{{category}}</p>
    </b-jumbotron>
    <b-row>
        <b-col lg="4" v-for="(item, index) in products" :key="index">
            <b-card id="gallery" :img-src="item.image" img-alt="Image" img-top img-height="300px" class="mb-5">
                <b-link @click="selectedProducts = item" data-toggle="modal" data-target=".bd-example-modal-lg" style="color:#8028d8;">
                    <h3 style="font-family:Arial;font-weight:bolder;text-align:left;">{{item.name}}</h3>
                </b-link>
                <h5>Price : &#x20B1; {{item.price}} / {{item.unit}}</h5>
            </b-card>
        </b-col>
    </b-row>
    <div id="productModal" class="modal fade bd-example-modal-lg" role="dialog" aria-labelledby="myLargeModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="row">
                    <div class="col">
                        <p style="font-size:19px; margin-left:20px;font-family: Comic Sans MS;">
                            <strong>{{selectedProducts.name}}</strong>
                        </p>
                        <img :src="selectedProducts.image" style="width:100%; height: 80%;margin-top:5px;margin-left:20px;">
                        <h5 style="font-size:20px; text-align:left; margin-left:20px;">
                            <strong>Price : &#x20B1; {{selectedProducts.price}} / {{selectedProducts.unit}}</strong>
                        </h5>
                    </div>
                    <div class="col">
                        <p style="font-size:19px; text-align:left;">
                            <strong>DESCRIPTION</strong>
                        </p>
                        <p style="font-size:14px;">
                            An
                            <strong>Ubechi</strong> is the best for all age to taste!
                            <br>Children Multi Purpose Bowl Baby Food Supplement Rice
                            <br>
                            <br>
                            <strong>INGREDIENTS:</strong>
                            <br>Pure Purple Ube, Butter, Sugar, Milk, Flour, Egg
                            <br>
                            <br>
                            <strong>DELIVERY:</strong>
                            <br>Within 2 kilometer all delivery is FREE upon minimum of 2 cakes ordered
                            Delivery fee starts beyond 2 kilometers 9 cakes or less -can set date and time of delivery
                            More than 9 cakes orders cannot set date and time but the owner will update you when:
                            <br>
                            <strong>
                                <br>RETAIL PRICE:
                            </strong> Php 850/cake (530 grams Net Weight).
                            <br>(Wholesale rates available upon request)
                            <br>
                            <br>Shelf life from production:
                            Room temp" 1-2 days Freezer: 30 days Chiller. 10-14 days
                            Best consumed within 7 days from production
                        </p>

                        <strong style="font-size:19px">QUANTITY</strong>

                        <div class="quantity-toggle" id="app">
                            <center>
                                <button @click="decrement(selectedProducts)">&mdash;</button>
                                <input type="text" v-model="selectedProducts.sub_quantity" readonly>
                                <button @click="increment(selectedProducts)">&#xff0b;</button>
                            </center>
                            <button id="cart" @click="toCart(selectedProducts)" data-dismiss="modal">
                                Add to Cart
                                <i class="fa fa-shopping-cart"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    mounted() {
        this.retrieve();
        if (!localStorage.getItem('carts')) {
            localStorage.setItem('carts', '[]')
        }
    },
    data() {
        return {
            show: false,
            products: null,
            selectedProducts: {},
        };
    },
    computed: {
        category() {
            var category = localStorage.getItem('category')
            return category
        }
    },
    methods: {
        toCart(object) {
            var carts = JSON.parse(localStorage.getItem('carts'))
            var isPresent = false
            carts.find(cart => {
                if (cart.id == object.id) {
                    cart.sub_quantity += object.sub_quantity
                    cart.sub_total = object.price * object.sub_quantity
                    isPresent = true
                }
            })
            if (!isPresent) {
                object.sub_total = object.price * object.sub_quantity
                carts.push(object)
            }
            console.log(isPresent)
            localStorage.setItem('carts', JSON.stringify(carts))
            object.sub_quantity = 1
        },
        increment(object) {
            object.sub_quantity++;
        },
        decrement(object) {
            if (object.sub_quantity === 1) {
                object.sub_quantity = 1;
            } else {
                object.sub_quantity--;
            }
        },
        retrieve() {
            let product = [{
                    id: 1,
                    name: "Ube Halaya",
                    price: 100.50,
                    unit: "pack",
                    sub_quantity: 1,
                    sub_total: 100.50,
                    image: require("@/assets/halaya.jpg")
                },
                {
                    id: 2,
                    name: "Buchi",
                    price: 70.75,
                    unit: "pack",
                    sub_quantity: 1,
                    sub_total: 100.50,
                    image: require("@/assets/buchi.jpg")
                },
                {
                    id: 3,
                    name: "Ube Halaya Happy Birthday Cake",
                    price: 700.25,
                    unit: "order",
                    sub_quantity: 1,
                    sub_total: 100.50,
                    image: require('@/assets/cake.png')
                },
                {
                    id: 4,
                    name: "Ubequencher",
                    price: 80.10,
                    unit: "glass",
                    sub_quantity: 1,
                    sub_total: 100.50,
                    image: require("@/assets/ubequencher.png")
                }
            ];
            this.products = product;
        }
    }
};
</script>

<style scoped>
.jumbotron {
    color: #8028d8;
    font-size: 50px;
    font-family: Segoe Script;
    font-weight: bolder;
    text-align: center;
    padding-bottom: 2px;
}

#category {
    font-size: 35px;
}

#cart {
    background-color: white;
    border: 2px solid #8028d8;
    color: #8028d8;
    font-family: Segoe Script;
    font-weight: bolder;
    border-radius: 8px;
    font-stretch: narrower;
    font-size: 16px;
    width: 50%;
    height: 40px;
    margin-left: 100px;
    margin-top: 20px;
}

#app {
    /* display: flex; */
    width: 100%;
    /* height: 100vh; */
    justify-content: center;
    align-items: center;
    font-size: 15px;
}

input {
    border: 0;
    width: 8.5rem;
    text-align: center;
    padding: 0 0.5rem;
    height: 35px;
    border: 2px solid black;
    color: black;
}

button {
    border: 2px solid black;
    padding: 0.5rem;
    background: #f5f5f5;
    color: black;
    font-size: 1 rem, bold;
    cursor: pointer;
    width: 10%;
    height: 35px;
}

#gallery {
    display: block;
    box-shadow: 0 0px 1px 0 rgb(214, 195, 247), 0 0px 2px 0 rgb(214, 195, 247);
}

#gallery img {
    border: 1px solid #8028d8;
}

#gallery:hover {
    box-shadow: 0 0px 1px 0 rgb(128, 40, 216), 0 0px 9px 0 rgb(128, 40, 216);
    -ms-transform: scale(1.05);
    /* IE 9 */
    -webkit-transform: scale(1.05);
    /* Safari 3-8 */
    transform: scale(1.05);
}
</style>
