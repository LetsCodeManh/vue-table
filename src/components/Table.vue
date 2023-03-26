<script lang="ts">
type Brewery = {
  name: string;
  brewery_type: string;
  phone: string;
  website_url: string;
};

export default {
  data() {
    return {
      listItem: [] as Brewery[],
      sortField: "name",
      sortDirection: "asc",
      selectedBreweryType: "all",
      breweryTypes: [
        "micro",
        "nano",
        "regional",
        "brewpub",
        "large",
        "planning",
        "bar",
        "contract",
        "proprietor",
        "closed",
      ],
      perPage: 5,
      currentPage: 1,
    };
  },
  methods: {
    async getBreweries() {
      let url: string = "https://api.openbrewerydb.org/breweries";
      if (this.selectedBreweryType !== "all") {
        url += `?by_type=${this.selectedBreweryType}`;
        url += `&page=${this.currentPage}&per_page=${this.perPage}`;
      } else {
        url += `?page=${this.currentPage}&per_page=${this.perPage}`;
      }
      const response = await fetch(url);
      const finalRes = await response.json();
      this.listItem = finalRes;
    },
    sortList(field: string) {
      if (field === this.sortField) {
        this.sortDirection = this.sortDirection === "asc" ? "desc" : "asc";
      } else {
        this.sortField = field;
        this.sortDirection = "asc";
      }

      this.listItem.sort((a: any, b: any) => {
        if (this.sortDirection === "asc") {
          return a[this.sortField].localeCompare(b[this.sortField]);
        } else {
          return b[this.sortField].localeCompare(a[this.sortField]);
        }
      });
    },
    nextPage() {
      this.currentPage++;
      this.getBreweries();
    },
    prevPage() {
      this.currentPage--;
      this.getBreweries();
    },
  },

  async mounted() {
    await this.getBreweries();
  },
  watch: {
    selectedBreweryType: async function () {
      await this.getBreweries();
    },
  },
};
</script>

<template>
  <div class="pb-5 d-flex align-center" style="gap: 1rem">
    <label for="brewery-type-select">Select brewery type: </label>
    <select
      id="brewery-type-select"
      v-model="selectedBreweryType"
      class="text-white pa-2 border text-center"
    >
      <option value="all">All</option>
      <option v-for="type in breweryTypes" :value="type">{{ type }}</option>
    </select>
  </div>

  <VTable class="bg-grey-darken-4 text-white">
    <thead>
      <tr>
        <th
          @click="sortList('name')"
          style="cursor: pointer"
          class="text-white"
        >
          Name &#8597;
        </th>
        <th class="text-white">URL</th>
        <th class="text-white">Type</th>
        <th class="text-white">Phone</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in listItem">
        <td>{{ item.name }}</td>
        <td>
          <a
            :href="item.website_url"
            target="_blank"
            rel="noopener noreferrer"
            class="text-white"
            >{{ item.website_url }}</a
          >
        </td>
        <td>{{ item.brewery_type }}</td>
        <td>{{ item.phone }}</td>
      </tr>
    </tbody>
  </VTable>
  <div class="d-flex justify-space-between align-center pt-10">
    <div class="d-flex justify-center" style="gap: 1rem">
      <div @click="prevPage" v-if="currentPage > 1">&#8592;</div>
      <div>{{ currentPage }}</div>
      <div @click="nextPage" v-if="listItem.length === perPage">&#8594;</div>
    </div>
    <div>
      <label for="items-per-page-input">Items per page: </label>
      <input
        id="items-per-page-input"
        type="number"
        min="1"
        max="200"
        v-model="perPage"
        class="text-white border text-center"
        @change="getBreweries()"
      />
    </div>
  </div>
</template>

<!-- 
  Tasks
    1.  Table by using Vuetify - check
    2.  Get Data from this API: https://api.openbrewerydb.org/breweries
    3.  Show some of the Data in the Table - Important show the website_url as a link with the target of _blank - check
    4.  Only show 5 results per page - check
    5.  Getting more result by scrolling through Pagination - check
    6.  Will be sorted by "by_dist" - check
    7.  Get a list of by_type to choose from and display the data - check
    8.  Filter with phone
    9.  the date should be in this format dd.mm.YYYY - cant do because no date exits
-->
