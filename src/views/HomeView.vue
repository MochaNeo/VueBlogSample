<template>
	<div>
		<div>
			<v-col v-for="article in articles" :key="article.id">
				<!--h1コンテナ-->
				<v-card to="detail">
					<!--イメージ-->
					<v-img
					:aspect-ratio="16 / 9"
					dark
					gradient="to top, rgba(25,32,72,.7), rgba(25,32,72,.0)"
					height="500px"
					:src="article.image.url">

						<v-card-text class="fill-height d-flex align-end">
							<v-row class="flex-column">

								<!--カテゴリ-->
								<v-col>
									<v-btn color="accent" to="category">Travel</v-btn>
								</v-col>

								<!--タイトル-->
								<v-col cols="12" lg="8" md="10" xl="7">
									<h2 class="text-h3 py-3" style="line-height: 1.2">
										{{ article.title }}
									</h2>
								</v-col>

								<!--作者・日時-->
								<v-col class="d-flex align-center">
									<v-avatar class="elevation-4" color="accent">
										<v-icon large>mdi-feather</v-icon>
									</v-avatar>
									<div class="text-h6 pl-2">Yan Lee · 22 July 2019</div>
								</v-col>

							</v-row>
						</v-card-text>
					</v-img>
				</v-card>
			</v-col>
		</div>


		<v-row>
			<v-col v-for="article in articles" :key="article.id" cols="12" lg="12" xl="8">
				<div>

					<!--Recommended For You-->
					<div class="pt-16">
						<h2 class="text-h4 font-weight-bold pb-4">Recommended For You</h2>

						<v-row>
							<v-col v-for="i in 6" :key="i" cols="12" lg="4" md="6">
								<v-hover
								v-slot:default="{ hover }"
								close-delay="50"
								open-delay="50">
									<div>
										<v-card
										:color="hover ? 'white' : 'transparent'"
										:elevation="hover ? 12 : 0"
										flat
										hover
										to="/detail">
											<!--画像-->
											<v-img
											:aspect-ratio="16 / 9"
											class="elevation-2"
											gradient="to top, rgba(25,32,72,.4), rgba(25,32,72,.0)"
											height="200px"
											:src="article.image.url"
											style="border-radius: 16px">
												<!--タグ-->
												<v-card-text>
													<v-btn color="accent" to="category">TIPS</v-btn>
												</v-card-text>
											</v-img>

											<!--テキスト-->
											<v-card-text>
												<!--タイトル-->
												<div class="text-h5 font-weight-bold primary--text">
													{{ article.title }}
												</div>

												<!--要約-->
												<div class="text-body-1 py-4">
													{{ article.detail }}
												</div>

												<!--作者・日時-->
												<div class="d-flex align-center">
													<v-avatar color="accent" size="36">
														<v-icon dark>mdi-feather</v-icon>
													</v-avatar>
													<div class="pl-2">Yan Lee · 22 July 2019</div>
												</div>
											</v-card-text>
										</v-card>
									</div>
								</v-hover>
							</v-col>
						</v-row>
					</div>

					<!--Featured-->
					<div class="pt-16">
						<h2 class="text-h4 font-weight-bold pb-4">Featured</h2>

						<v-row>
							<v-col v-for="i in 3" :key="i" cols="6" lg="4">
								<v-card dark flat>
									<!--画像-->
									<v-img
									:aspect-ratio="16 / 9"
									class="elevation-2 fill-height"
									gradient="to top, rgba(25,32,72,.4), rgba(25,32,72,.0)"
									height="600px"
									:src="article.image.url">
										<!--タグ-->
										<div class="d-flex flex-column justify-space-between fill-height">
											<v-card-text>
												<v-btn color="accent">ANIMALS</v-btn>
											</v-card-text>

											<!--テキスト-->
											<v-card-text>
												<!--タイトル-->
												<div
												class="text-h5 py-3 font-weight-bold"
												style="line-height: 1.2">
												{{ article.title }}
												</div>

												<!--作者・日時-->
												<div class="d-flex align-center">
													<v-avatar color="accent" size="36">
														<v-icon dark>mdi-feather</v-icon>
													</v-avatar>
													<div class="pl-2">Yan Lee · 03 Jan 2019</div>
												</div>
											</v-card-text>
										</div>
									</v-img>
								</v-card>
							</v-col>
						</v-row>
					</div>

					<!--Latest Posts-->
					<div class="pt-16">
						<h2 class="text-h4 font-weight-bold">Latest Posts</h2>

						<div>
							<v-row v-for="i in 6" :key="i" class="py-4">
								<v-col cols="12" md="4">
									<v-card flat height="100%">
										<!--画像-->
										<v-img
										:aspect-ratio="16 / 9"
										height="100%"
										:src="article.image.url"></v-img>
									</v-card>
								</v-col>

								<v-col>
									<div>
										<!--タグ-->
										<v-btn color="accent" depressed>TRAVEL</v-btn>

										<!--タイトル-->
										<h3 class="text-h4 font-weight-bold pt-3">
											{{ article.title }}
										</h3>

										<!--要約-->
										<p class="text-h6 font-weight-regular pt-3 text--secondary">
											{{ article.detail }}
										</p>

										<!--作者・日時-->
										<div class="d-flex align-center">
											<v-avatar color="accent" size="36">
												<v-icon dark>mdi-feather</v-icon>
											</v-avatar>
											<div class="pl-2">Yan Lee · 03 Jan 2019</div>
										</div>
									</div>
								</v-col>
							</v-row>
						</div>
					</div>
				</div>
			</v-col>

			<v-col>
				<div class="pt-16">
					<siderbar/>
				</div>
			</v-col>
		</v-row>
	</div>
</template>

<script>
import axios from "axios";

export default {
	name: "HomeView",
	components: {
		siderbar: () => import("@/components/details/SideBar"),
	},
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