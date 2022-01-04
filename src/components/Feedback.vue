<template>
  <v-container>
    <v-card>
      <v-card-title>
        Feedback
      </v-card-title>
      <v-spacer></v-spacer>
      <v-data-table
        :headers="headers"
        :items="items"
        :hide-default-header="true"
        item-key="name"
        class="elevation-1"
      >
        <template v-slot:top>
          <v-toolbar
            flat
          >
            <!-- <v-toolbar-title>Feedback</v-toolbar-title> -->
            <v-spacer></v-spacer>
            <v-dialog
              v-model="dialog"
              max-width="500px"
            >
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  color="primary"
                  dark
                  class="mb-2"
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon>mdi-plus</v-icon>
                </v-btn>
              </template>
              <v-card>
                <v-card-title>
                  <span class="text-h5">{{ formTitle }}</span>
                </v-card-title>

                <v-card-text>
                  <v-container>
                    <v-row>
                      <v-col
                        cols="12"
                        sm="6"
                        md="4"
                      >
                        <!-- <v-select
                          v-model="editedItem.category"
                          :items="categories"
                          item-text="state"
                          label="Select"
                          return-object
                          single-line
                        ></v-select> -->
                        <!-- <v-text-field
                          v-model="editedItem.category"
                          label="Category"
                        ></v-text-field> -->
                      </v-col>
                      <v-col
                        cols="12"
                      >
                        <v-text-field
                          v-model="editedItem.subject"
                          label=""
                        ></v-text-field>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card-text>

                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn
                    color="blue darken-1"
                    text
                    @click="close"
                  >
                    Cancel
                  </v-btn>
                  <v-btn
                    color="blue darken-1"
                    text
                    @click="save"
                  >
                    Save
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
            <v-dialog v-model="dialogDelete" max-width="500px">
              <v-card>
                <v-card-title class="text-h5">Are you sure you want to delete this item?</v-card-title>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
                  <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
                  <v-spacer></v-spacer>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </v-toolbar>
        </template>
        <template v-slot:item.toThread="{ item }">
          <router-link :to="item.id" style="text-decoration: none; color: inherit;">
          <v-icon
            small
            class="mr-2"
          >
            mdi-clipboard-text-multiple-outline
          </v-icon>
          </router-link>
        </template>
        <template v-slot:item.actions="{ item }">
          <v-icon
            small
            class="mr-2"
            @click="editItem(item)"
          >
            mdi-pencil
          </v-icon>
          <v-icon
            small
            @click="deleteItem(item)"
          >
            mdi-delete
          </v-icon>
        </template>
        <template v-slot:no-data>
          <v-btn
            color="primary"
            @click="initialize"
          >
            Reset
          </v-btn>
        </template>
      </v-data-table>
    </v-card>
  </v-container>
</template>

<script>

  export default {
    name: 'Feedback',
    data () {
      return {
        dialog: false,
        dialogDelete: false,
        items: [],
        editedIndex: -1,
        editedItem: {
          subject: '',
          category: '',
        },
        defaultItem: {
          subject: '',
          category: '',
        },
        headers: [
          {
            text: '内容',
            align: 'start',
            value: 'subject',
            groupable: false,
          },
          {
            text: 'Thread',
            value: 'toThread',
            sortable: false
          },
          {
            text: 'Actions',
            value: 'actions',
            sortable: false
          },
        ],
      };
    },
    methods: {
      filter(val, search) {
        return val === search;
      },
      initialize () {
        this.items = [
          {
            id: "1",
            subject: 'アプリが欲しい',
            category: 'feedback',
            content: 'アプリ版が欲しいです。'
          },
          {
            id: "2",
            subject: '一部の方の声だけ聞こえなくなることがある',
            category: 'feedback',
            content: '一部の方の声だけ聞こえなくなることがあるので、改善して欲しいです。'
          },
          {
            id: "3",
            subject: '「離席」ではなく「取り込み中」状態が欲しい',
            category: 'feedback',
            content: '「取り込み中」のステータスを追加して欲しいです。'
          },
          {
            id: "4",
            subject: 'ホワイトボードツール',
            category: 'feedback',
            content: 'ホワイトボードツールがあると便利だと思います。'
          },
          {
            id: "5",
            subject: 'ミュートを解除した瞬間に話し出すと最初の1秒ほど相手に声が届いていない',
            category: 'feedback',
            content: 'ミュートを解除した瞬間に話し出すと最初の1秒ほどは相手に声が届いてないようなので改善をお願いいたします。'
          },
        ]
      },
      editItem (item) {
        this.editedIndex = this.items.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },
      deleteItem (item) {
        this.editedIndex = this.items.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },
      deleteItemConfirm () {
        this.items.splice(this.editedIndex, 1)
        this.closeDelete()
      },
      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },
      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },
      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.items[this.editedIndex], this.editedItem)
        } else {
          this.items.push(this.editedItem)
        }
        this.close()
      },
    },
    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      },
    },
    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },
    created () {
      this.initialize()
    }
  }
</script>
