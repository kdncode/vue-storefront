<template>
  <div id="category">
    <header class="bg-lightgray py35 pl20">
        <div class="container">
            <breadcrumbs :routes="breadcrumbs.routes" :active-route="category.name" />
            <h1 class="mb10"> {{ category.name }} </h1> 
        </div>
        <button class="mobile-filters-button bg-black brdr-none c-white" @click="openFilters">ADD FILTERS</button>
    </header>
    <div class="container pb60">
        <div class="row pt15 pl20 center-md">
            <div class="col-md-3 start-xs category-filters">
                <sidebar :filters="filters"/>
            </div>
            <div class="col-md-3 start-xs mobile-filters" v-if="mobileFilters">
                <div class="close-container">
                    <i class="material-icons p15 close c-black" @click="closeFilters">close</i>
                </div>
                <sidebar class="mobile-filters-body" :filters="filters"/>
            </div>
            <div class="col-md-9 pt20 products-list">
                <div v-if="isCategoryEmpty">
                    No products found!
                </div>
                <product-listing columns="3" :products="products" />
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import { corePage } from 'lib/themes'

import Sidebar from '../components/core/blocks/Category/Sidebar.vue'
import ProductListing from '../components/core/ProductListing.vue'
import Breadcrumbs from '../components/core/Breadcrumbs.vue'

export default {
  components: {
    ProductListing,
    Breadcrumbs,
    Sidebar
  },
  data () {
    return {
      mobileFilters: false
    }
  },
  methods: {
    openFilters () {
      this.mobileFilters = true
    },
    closeFilters () {
      this.mobileFilters = false
    }
  },
  mixins: [corePage('Category')]
}
</script>

<style lang="scss" scoped>

    .category-filters {
        width: 242px;
    }

    .mobile-filters {
        display: none;
        overflow: auto;
    }

    .mobile-filters-button {
        margin-top: 25px;
        padding: 15px;
        display: none;
    }

    @media (max-width: 64em) {
        .products-list {
            max-width: 530px;
        }
    }

    @media (max-width: 770px) {

        .products-list {
            width: 100%;
            max-width: none;
        }

        .mobile-filters {
            display: block;
        }

        .mobile-filters-button {
            display: block;
        }

        .category-filters {
            display: none;
        }

        .product-listing {
            justify-content: center;;
        }

        .mobile-filters {
            position: fixed;
            background-color: #F2F2F2;
            z-index: 5;
            padding: 0 40px;
            left: 0;
            width: 100vw;
            height: calc(100vh - 56px);
            top: 56px;
            box-sizing: border-box;
        }

        .mobile-filters-body {
            padding-top: 50px;
        }
    }

    .close-container {
        width: 100%;
        position: absolute;
        left: 0;
    }

    .close {
        margin-left: auto;
    }

</style>
