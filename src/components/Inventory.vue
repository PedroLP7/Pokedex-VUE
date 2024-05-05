<template>
  <div>
    <h1 class="text-center">MY INVENTORY</h1>

    <div class="container">
      <div class="row">
        <Item v-for="(item, index) in items1" :key="index" :item="item" />
        <button class="btn btn-primary" @click="showModal()">SHOP</button>
      </div>
    </div>

    <!-- <button class="btn btn-primary" @click="showModal()">SHOP</button> -->
    <div class="modal" tabindex="-1" id="shopModal">
      <div class="modal-dialog custom-modal">
        <div class="modal-content  " id="alert-danger-delete">
          <div class="modal-body">
            <Shop @buy="updateItems" />
            
          </div>
          <div class="modal-footer" id="alert-danger-delete-footer">
            <button
              type="button"
              class="btn btn-secondary"
              id="alert-danger-delete-cancel"
              data-bs-dismiss="modal"
            >
              Cerrar
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- <Shop @buy="updateItems" /> -->
  </div>
</template>
<script>
import Shop from "./Shop.vue";
import axios from "axios";
import Item from "./Item.vue";
import * as bootstrap from "bootstrap";

export default {
  name: "Inventory",
  components: {
    Shop,
    Item,
  },
  methods: {
    changeOneItem() {
      const item = this.items1.find((i) => i.id === 1);
      if (item) {
        item.quantity += 5;
      }
    },
    showModal() {
      this.myModal = new bootstrap.Modal("#shopModal");
      this.myModal.show();
    },
    updateItems(data) {
      if (data) {
        const { id, desiredQuantity } = data;
        const itemToUpdate = this.items1.find((item) => item.id === id);
        if (itemToUpdate) {
          const totalQuantity = itemToUpdate.quantity + desiredQuantity;

          if (totalQuantity > itemToUpdate.maxQuantity) {
            const excessQuantity = totalQuantity - itemToUpdate.maxQuantity;
            itemToUpdate.quantity = itemToUpdate.maxQuantity;
            console.log(`La cantidad excede el límite en ${excessQuantity}.`);
          } else {
            itemToUpdate.quantity += desiredQuantity;
          }
        }
      }
    },
    getItems() {
      let firstItem = 1;
      let lastItem = 50;
      let desiredItems = [1, 2, 4, 17, 23, 29, 40, 46, 50, 51, 77];

      for (let i = firstItem; i <= lastItem; i++) {
        axios
          .get(`https://pokeapi.co/api/v2/item/${i}`)
          .then((response) => {
            if (desiredItems.includes(i)) {
              response.data.quantity = 0;

              switch (i) {
                case 1:
                case 2:
                case 4:
                  response.data.maxQuantity = 15;

                  break;

                case 17:
                case 23:
                case 29:
                case 40:
                case 46:
                case 50:
                case 51:
                case 77:
                  response.data.maxQuantity = 5;

                  break;
              }

              this.items1.push(response.data);
              // console.log(this.items1)
            }
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  },

  data() {
    return {
      items1: [],
    };
  },
  mounted() {
    this.getItems();
  },
};
</script>
<style>
.custom-modal {
    max-width: 50%; /* Ancho máximo personalizado */
   
  
}





</style>
