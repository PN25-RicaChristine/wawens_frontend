<template>
<div class="container">
    <h1>WAWEN'S UBE HALAYA : Cart</h1>
    <div class="empty" v-if="selectedProducts.length == 0">
        <i class="fa fa-shopping-cart" style="color: #8028d8"></i>
        <span class="description"><b>Your Cart Is Empty!</b></span>
        <span style="font-size: 15px;">Start adding your UBEfavorites.</span>
    </div>
    <form @submit.prevent="submit()" method="get" v-if="selectedProducts.length > 0">
        <hr>
        <div class="row">
            <div class="column" style="border-right-color: #e5b1fd;border-style: solid;border-width: thin;border-left-color: white;border-top-color: white;border-bottom-color: white;">
                <h2>Selected Products</h2>
                <div v-for="(item, index) in selectedProducts" :key="index">
                    <div class="selected-item">
                        <div class="column1" style="width:40%">
                            <img :src="item.image">
                        </div>
                        <div class="column1" style="width:50%;margin-left:5%;">
                            <h2>{{item.name}}</h2>
                            <h4>Price: &#x20B1; {{item.price}} / {{item.unit}}</h4>
                            <span id="quantity">
                                <button type="button" @click="decrement(item)">&mdash;</button>
                                <input type="text" :value="item.sub_quantity" disabled>
                                <button type="button" @click="increment(item)">&#xff0b;</button>
                            </span>
                            <br>
                            <button style="margin-top:5px;background-color:#cca4f5;color:white;" type="button" class="btn" @click="remove(item)">Remove</button>
                        </div>
                    </div>
                </div>
            </div>
            <div class="column" style="border-right-color: white;border-style: solid;border-width: thin;border-left-color: #e5b1fd;border-top-color: white;border-bottom-color: white;">
                <div style="margin-left:10px;">
                    <h2>Delivery Details</h2>
                    <div class="form-row">
                        <div class="form-group col-md-6">
                            <label>
                                <i style="color:red;">*</i>Preferred Delivery Date:
                            </label>
                            <input type="date" class="form-control" :min="now" v-model="order.date" required>
                        </div>
                        <div class="form-group col-md-6">
                            <label>
                                <i style="color:red;">*</i>Preferred Delivery Time:
                            </label>
                            <select style=" height: 30px;" v-model="order.time" class="form-control" placeholder="---select---" required>
                                <option>8 AM - 12 PM</option>
                                <option>1 PM - 5 PM</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-row">
                        <div class="form-group col-md-6">
                            <label>
                                <i style="color:red;">*</i>Payment Option:
                            </label>
                            <select style=" height: 30px;" v-model="order.payment" class="form-control" placeholder="---select---" required>
                                <option>COD (Cash on Delivery)</option>
                                <option>PayMaya</option>
                                <option>GCash</option>
                                <option>BDO</option>
                                <option>BPI</option>
                            </select>

                        </div>
                        <div class="form-group col-md-6">
                            <label>
                                <i style="color:red;">*</i>Active Contact Number:
                            </label>
                            <input v-model="order.contact" type="tel" pattern="^(09|\+639)\d{9}$" class="form-control" placeholder="+639xxxxxxxxx or 09xxxxxxxxx" required>

                        </div>
                    </div>
                    <div class="form-group">
                        <label>
                            <i style="color:red;">*</i>Receiver's Complete Name:
                        </label>
                        <input type="text" class="form-control" v-model="order.receiver" required>

                    </div>
                    <div class="form-group">
                        <label>
                            <i style="color:red;">*</i>Complete Name Delivery Address:
                        </label>
                        <div class="form-row" style="margin-bottom:3px;">
                            <div class="col">
                                <input type="text" class="form-control" v-model="address.company" placeholder="Company(Optional)">
                            </div>
                            <div class="col">
                                <input type="text" class="form-control" v-model="address.building" placeholder="Apartment, building, etc.(Optional)">
                            </div>
                        </div>
                        <div class="form-row" style="margin-bottom:3px;">
                            <div class="col">
                                <input type="text" class="form-control" v-model="address.brgy" placeholder="Sitio,Road,Barangay" required>

                            </div>
                            <div class="col">
                                <input type="text" class="form-control" v-model="address.municipality" placeholder="Municipality" required>

                            </div>
                        </div>
                        <div class="form-row">
                            <div class="col">
                                <input type="text" class="form-control" v-model="address.city" placeholder="City" required>

                            </div>
                            <div class="col">
                                <input type="text" class="form-control" v-model="province" placeholder="Province" required>
                            </div>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>Message/Delivery Instructions(Optional):</label>
                        <textarea class="form-control" v-model="order.message" rows="5"></textarea>
                    </div>
                    <div class="form-row" style="font-size:30px;font-weight:bold;">
                        <div class="form-group col-md-6">
                            <label>TOTAL:
                            </label>
                        </div>
                        <div class="form-group col-md-6" style="text-align:right;">
                            <label>
                                &#x20B1; {{order.total}}
                            </label>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <input id="submit" class="btn btn-primary btn-lg" type="submit" value="Continue to Submit Order">
    </form>
</div>
</template>

<style scoped>
.container {
    margin-top: 80px;
    width: 90%;
    margin-left: 5%;
    margin-right: 5%;
}

