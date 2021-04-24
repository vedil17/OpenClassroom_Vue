<template>
  <div class="menu-item">
    <img class="menu-item__image" :src="image.source" :alt="image.alt"/>
    <div>
      <h3>{{ name }}</h3>
      <p>Prix : {{ generatedPrice }}</p>
      <p v-if="inStock">En stock</p>
      <p v-else>En rupture de stock</p>
      <div>
        <label for="add-item-quantity">Quantité : {{ quantity_data }}</label>
        <input v-model.number="quantity_data" id="add-item-quantity" type="number"/>
        <BaseButton @click="updateShoppingCart(quantity_data)">
          Ajouter au panier d'achat
        </BaseButton>
      </div>
    </div>
  </div>
</template>

<script>
import BaseButton from "@/components/BaseButton";
import { mapActions } from "vuex"

export default {
  name: "MenuItem",
  components: {
    BaseButton
  },
  props: {
    image: {
      type: Object,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    quantity: {
      type: Number,
      default: 1
    },
    price: {
      type: Number,
      required: true
    },
    inStock: {
      type: Boolean,
      required: true
    }
  },
  data () {
    return {
      onsale: false,
      quantity_data: this.$props.quantity
    }
  },
  computed: {
    generatedPrice () {
      if (this.onsale) {
        return (this.price*0.9).toFixed(2)
      } else {
        return this.price
      }
    }
  },
  beforeMount() {
    const today = new Date().getDate()

    if (today % 2 === 0) {
      this.onsale = true
    }
  },
  methods: {
    ...mapActions(["updateShoppingCart"])
  }
}
</script>

<style>
  .menu-item {
    display: flex;
    width: 500px;
    justify-content: space-between;
    margin-bottom: 30px;
  }

  .menu-item__image {
    max-width: 300px;
  }
</style>
