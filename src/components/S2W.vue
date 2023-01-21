<template>
  <v-container>
    <v-card>
      <v-tabs v-model="tab" color="blue" align-tabs="left">
        <v-tab :value="1" @click="changeTab">Normal</v-tab>
        <v-tab :value="2" @click="changeTab">Deluxe</v-tab>
      </v-tabs>
    </v-card>
    <v-row>
      <!-- S2W CATEGORIES -->
      <v-col cols="5">
        <v-card>
          <v-table fixed-header height="590px">
            <thead>
              <tr>
                <th class="text-left">Slice</th>
                <th class="text-left">Weighting</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="cat in currCategory" :key="cat.id">
                <!-- Make these selectable -->
                <td @click="selectedCat = cat.id">
                  {{ cat.name }}
                </td>
                <td class="text-center text-small">
                  {{ cat.weighting }}

                  <v-btn
                    icon
                    size="x-small"
                    class="float-right"
                    @click="showDeleteDialog(cat.id)"
                  >
                    <v-icon color="error">mdi-close</v-icon>
                    <v-tooltip
                      activator="parent"
                      location="bottom"
                      open-delay="700"
                      >Delete this category</v-tooltip
                    >
                  </v-btn>
                  <v-btn
                    style="
                      color: transparent !important;
                      box-shadow: none !important;
                    "
                    icon
                    size="small"
                    class="float-right"
                    ><v-tooltip
                      activator="parent"
                      location="bottom"
                      open-delay="700"
                      >Slice is currently active.</v-tooltip
                    >
                    <v-icon color="success">mdi-check</v-icon>
                  </v-btn>
                </td>
              </tr>
            </tbody>
          </v-table>
        </v-card>
        <br />
        <v-btn
          class="float-right"
          size="small"
          prepend-icon="mdi-pinwheel-outline"
          @click="addCategory"
        >
          Add Category
        </v-btn>

        <p v-if="currCategory.length <= 32" class="text-left text-green">
          Total Active Slices {{ currCategory.length }}/32
        </p>
        <p v-else class="text-left text-red">
          Total Active Slices {{ currCategory.length }}/32
        </p>
      </v-col>
      <v-col cols="7">
        <Details :selectedCat="getCat(selectedCat)" />
      </v-col>

      <!-- Category Info + Prizes -->
    </v-row>
    <!-- Misc Settings -->
    <v-row>
      <v-col cols="12">
        <v-expansion-panels v-model="panels">
          <v-expansion-panel value="timing">
            <v-expansion-panel-title v-slot="{ open }">
              <v-row no-gutters>
                <v-col cols="4" class="d-flex justify-start">
                  Default Timing (Seconds)
                </v-col>
              </v-row>
            </v-expansion-panel-title>
            <v-expansion-panel-text>
              <v-row no-gutters>
                <v-spacer></v-spacer>
                <v-col cols="5">
                  <v-text-field
                    label="Duration"
                    outlined
                    dense
                    type="number"
                    placeholder="180"
                  />
                </v-col>

                <v-divider vertical class="mx-4"></v-divider>

                <v-col cols="3"> Set Default Duration </v-col>
              </v-row>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn variant="text" color="grey">Clear </v-btn>
                <v-btn variant="text" color="green" @click="saveTiming">
                  Save
                </v-btn>
              </v-card-actions>
            </v-expansion-panel-text>
          </v-expansion-panel>
        </v-expansion-panels>
      </v-col>
    </v-row>
    <!-- Close Dialog -->
    <v-dialog
      v-model="dialog"
      :catId="catId"
      height="500"
      persistent
      max-width="400px"
    >
      <v-card>
        <v-card-text>
          Are you sure you want to delete this category?<br />
          <span class="text-red"
            >This will delete all prizes in the category!</span
          >
        </v-card-text>
        <v-card-actions>
          <v-btn color="grey" @click="dialog = false">Cancel</v-btn>
          <v-btn class="text-red" @click="(dialog = false), deleteCat(catId)"
            >Delete</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-snackbar
      v-model="snackbar"
      :timeout="timeout"
      :color="color"
      variant="tonal"
    >
      {{ text }}
      <!-- <template v-slot:action="{ attrs }"> -->
      <v-icon class="float-right">mdi-check</v-icon>
      <!-- </template> -->
    </v-snackbar>
  </v-container>
</template>

<script>
import Details from './spintowin/Details.vue';
export default {
  name: 'S2W',
  components: {
    Details,
  },
  data() {
    return {
      tab: 1,
      dialog: false,
      panels: [],

      //  TODO  SNACKBAR MOVE this to a mixin
      snackbar: false,
      text: '',
      color: '',
      timeout: 2000,
      selectedCat: null,
      catId: 0,
      categories: [],
      basicCategories: [],
      deluxeCategories: [],
      currCategory: [],
      // filter out categories that are not active
    };
  },
  methods: {
    async getCategories() {
      // Get Categories
      const resp = await fetch('/api/s2w/categories', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        },
      });
      const data = await resp.json();

      return data;
    },
    deleteCat(id) {
      this.currCategory = this.currCategory.filter((cat) => cat.id != id);
      console.log(id);
    },
    showDeleteDialog(id) {
      this.dialog = true;
      this.catId = id;
    },
    changeTab() {
      if (this.tab == 1) {
        this.currCategory = this.basicCategories;
      } else if (this.tab == 2) {
        this.currCategory = this.deluxeCategories;
      }
    },
    addCategory() {
      // TODO  add category to database via api
      this.currCategory.push({
        id: 0,
        name: 'New Category',
        count: 0,
        weighting: 0,
        background: 0,
        isDeluxe: 0,
      });
    },
    getCat(id) {
      return this.currCategory.find((cat) => cat.id == id);
    },
    saveTiming() {
      // TODO save timing to database via api
      this.panels = [];
      this.snackbar = true;
      this.text = 'Timing Saved';
      this.color = 'success';
    },
  },
  computed: {},
  async mounted() {
    // Get Categories
    const resp = await fetch('/api/s2w/categories', {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      },
    });
    const data = await resp.json();

    this.categories = data;
    data.forEach((category) => {
      if (category.isDeluxe == 1) {
        this.deluxeCategories.push(category);
      } else {
        this.basicCategories.push(category);
      }
    });
    this.changeTab();
  },
};
</script>
