<template>
    <section class="h-100 flex flex-column items-center overflow-auto">
        <div class="h2 w-70 mv4">
          <GoBackArrow/>
        </div>
        <template v-if="cart.length">
          <CartItem v-for="(item, index) in cart" :key="index" :product="item" @on-close="deleteCartItem"/>
        </template>
        <div v-else>
          <h1 class="silver">No hay elementos añadidos al carrito.</h1>
        </div>
        <div class="w-70 mv3 flex justify-end">
            <p class="text-conservas f2 b">Total: <span class="text-conservas-header f1 normal">${{ $store.getters.totalPrice ? $store.getters.totalPrice : 0 }}</span></p>
            <div class="flex items-center">
                <Button class="f3 mh3">Comprar!</Button>
            </div>
        </div>
    </section>
</template>

<script>
import { mapGetters } from 'vuex'
import CartItem from '../../components/UI/CartItem'
import GoBackArrow from '../../components/UI/GoBackArrow'
import Button from '../../components/UI/Button'

export default {
  components: {
    CartItem,
    GoBackArrow,
    Button
  },
  methods: {
    deleteCartItem (id) {
      this.$store.dispatch('deleteFromCart', id)
    }
  },
  computed: {
    ...mapGetters(['cart'])
  }
}
</script>
