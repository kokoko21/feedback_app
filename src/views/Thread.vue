<template>
  <v-container>
    <v-row>
      <v-col cols="12">
      <v-card
        elevation="10"
        outlined
      >
        <v-card-title>{{ thread.subject }}</v-card-title>
        <v-card-subtitle>{{ thread.user }}</v-card-subtitle>
        <v-card-text>{{ thread.content }}</v-card-text>
      </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-text-field
          outlined
          v-model="newContent"
        ></v-text-field>
        <v-btn
          class="mr-4"
          type="submit"
          value="送信"
          @click="addComent(newContent)"
        >
          submit
        </v-btn>
      </v-col>
    </v-row>
    <v-list three-line>
      <template v-for="(coment, index) in coments">
        <!-- <v-subheader
          :key="coment.header"
          v-text="coment.header"
        ></v-subheader> -->
        <v-divider
          :key="index"
        ></v-divider>
        <v-list-item
          :key="coment.text"
        >
          <v-list-item-content>
            <v-list-item-title v-html="coment.text"></v-list-item-title>
            <v-list-item-subtitle v-html="coment.user"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </template>
    </v-list>
  </v-container>
</template>

<script>

export default {
  data: () => ({
    name: 'Thread',
    coment: {},
    newContent: '',
    newComent: {
      text: '',
      user: '',
    },
    defaultComent: {
      text: '',
      user: '',
    },
    thread:
    {
      id: '1',
      subject: 'アプリが欲しい',
      user: 'user01',
      content: 'Greyhound divisively hello coldly wonderfully marginally far upon excluding.',
    },
    coments: [
      {
        text: 'Brunch this weekend?',
        user: 'Ali Connors',
      },
      {
        text: 'Summer BBQ ',
        user: 'Jennifer',
      },
      {
        text: 'Oui oui',
        user: 'Sandra Adams',
      },
      {
        text: 'Birthday gift',
        user: 'Trevor Hansen',
      },
      {
        text: 'Recipe to try',
        user: 'Britta Holt',
      },
    ],
  }),
  methods: {
    addComent(newContent) {
      this.newComent.user = 'user02'
      this.newComent.text = newContent
      console.log(this.newComent)
      this.coments.push(this.newComent)
      this.afterComent()
    },
    afterComent() {
      this.$nextTick(() => {
        this.newComent = Object.assign({}, this.defaultComent)
      })
      this.newContent = ''
    }
  }
}
</script>