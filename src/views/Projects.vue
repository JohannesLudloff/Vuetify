<template>
	<div class="projects">
		<h1 class="caption grey--text">Projects</h1>
		<v-container>
			<v-expansion-panels accordion>
				<v-expansion-panel v-for="project in myProjects" :key="project.title">
					<v-expansion-panel-header>
						{{ project.title }}
					</v-expansion-panel-header>
					<v-expansion-panel-content class="px-4 grey--text">
						<div class="font-weight-bold">{{ project.due }}</div>
						<div>{{ project.content }}</div>
					</v-expansion-panel-content>
				</v-expansion-panel>
			</v-expansion-panels>
		</v-container>
	</div>
</template>

<script>
export default {
	data() {
		return {
			projects: [],
		};
	},
	methods: {
		async getProjects() {
			const res = await fetch("http://localhost:3000/projects");
			let Projects = await res.json();
			return Projects;
		},
	},
	async created() {
		this.projects = await this.getProjects();
	},

	computed: {
		myProjects() {
			return this.projects.filter((project) => project.person === "Me");
		},
	},
};
</script>
