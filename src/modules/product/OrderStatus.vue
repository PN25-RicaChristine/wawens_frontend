<template>
<div class="container">
    <h1>ORDER STATUS</h1>
    <i><i style="color:red;">*</i>Only pending and confirmed orders will appear here, once your order is marked complete or cancelled it will no longer appear here.</i>
    <br><i><i style="color:red;">*</i>CANCEL or UPDATE on orders can only be done when order is still pending.</i>
    <!-- <div class="empty" v-if="orderSubmitted.length == 0">
        <i class="fa fa-tasks" style="color: #8028d8"></i>
        <span class="description"><b>NO ORDERS HAVE BEEN RECORDED</b></span>
        <span style="font-size: 15px;">Start ordering your UBEfavorites.</span>
    </div> -->
    <div class="transaction">
        <div class="row" id="header">
            <div class="col-sm-3">DATE AND TIME ORDERED:</div>
            <div class="col-sm-4" id="value">value</div>
            <div class="col-sm-2">ORDER NO:</div>
            <div class="col-sm-3" id="value">value</div>
            <div class="w-100"></div>
            <div class="col-sm-3">STATUS:</div>
            <div class="col-sm-4" id="value">value</div>
            <div class="col-sm-2">LABEL:</div>
            <div class="col-sm-3" id="value">value</div>
            <div class="w-100"></div>
            <div class="col-sm-1">REMARKS:</div>
            <div class="col-sm-11" id="remarks"><span class="form-control" style="height:50px;overflow: auto;"></span></div>
        </div>
    </div>
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

i {
    font-size: 15px;
}

.empty {
    width: 100%;
    margin-top: 25px;
    margin-bottom: 25px;
    float: left;
    min-height: 450px;
    text-align: center;
    border: solid 2px rgb(127, 127, 127);
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

.transaction {
    width: 100%;
    margin-top: 25px;
    margin-bottom: 25px;
    float: left;
    /* height: auto; */
    min-height: 450px;
    text-align: center;
    border: solid 2px #e5b1fd;
}

#header {
    text-align: left;
    width: 96%;
    margin-left: 2%;
    margin-right: 2%;
    margin-top: 1%;
    font-size: 16px;
    float: center;
    color: #8028d8;
    font-family: Segoe Print;
    font-weight: bolder;
}

#value {
    color: black;
    font-family: Arial;
    font-weight: normal;
}

#remarks span{
    border: 1px solid #e5b1fd;
}
</style>

<script>
export default {
    data() {
        return {
            orderSubmitted: []
        }
    }
}
</script>
