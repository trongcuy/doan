<template>
  <div class="customer">
    <div class="customer__title">
      Thông tin khách hàng
    </div>
    <div class="customer__content">
      <empty-customer
        v-if="!hasCustomer"
        @selectCustomer="selectCustomer"
      />
      <customer-selected
        v-else
        :customer="customer"
        @removeCustomer="removeCustomer"
      />
    </div>
  </div>
</template>

<script>
import EmptyCustomer from './components/empty-customer.vue'
import CustomerSelected from './components/customer-selected.vue'
import { computed, ref, watch } from 'vue'
import { useStore } from 'vuex'
const MODULE_NAME = 'order'

export default {
  components: { EmptyCustomer, CustomerSelected },
  setup () {
    const store = useStore()
    const customer = ref(null)
    const hasCustomer = computed(() => customer.value)
    const order = computed(() => store.state[MODULE_NAME].order)
    const selectCustomer = value => {
      customer.value = value
      order.value.customer = value.customerId
    }

    const removeCustomer = () => {
      customer.value = null
      order.value.customer = null
    }
    return {
      hasCustomer,
      customer,
      selectCustomer,
      removeCustomer
    }
  }
}
</script>

<style lang="scss" scoped>
.customer {
   background: #fff;
   padding: 24px;
   display: flex;
   flex-direction: column;
   height: 280px;

   &__title {
     margin-bottom: 12px;
     font-weight: 500;

   }

   &__content {
     flex: 1;
   }
}

</style>
