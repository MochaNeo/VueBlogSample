<template>
    <div>
        <!--Popular Posts-->
        <div>
            <h3 class="text-h5 font-weight-medium pb-4">Popular Posts</h3>
            <v-divider></v-divider>
            <div>
                <v-row v-for="article in articles" :key="article.id" class="py-2">
                    <!--サムネ-->
                    <v-col cols="12" md="6" lg="5">
                        <v-card height="100%" flat>
                            <v-img
                                :src="article.image.url"
                                :aspect-ratio="16 / 9"
                                height="100%"
                            ></v-img>
                        </v-card>
                    </v-col>

                    <!--テキスト-->
                    <v-col>
                        <div>
                            <!--タグ-->
                            <v-btn depressed color="accent" small>TRAVEL</v-btn>
    
                            <!--タイトル-->
                            <h3 class="text-h6 font-weight-bold primary--text py-3">
                                {{ article.title }}
                            </h3>
    
                            <!--作者・日付-->
                            <div class="d-flex align-center">
                                <v-avatar color="accent" size="24">
                                    <v-icon dark small>mdi-feather</v-icon>
                                </v-avatar>
                                <div class="pl-2">Yan Lee · 03 Jan 2019</div>
                            </div>

                        </div>
                    </v-col>
                </v-row>
            </div>
        </div>

        <!--Category-->
        <div class="pt-4">
            <h3 class="text-h5 font-weight-medium pb-4">Category</h3>
            <v-divider></v-divider>
            <v-card color="accent" dark flat v-for="i in 5" :key="i" class="my-4">
                <v-card-text
                    class="d-flex justify-space-between align-center white--text">
            
                <h6 class="text-h6">Travel</h6>
  
                <div class="text-h6">47</div>

                </v-card-text>
            </v-card>
        </div>

        <!--Tag-->
        <div class="pt-4">
            <h3 class="text-h5 font-weight-medium pb-4">Tags</h3>
            <v-divider></v-divider>
            <v-row class="pt-4">
                <v-col v-for="i in 7" :key="i" class="flex-shrink-0" cols="auto">
                    <v-chip color="accent">#Images</v-chip>
                </v-col>
            </v-row>
        </div>
  
        <!--Newsletter-->
        <div class="pt-4">
            <h3 class="text-h5 font-weight-medium pb-4">Newsletter</h3>
            <v-divider></v-divider>
            <v-text-field
                label="Your email adress"
                solo
                type="email"
                outlined
                flat
                class="pt-4"
            ></v-text-field>
            <v-btn color="accent" block large>Subscrbe</v-btn>
        </div>
    </div>
</template>



<script>
import axios from "axios";
  
export default {
    name: "HomeView",
    data: () => ({
        articles: []
    }),
    async mounted() {
        //記事の取得
        await axios.get('https://nepnep.microcms.io/api/v1/articles', {
            headers: { 'X-API-KEY': process.env.VUE_APP_X_API_KEY }
        })
        .then((response) => this.articles = response.data.contents);
    }
};
</script>