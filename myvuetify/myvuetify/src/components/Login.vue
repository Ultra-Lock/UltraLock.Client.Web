<template>
  <v-app id="inspire">
    <v-alert dense outlined type="error" v-if="alert_login">
      密码/用户名错误
    </v-alert>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.png')"
          class="my-3"
          contain
          height="200"
          v-if="!juage_login"
        />
      </v-col>
      <div class="mx-auto">
        <v-form ref="form" lazy-validation>
          <v-text-field
            v-model="user_put"
            :counter="10"
            label="用户名"
            required
            v-if="!juage_login"
          ></v-text-field>
          <v-text-field
            v-model="passord_put"
            label="密码"
            required
            v-on:keyup.enter="login(user_put, passord_put)"
            v-if="!juage_login"
          ></v-text-field>

          <v-btn
            block
            depressed
            elevation="5"
            raised
            v-on:click="login(user_put, passord_put)"
            v-if="!juage_login"
            >登录</v-btn
          >
        </v-form>
      </div>
    </v-row>
    <v-system-bar app>
      <v-spacer></v-spacer>

      <v-icon>mdi-square</v-icon>

      <v-icon>mdi-circle</v-icon>

      <v-icon>mdi-triangle</v-icon>
    </v-system-bar>

    <v-alert dense outlined type="error" v-if="alert_empty">
      不能输入空口令
    </v-alert>
    <v-alert dense outlined type="error" v-if="alert_repeat">
      不能输入重复口令
    </v-alert>
    <v-navigation-drawer v-model="drawer" app v-if="juage_login">
      <v-sheet color="grey lighten-4" class="pa-4">
        <v-avatar class="mb-4" color="pink darken-1" size="64">
            <img src="http://5b0988e595225.cdn.sohucs.com/images/20190720/08cfa5238aae4ccf9dcaa1760fa8f81a.jpeg">
        </v-avatar>

        <div>www.gaein.cn/</div>
      </v-sheet>

      <v-divider></v-divider>

      <v-list>
        <v-list-item v-for="[icon, text] in links" :key="icon" link>
          <v-list-item-icon>
            <v-icon>{{ icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
 <v-app-bar app
 v-if="juage_login"
 >
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>管理</v-toolbar-title>
    </v-app-bar>

                <template
                v-if="juage_login"
                >
                    <v-img
                            :src="imgsrc"
                            class="my-1"
                            contain
                            height="150"
                    />
                    <div>
                    <v-btn
                            class="ma-2"
                            outlined
                            color="indigo"
                            @click="getpic"
                    >
                        随机动漫图片
                    </v-btn>
                    <v-btn
                            class="ma-2"
                            color="success"
                            @click="loader = 'loading2'"
                    >
                        开门
                    </v-btn>
                    </div>
                    <v-card
                            class="mx-auto"
                            max-width="344"
                            v-if="juage_display&&juage_login"
                    >
                        <v-card-text>
                            <div>NFCid</div>
                            <p class="display-1 text--primary">
                                963455266
                            </p>
                        </v-card-text>
                        <v-card-actions>
                            <v-btn
                                    text
                                    color="teal accent-4"
                                    @click="juage_display = false"
                            >
                                Close it
                            </v-btn>
                        </v-card-actions>

                    </v-card>
                    <v-banner
                            elevation="4"
                            style="display:inline"
                    >
                  <v-text-field
                    v-model="word"
                    :counter="10"
                    label="单次口令添加"
                    required
                    v-if="juage_login"
                    @keyup.enter="pushword(word)"
                  ></v-text-field>
                    <v-btn
                            class="mx-2"
                            fab
                            dark
                            color="indigo"
                            v-on:click="pushword(word)"
                            v-if="juage_login"
                    >
                        <v-icon dark>
                            mdi-plus
                        </v-icon>
                    </v-btn>
                    </v-banner>
                    <v-list>
                        <v-list-item
                                v-for="(item, i) in words"
                        >
                            <v-list-item-icon>
                                <v-icon
                                        v-if="item.icon"
                                        color="pink"
                                >
                                    mdi-star
                                </v-icon>
                            </v-list-item-icon>

                            <v-list-item-content style="display:inline">
                                <v-chip
                                        class="ma-2"
                                        color="green"
                                        text-color="white"
                                >
                                    {{ i + 1 + "  :  " + item + "" }}
                                </v-chip>
                                <v-btn
                                        depressed
                                        color="error"
                                        @click="delate(index)"
                                >
                                    Delete
                                </v-btn>
                            </v-list-item-content>

                            <v-list-item-avatar>
                                <v-img :src="item.avatar"></v-img>
                            </v-list-item-avatar>
                        </v-list-item>
                    </v-list>

                </template>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    imgsrc:"",
    user: "yeling",
    passord: 123456,
    user_put: "",
    passord_put: "",
    juage_login: false,
    juage_display:true,
    alert_empty: false,
    alert_repeat: false,
    alert_login:false,
    adminid:963455266,
    cards: ["口令"],
    drawer: null,
    word: "",
      reveal:true,
    words: ["芝麻开门", "芝麻拆门"],
    links: [["mdi-inbox-arrow-down", "管理"]],
    ecosystem: [
      {
        text: "vuetify-loader",
        href: "https://github.com/vuetifyjs/vuetify-loader",
      },
      {
        text: "github",
        href: "https://github.com/vuetifyjs/vuetify",
      },
      {
        text: "awesome-vuetify",
        href: "https://github.com/vuetifyjs/awesome-vuetify",
      },
    ],
    importantLinks: [
      {
        text: "Documentation",
        href: "https://vuetifyjs.com",
      },
      {
        text: "Chat",
        href: "https://community.vuetifyjs.com",
      },
      {
        text: "Made with Vuetify",
        href: "https://madewithvuejs.com/vuetify",
      },
      {
        text: "Twitter",
        href: "https://twitter.com/vuetifyjs",
      },
      {
        text: "Articles",
        href: "https://medium.com/vuetify",
      },
    ],
    whatsNext: [
      {
        text: "Explore components",
        href: "https://vuetifyjs.com/components/api-explorer",
      },
      {
        text: "Select a layout",
        href: "https://vuetifyjs.com/getting-started/pre-made-layouts",
      },
      {
        text: "Frequently Asked Questions",
        href:
          "https://vuetifyjs.com/getting-started/frequently-asked-questions",
      },
    ],
  }),
  methods: {
    login(user_put, passord_put) {
      if (this.user_put == "yeling" && this.passord_put == "123456") {
        this.juage_login = true;
        this.getpic();
      }
      if (this.juage_login) {
        this.alert_login=false;
      } else {
        this.alert_login=true;
      }
    },
    pushword(word) {
      for (let i = 1; i < this.words.length; i++) {
        if (this.word == this.words[i]) {
          this.alert_repeat = true;
          break;
        }
        else{
            this.alert_repeat = false;
        }
      }
      if (word == "") {
        this.alert_empty = true;
      }
      else{
          this.alert_empty = false;
      }
      if (!this.alert_repeat && word != "") {
        this.alert_empty = false;
        this.alert_repeat = false;
        this.words.push(this.word);
        this.word = "";
      }
    },
    delate(index) {
      this.words.splice(index, 1);
    },
      getpic(){
        var that=this;
          this.$axios.get("https://api.vvhan.com/api/acgimg").then(function(response){
            console.log(response);
            that.imgsrc=response.request.responseURL;
            console.log(imgsrc);
        },function(err){

        })
      },
  },
};
</script>