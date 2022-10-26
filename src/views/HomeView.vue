<template>
  <v-container fluid>
    <v-row>
      <v-col cols="12">
        <v-data-table
          :headers="headers"
          :items="plans"
          hide-default-footer
          class="text-h3">
  
          <template v-slot:top>
            <v-toolbar flat>
              <v-toolbar-title class="mr-3">Plans</v-toolbar-title>
              <v-divider
                class="mx-4"
                inset
                vertical></v-divider>
  
              <v-spacer></v-spacer>
  
              <v-dialog
                v-model="dialog"
                max-width="750">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    dark
                    tile
                    v-on="on"
                    v-bind="attrs">
                    New Phase
                  </v-btn>
                </template>
  
                <v-card>
                  <v-card-title>Create New Phase</v-card-title>
                  <v-card-text>
                    <v-container>
                      <v-row>
                        <v-col
                          md="6"
                          sm="12">
                          <v-text-field
                            v-model="editedItem.name"
                            :label="editedItemLabel.name"
                            dense
                            class="rounded-0"
                            outlined>
                          </v-text-field>
                        </v-col>
                      </v-row>
                      <v-row>
                        <v-col
                          md="12"
                          sm="12">
                          <v-textarea
                            v-model="editedItem.description"
                            :label="editedItemLabel.description"
                            dense
                            class="rounded-0"
                            outlined>
                          </v-textarea>
                        </v-col>
                      </v-row>
                      <v-row>
  
                        <v-col
                          md="6"
                          sm="12">
                          <v-menu
                            v-model="start_date_menu">
                            <template v-slot:activator="{ on, attrs }">
                              <v-text-field
                                v-model="editedItem.start_date"
                                :label="editedItemLabel.start_date"
                                append-icon="mdi-calendar"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                dense
                                class="rounded-0"
                                outlined>
                              </v-text-field>
                            </template>
                            <v-date-picker
                              v-model="editedItem.start_date"
                              no-title
                              scrollable>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
  
                        <v-col
                          md="6"
                          sm="12">
                          <v-menu
                            v-model="end_date_menu">
                            <template v-slot:activator="{ on, attrs }">
                              <v-text-field
                                v-model="editedItem.end_date"
                                :label="editedItemLabel.end_date"
                                append-icon="mdi-calendar"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                dense
                                class="rounded-0"
                                outlined>
                              </v-text-field>
                            </template>
                            <v-date-picker
                              v-model="editedItem.end_date"
                              no-title
                              scrollable>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </v-row>
                    </v-container>
                  </v-card-text>
  
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn
                      color="blue darken-1"
                      text
                      @click="cancel">
                      Cancel
                    </v-btn>
                    <v-btn
                      color="blue darken-1"
                      text
                      @click="save">
                      Save
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-toolbar>
          </template>
  
          <template v-slot:item.actions="{ item }">
            <v-icon>
              mdi-pencil
            </v-icon>
            <v-icon>
              mdi-delete
            </v-icon>
          </template>
        </v-data-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      dialog: false,
      start_date_menu: false,
      end_date_menu: false,
      editedIndex: -1,
      date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
      editedItem: {
        name: '',
        description: '',
        start_date: '',
        end_date: '',
      },
      defaultItem: {
        name: '',
        description: '',
        start_date: '',
        end_date: '',
      },
      editedItemLabel: {
        name: 'Name',
        description: 'Description',
        start_date: 'Start Date',
        end_date: 'End Date'
      },
      headers: [
        { text: 'Name', align: 'left', value: 'name' },
        { text: 'Description', value: 'description' },
        { text: 'Start Date', value: 'start_date' },
        { text: 'End Date', value: 'end_date' },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      plans: [
        {
          name: 'Plan 1',
          description: 'Plan 1 Description',
          start_date: '01/01/2022',
          end_date: '01/02/2022',
        },
        {
          name: 'Plan 2',
          description: 'Plan 2 Description',
          start_date: '01/01/2022',
          end_date: '01/02/2022',
        },
      ],
    }
  },
  methods: {
    editItem(item) {
      console.log('edit item: ', item)
    },
    deleteItem(item) {
      console.log('delete item: ', item)
    },
    save() {
      console.log('save', this.editedIndex, this.editedItem)
    },
    cancel() {
      this.dialog = false
      this.editedItem = this.defaultItem
      console.log('close', this.editedIndex)
    },
  }
}
</script>

<!-- <template v-slot:body=" { items } ">
                      <tbody>
                        <tr v-for="(item, index) in items" :key="index">
                          <td>{{item.name}}</td>
                          <td>{{item.description}}</td>
                          <td>{{item.start_date}}</td>
                          <td>{{item.end_date}}</td>
                        </tr>
                      </tbody>
                    </template> -->