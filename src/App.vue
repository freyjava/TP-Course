<!-- <template>
  <div>
    <MenuComponent
      v-for="menu in menus.filter((menu) => menu.id !== 2)"
      :key="menu.id"
      :textTitle="menu.textTitle"
      v-bind="menu"
      @groupSelected="updateCategoryGroup"
    />
  </div>

  <div class="row-1">
    <CategoryComponent
      v-for="category in categories"
      :key="category.id"
      :image="category.image"
      :name="category.name"
      :productCount="category.productCount"
      :color="category.color"
    />
  </div>
  <div class="row-2">
    <PromotionComponent
      v-for="promotion in promotions"
      :key="promotion.id"
      :color="promotion.color"
      :title="promotion.title"
      :image="promotion.image"
      :buttonColor="promotion.buttonColor"
    />
  </div>

  <div>
    <MenuComponent
      v-if="menus.find((menu) => menu.id === 2)"
      :key="menus.find((menu) => menu.id === 2).id"
      :textTitle="menus.find((menu) => menu.id === 2).textTitle"
      v-bind="menus.find((menu) => menu.id === 2)"
      @groupSelected="updateProductGroup"
    />
  </div>
  <div class="row-3">
    <ProductComponent
      v-for="product in productsByGroup"
      :key="product.id"
      :name="product.name"
      :rating="product.rating"
      :size="product.size"
      :images="product.image"
      :price="product.price"
      :promotionAsPercentage="product.promotionAsPercentage"
      :categoryId="product.categoryId"
      :instock="product.instock"
      :coundSold="product.countSold"
      :group="product.group"
    />
  </div>
  <RouterView></RouterView>
</template>

<script>
import CategoryComponent from "./components/CategoryComponent.vue";
import PromotionComponent from "./components/PromotionComponent.vue";
import ButtonComponent from "./components/ButtonComponent.vue";
import MenuComponent from "./components/MenuComponent.vue";
import ProductComponent from "./components/ProductComponent.vue";
import { useProductStore } from "./stores/Product";
import { mapState } from "pinia";

export default {
  setup() {
    const store = useProductStore();
    return {
      store
    }
  },
  components: {
    CategoryComponent,
    PromotionComponent,
    ButtonComponent,
    MenuComponent,
    ProductComponent,
  },

  data() {
    return {
      currentProductGroup: null, //For product filtering
      currentCategoryGroup:null, //For Category filtering

      menus: [
        {
          id: 1,
          textTitle: "Featured Categories",
        },
        {
          id: 2,
          textTitle: "Popular Component",
        },
      ],
    };
  },

  methods: {
    updateCategoryGroup(group){
      this.currentCategoryGroup = group || null;
    },

    updateProductGroup(group){
      this.currentProductGroup = group || null;
    }
  },

  async mounted() {
    await this.store.fetchCategories()
    await this.store.fetchPromotions()  
    await this.store.fetchProducts()
    await this.store.fetchGroups()
  }, 

  
  computed: {
    ...mapState(useProductStore, {
      promotions: "promotions",
      products: "products",
      groups: "groups",
      categories: "categories",

      meatProducts(store) { 
        // results from getter work fine
        return store.getMeatProducts
      },

      // categories(store) {
      //   const cats = store.getCategoriesByGroup(this.currentGroupName)
      //   console.log("Categories by group name")
      //   console.log(cats)
      //   return cats
      // },

      productsByGroup(store) {
        return store.getProductsByGroup()
      },

      popularProducts(store) {
        return store.getPopularProducts
      },

    
    }),

  },


};
</script>

<style>
.row-1,
.row-2,
.row-3 {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style> -->
<template>
  <RouterView></RouterView>
</template>