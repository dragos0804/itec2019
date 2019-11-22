<template>
<div>
  <div v-for="product in products" :key="product">
  <b-card
    :title="product.name"
    img-src="https://picsum.photos/600/300/?image=25"
    img-alt="Image"
    img-top
    tag="article"
    style="max-width: 20rem;"
    class="mb-2"
  >
    <b-card-text>
      unitPrice: <br\>
      Category
    </b-card-text>

    <b-button href="#" variant="primary">Go somewhere</b-button>
  </b-card>
</div>
</div>
</template>

<script>
export default {
    data () {
        return {
            products: [
                {
                    name: 'gigi',
                    unit: '',
                    unitPrice: '',
                    category: '',
                    subcategory: ''
                },
                {
                    name: 'boaba',
                    unit: '',
                    unitPrice: '',
                    category: '',
                    subcategory: ''
                }
            ]
        }
    }
}
</script>