<template>
  <v-app>

    <v-app-bar app color="primary" dark>
      <v-text-field
          slot="extension" 
          hide-details
          append-icon="mdi-microphone"
          flat
          label="Search"
          prepend-inner-icon="mdi-magnify"
          solo-inverted
        ></v-text-field>
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Vueshop</v-toolbar-title>

      <!-- pemisah konten -->
      <v-spacer></v-spacer>

      <v-btn icon>
        <v-badge color="orange" overlap>
          <template v-slot:badge>
            <span>3</span>
          </template>
          <v-icon>mdi-cart</v-icon>
        </v-badge>
      </v-btn>
    </v-app-bar>
    

    <v-card>
      <v-navigation-drawer app  v-model="drawer">

        <div class="pa-2" v-if="guest">
        <v-btn block color="primary" class="mb-1">
          <v-icon left>mdi-lock</v-icon>
            Login
        </v-btn>
        <v-btn block color="success">
          <v-icon left>mdi-account</v-icon>
            Register
        </v-btn>
      </div>

        <v-list-item v-if="!guest">
          <v-list-item-avatar>
            <v-img src="https://randomuser.me/api/portraits/men/78.jpg"></v-img>
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title>John Leider</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider>

        <v-list>
          <v-list-item
            v-for="(item, index) in menus"
            :key="`menu-`+index"
            :to="item.route"
          >
            <v-list-item-icon>
              <v-icon left>{{ item.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>

        <template v-slot:append v-if="!guest">
          <div class="pa-2">
            <v-btn block color="red" dark>
              <v-icon left>mdi-lock</v-icon>
                Logout
            </v-btn>
          </div>
        </template>
      </v-navigation-drawer>
      
    </v-card>
    
    
    

    <v-content>
      <v-container fluid>
        <!-- jika menggunakan vue-router -->
        <template>
  <div>
    <!-- template categries -->
    <v-container class="ma-0 pa-0" grid-list-sm>
      <div class="text-right">
        <v-btn small text to="/categories" class="blue--text">
          All Categories <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </div> 
      <v-layout wrap>
        <v-flex v-for="(category) in categories" :key="`category-`+category.id" xs6>
          <v-card :to="'/category/'+ category.slug">
            <v-img
              :src="category.image"
              class="white--text"
            >
              <v-card-title 
                class="fill-height align-end"
                v-text="category.name"
              ></v-card-title>
            </v-img>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>

    <!-- template books -->
    <v-container class="ma-0 pa-0 mt-2" grid-list-sm>
  <div class="text-right">
    <v-btn small text to="/books" class="blue--text">
      All Books <v-icon>mdi-chevron-right</v-icon>
    </v-btn>
  </div> 
  <v-layout wrap>
    <v-flex v-for="(book) in books" :key="`book-`+book.id" xs6>
      <v-card :to="'/book/'+ book.slug">
        <v-img
          :src="book.cover"
          class="white--text"
        >
          <v-card-title 
            class="fill-height align-end"
            v-text="book.title"
          ></v-card-title>
        </v-img>
      </v-card>
    </v-flex>
  </v-layout>
</v-container>

  </div>
</template>
        <router-view></router-view>
      </v-container>
    </v-content>

    <v-card>
      <v-footer absolute app>
        <v-card-text class="text-center">
          &copy; {{ new Date().getFullYear() }} — <strong>Vueshop</strong>
        </v-card-text>
      </v-footer>
    </v-card>

  </v-app>
  
</template>

<script>
export default {
  created () {
    window.axios.get('http://127.0.0.1:8000/buku/PHP MySQL')
    .then((response) => {
        console.log(response)
    })
    .catch((error) => {
        console.log(error)
    })
  },
  name: 'App',
  data: () => ({
  drawer: true,
  menus: [
    { title: 'Home', icon: 'mdi-home', route: '/' },
    { title: 'About', icon: 'mdi-account', route: '/about' },
  ],
  guest: true, // <= tambahkan ini
  categories: [
      { 
        id: 1,
        image: 'https://via.placeholder.com/150',
        name: 'Ekonomi',
        slug: 'ekonomi'
      },
      { 
        id: 2,
        image: 'https://via.placeholder.com/150',
        name: 'Agama',
        slug: 'agama'
      },
  ],
  books: [
      { 
        id: 1,
        cover: 'https://via.placeholder.com/150',
        title: 'Laravel 5.8',
        slug: 'laravel-5-8'
      },
      { 
        id: 2,
        cover: 'https://via.placeholder.com/150',
        title: 'Vue 2.6',
        slug: 'vue-2-6'
      },
      { 
        id: 3,
        cover: 'https://via.placeholder.com/150',
        title: 'PHP 7.4',
        slug: 'php-7-4'
      },
      { 
        id: 4,
        cover: 'https://via.placeholder.com/150',
        title: 'NodeJS 12',
        slug: 'nodejs-12'
      },
    ]
})
};


</script>

