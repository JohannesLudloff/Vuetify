<template>
	<div class="team">
		<h1 class="subheading grey--text">Team</h1>

		<v-container class="my-5">
			<v-layout row wrap>
				<v-flex xs12 sm6 md4 lg2 v-for="person in team" :key="person.name.first">
					<v-card flat class="text-center ma-3">
						<v-responsive class="pt-4">
							<v-avatar size="100">
								<img :src="person.picture.large" alt="picture" />
							</v-avatar>
						</v-responsive>
						<v-card-text>
							<div class="">{{ person.name.first }} {{ person.name.last }}</div>
							<div class="caption grey--text">{{ person.location.city }}</div>
						</v-card-text>
						<v-card-actions>
							<div class="my-2 grey--text">
								<v-btn fab text x-small class="grey--text">
									<v-icon>mdi-television</v-icon>
								</v-btn>
							</div>
							<div class="my-2 grey--text">
								<v-btn fab text x-small class="grey--text">
									<v-icon>mdi-twitter</v-icon>
								</v-btn>
							</div>
							<div class="my-2 ">
								<v-btn fab text x-small class="grey--text">
									<v-icon>mdi-facebook</v-icon>
								</v-btn>
							</div>
							<div class="my-2 ">
								<v-btn fab text x-small class="grey--text">
									<v-icon>mdi-github</v-icon>
								</v-btn>
							</div>
						</v-card-actions>
					</v-card>
				</v-flex>
			</v-layout>
		</v-container>
	</div>
</template>

<script>
export default {
	name: "team",
	methods: {
		async getUsers() {
			const res = await fetch("https://randomuser.me/api/?results=10&nat=DE");
			let Users = await res.json();
			return Users.results;
		},
	},
	data() {
		return {
			team: [],
		};
	},
	async created() {
		this.team = await this.getUsers();
	},
};
</script>