h1 {
    color: #8028d8;
    font-family: Segoe Print;
    font-weight: bolder;
    text-align: center;
    padding-bottom: 2%;
}

h2 {
    color: #8028d8;
    font-family: Segoe Print;
    font-weight: bold;
}

hr {
    width: 100%;
    background-color: #e5b1fd;
    display: block;
    height: 1px;
    border-style: inset;
    border-width: 1px;
}

.column,
.column1 {
    float: left;
    width: 50%;
    height: auto;
}

.row:after {
    content: "";
    display: table;
    clear: both;
}

.selected-item {
    width: 100%;
    height: 150px;
    margin-top: 10px;
}

.selected-item img {
    width: 100%;
    height: 150px;
    border: 1px solid #e5b1fd;
    border-radius: 2px;
    padding: 3px;
}

#quantity button {
    text-align: center;
    border: 1px solid #808080;
    color: white;
    background-color: #808080;
    width: 35px;
    font-weight: bolder;
    font-size: 16px;
}

#quantity input {
    text-align: center;
    width: 100px;
    color: black;
    font-size: 15px;
    border: 2px solid #808080;
}

#submit {
    float: right;
    color: #8028d8;
    border-radius: 10px;
    border: 2px solid #8028d8;
    background-color: #e5b1fd;
    font-weight: bolder;
    height: 40px;
    font-size: 15px;
    margin-top: 50px;
    margin-bottom: 50px;
}

.form-group input,
.form-group textarea,
.form-group select {
    border: 1px solid #e5b1fd;
    font-size: 13px;
}

.form-group input {
    height: 30px;
}

.form-group label {
    font-weight: bolder;
    font-size: 16px;
}

.form-group option {
    background-color: #f0e6ff;
    font-size: 13px;
}

#brgy,
#municipality {
    display: none;
}

.empty {
    width: 100%;
    margin-bottom: 25px;
    float: left;
    min-height: 450px;
    overflow-y: hidden;
    text-align: center;
    border: solid 2px #e5b1fd;
}

.empty i {
    font-size: 100px;
    padding-top: 150px;
}

.empty span {
    width: 100%;
    float: left;
}

.empty .description {
    font-size: 24px;
}
</style>

<script>
import ROUTER from "@/router";
export default {
    mounted() {
        this.retrieve();
        this.today()
    },
    data() {
        return {
            now: null,
            address: {
                company: '', //optional
                building: '', //optional
                brgy: '',
                municipality: '',
                city: '',
            },
            province: '',
            order: {
                date: null,
                time: null,
                payment: null,
                contact: null,
                receiver: null,
                address: '',
                message: null, //optional
                products: [],
                total: 0.00
            },
            selectedProducts: []

        };
    },
    computed: {
        // total() {
        //     var total = 0
        //     if (localStorage.getItem('orders')) {
        //         JSON.parse(localStorage.getItem('orders')).products.forEach(item => {
        //             total += (item.quantity * item.price)
        //         });
        //     }
        //     return total
        // }
    },
    methods: {
        itemTotal() {
            for (let i = 0, l = this.selectedProducts.length; i < l; i++) {
                this.order.total += (this.selectedProducts[i].price * this.selectedProducts[i].sub_quantity)
            }
        },
        submit() {
            for (var add in this.address) {
                if (this.address[add] != '') {
                    this.address[add] += ','
                }
            }
            this.order.address = this.address.company + this.address.building + this.address.brgy + this.address.municipality + this.address.city + this.province
            this.order.products = this.selectedProducts
            localStorage.setItem('orders', JSON.stringify(this.order))
            console.log(this.order.address)
            ROUTER.push("/submit_order");
        },
        increment(item) {
            let price = item.price
            let prev = item.sub_quantity
            item.sub_quantity++;
            let inc = item.sub_quantity - prev
            let addon = price * inc
            this.order.total += addon
            localStorage.setItem('carts', JSON.stringify(this.selectedProducts))
        },
        decrement(item) {
            let price = item.price
            let prev = item.sub_quantity
            if (item.sub_quantity === 1) {
                item.sub_quantity = 1;
            } else {
                item.sub_quantity--;
            }
            let dec = prev - item.sub_quantity
            let deduct = price * dec
            this.order.total -= deduct
            localStorage.setItem('carts', JSON.stringify(this.selectedProducts))
        },
        remove(item) {
            let deduct = item.price * item.sub_quantity
            this.order.total -= deduct
            let index = this.selectedProducts.indexOf(item);
            this.selectedProducts.splice(index, 1);
            localStorage.setItem('carts', JSON.stringify(this.selectedProducts))
        },
        retrieve() {
            //this is where api from carts should be
            this.selectedProducts = JSON.parse(localStorage.getItem('carts'));
            this.itemTotal()
        },
        today() {
            var today = new Date();
            var dd = today.getDate();
            var mm = today.getMonth() + 1;
            var yyyy = today.getFullYear();
            if (dd < 10) {
                dd = '0' + dd;
            }
            if (mm < 10) {
                mm = '0' + mm;
            }
            today = yyyy + '-' + mm + '-' + dd;
            this.now = today
        }
    }
};
</script>
