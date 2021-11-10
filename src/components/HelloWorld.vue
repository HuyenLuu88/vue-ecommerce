<template>
  <div class="m-3">
    <div class="text-left h4">
      Inventory
    </div>
    <div class="mt-4">
      <b-row>
        <b-col xl="3" lg="3" md="3" sm="12">
          <b-form-group
                  label=""
                  label-for="filter-input"
                  label-align-sm="right"
                  label-size="sm"
                  class="mb-0"
          >
            <b-input-group size="sm" >
              <b-form-input
                      id="filter-input"
                      v-model="filter"
                      placeholder="Search..."
                      class="mb-4"
              ></b-form-input>
            </b-input-group>
          </b-form-group>
        </b-col>
      </b-row>
      <b-table
              responsive
              striped hover
              :items="items"
              :fields="fields"
              :current-page="currentPage"
              :per-page="perPage"
              :filter="filter"
              :filter-included-fields="filterOn"
              :sort-by.sync="sortBy"
              :sort-desc.sync="sortDesc"
              :sort-direction="sortDirection"
              class="text-center custom-table"
              show-empty
              small
      >
        <template #cell(product)="row">
          <span class="text-success">
            {{row.item.product}}
          </span>
        </template>
        <template #cell(updated)="row">
          <span class="">
            {{row.item.updated.split(' ')[0]}}<br>
            {{row.item.updated.split(' ')[1]}}
          </span>
        </template>
        <template #cell(quantity)="row">
            <b-input-group size="sm" prepend='qty'>
                <b-form-input
                        type="number"
                        :value="row.item.quantity"
                        v-on:change="quantityChange(row.item.no, $event)"
                ></b-form-input>
            </b-input-group>
        </template>
      </b-table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      items: [],
      fields: [
        {key: 'code', label: 'Item Code'},
        {key: 'product', label: 'Product', sortable: true, sortDirection: 'desc'},
        {key: 'package', label: 'Package', sortable: true, sortDirection: 'desc'},
        {key: 'units', label: 'Available units', sortable: true, sortDirection: 'desc'},
        {key: 'category', label: 'Category', sortable: true, sortDirection: 'desc'},
        {key: 'updated', label: 'Last Updated', sortable: true, sortDirection: 'desc'},
        {key: 'quantity', label: 'Edit available quantity'},
      ],
      totalRows: 1,
      currentPage: 1,
      perPage: 25,
      pageOptions: [25, 50, 100],
      sortBy: '',
      sortDesc: false,
      sortDirection: 'asc',
      filter: null,
      filterOn: [],
    }
  },
  mounted() {
    this.items = [
      {no: 1, code: 'ACC1', product: 'Apple granny smith', package: '40 LB', units: '3638066', category: 'Fruits', updated: '2021-02-05 08:28:36', quantity: '3638066'},
      {no: 2, code: 'ACC1', product: 'Pineapple crownless', package: '7 CT', units: '309434', category: 'Fruits', updated: '2021-02-03 02:28:36', quantity: '3638066'},
      {no: 3, code: 'ACC1', product: 'Banana green', package: '8 CT', units: '364368066', category: 'Fruits', updated: '2021-02-09 08:28:36', quantity: '3638066'},
      {no: 4, code: 'ACC1', product: 'Banana green tip', package: '40 LB', units: '85638066', category: 'Fruits', updated: '2021-02-25 08:28:36', quantity: '3638066'}
    ]
  },
  methods: {
    quantityChange(no, value) {
      this.items.map(item => {
        if (item.no === no) {
          item.quantity = value;
        }
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.custom-table td {
  vertical-align: inherit!important;
}
</style>
