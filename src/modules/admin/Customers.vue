<template>
<sidebar>
  <div>
    <sidebar>
      <div>
        <p
          style="color: purple;font-weight: bold;font-family: Segoe Script;font-style: italic;font-size: 20px;margin-top: 1%;"
        >Customer's Management</p>
      </div>
      <table
        class="table table-purple"
        style="font-size: 15px;-align: center;margin-bottom: 1rem;width: 40%;"
      >
        <thead>
          <tr>
            <th
              scope="col"
              style="padding: 8px;color: white;background-color: blueviolet;width: 10%;border: 2px solid violet;"
            >SORT</th>
            <th class="dropdown" style="background-color: violet;color:purple;">
              <a
                data-toggle="dropdown"
                class="dropdown-toggle"
                aria-haspopup="true"
                aria-expanded="false"
              >Total Orders</a>
              <ul class="dropdown-menu">
                <li>
                  <a class="dropdown-item">Completed Orders</a>
                  <a class="dropdown-item">Cancelled Orders</a>
                  <a class="dropdown-item">Best Buyers</a>
                </li>
              </ul>
            </th>
          </tr>
        </thead>
      </table>
      <b-form-input class="searchbar" placeholder="Search here..."></b-form-input>
      <div>
        <b-table :items="items" :fields="fields">
          <template v-slot:cell(ACTIONS)="row">
            <i
              @click="row.toggleDetails"
              class="fa fa-eye"
              data-toggle="modal"
              data-target="#ViewHistory"
              style="font-size:20px;"
              aria-hidden="true"
            ></i>
          </template>
        </b-table>
        <!-- History Modal -->
        <div
          class="modal fade bd-example-modal-lg"
          id="ViewHistory"
          tabindex="-1"
          role="dialog"
          aria-labelledby="CustomerHistoryModal"
          aria-hidden="true"
        >
          <div class="modal-dialog modal-lg" role="document">
            <div class="modal-content">
              <div class="modal-header" style="background-color: violet;">
                <h5
                  class="modal-title"
                  style="margin-left: 26%;font-size: 20px;"
                >CUSTOMER TRANSACTION HISTORY</h5>
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>
              <div class="modal-body">
                <button
                  type="button"
                  class="btn btn-primary"
                  style=" width: 15%;color: red;font-weight: bold;float: right;background-color: violet;"
                >CLOSE</button>
              </div>
            </div>
          </div>
        </div>
        <!-- History Modal End -->
      </div>
    </sidebar>
  </div>
</sidebar>
</template>
<script>
import sidebar from "../../components/frame/sidebar";
export default {
  components: {
    sidebar
  },
  data() {
    return {
      fields: [
        "USERNAME",
        "TOTAL_ORDERS",
        "COMPLETED_ORDERS",
        " CANCELLED_ORDERS",
        "ACTIONS"
      ],
      items: [
        {
          USERNAME: "mingming",
          TOTAL_ORDERS: "",
          COMPLETED_ORDERS: "",
          CANCELLED_ORDERS: ""
          // ACTIONS: ""
        },
        {
          USERNAME: "mingming",
          TOTAL_ORDERS: "",
          COMPLETED_ORDERS: "",
          CANCELLED_ORDERS: ""
          // ACTIONS: ""
        }
      ]
      //       $(function(){
      //    $(".dropdown-menu").on('click', 'a', function(){
      //        $(this).parents('.dropdown').find('button').text($(this).text());
      //    });
      // });
    };
  }
};
</script>
<style scoped>
.dropdown-toggle {
  cursor: pointer;
}
a {
  color: purple;
  text-decoration: none;
  background-color: transparent;
}
.a:hover {
  color: purple;
  text-decoration: none;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  display: none;
  width: 100%;
  font-size: 1.5rem;
  color: purple;
  text-align: center;
  list-style: none;
  background-color: violet;
  margin-left: -35%;
  margin-top: 3.5%;
}
.dropdown-menu:hover {
  cursor: pointer;
  background-color: violet;
}
table,
tr,
th,
tbody {
  border: 2px solid violet;
  text-align: center;
  vertical-align: bottom;
  border-bottom: 2px solid violet;
}
.form-control {
  width: 60%;
  height: calc(1.5em + 0.75rem + 2px);
  padding: 0.375rem 0.75rem;
  font-size: 20px;
  color: violet;
  background-color: #fff;
  background-clip: padding-box;
  border: 2px solid violet;
  border-radius: 0.25rem;
  float: right;
  margin-top: -5.3%;
}
.fa-eye:hover {
  cursor: pointer;
}
</style>
