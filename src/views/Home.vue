<template>
  <div id="app" class="app">
    <h1>{{ restaurantName }}</h1>
    <p class="description">
      Bienvenue dans notre café {{ restaurantName }}! Nous sommes réputés pour
      notre pain et nos merveilleuses pâtisseries. Faites vous plaisir dès le
      matin ou avec un goûter réconfortant. Mais attention, vous verrez qu'il
      est difficile de s'arrêter.
    </p>

    <section class="menu">
      <h2>Menu</h2>
      <MenuItem
          v-for="item in simpleMenu"
          @add-items-to-cart="addToShoppingCart"
          :name="item.name"
          :image="item.image"
          :price="item.price"
          v-model:quantity="item.quantity"
          :inStock="item.inStock"
          :key="item.name"
      />
    </section>

    <aside class="shopping-cart">
      <h2>Panier : {{ shoppingCart }} articles</h2>
    </aside>

    <footer class="footer">
      <p>{{ copyright }}</p>
    </footer>
  </div>
</template>

<script>
import MenuItem from "../components/MenuItem"
import { mapState, mapGetters} from "vuex"
export default {
  name: "Home",
  components: {
    MenuItem
  },
  computed: {
    ...mapState({
      restaurantName: "restaurantName",
      shoppingCart: "shoppingCart",
      simpleMenu: "simpleMenu"
    }),
    ...mapGetters({
      copyright: "copyright"
    }),
  },
  methods: {
    addToShoppingCart(amount) {
      this.shoppingCart += amount
    }
  }
}
</script>

<style>
  .description {
    max-width: 960px;
    font-size: 1.2rem;
    margin: 0 auto;
  }

  .footer {
    text-align: center;
    font-style: italic;
  }

  .menu {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .shopping-cart {
    position: absolute;
    right: 30px;
    top: 0;
  }
</style>
