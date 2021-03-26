<template>
	<div class="dashboard">
		<h1 class="subheading grey--text">Dashboard</h1>
		<v-container class="my-5">
			<v-layout row class="mb-3 pr-1">
				<v-btn small text color="grey" @click="sortBy('title')">
					<v-icon left small>mdi-folder</v-icon>
					<span class="caption text-lowercase">By project name</span>
				</v-btn>
				<v-btn small text color="grey" @click="sortBy('person')">
					<v-icon left small>mdi-account</v-icon>
					<span class="caption text-lowercase">By person</span>
				</v-btn>
				<v-spacer></v-spacer>
				<Popup btn_icon="mdi-plus-box" />
			</v-layout>
			<v-card flat class="pa-3" v-for="project in projects" :key="project.title">
				<v-row :class="`project ${project.status}`">
					<v-col cols="12" md="6">
						<div class="caption grey--text">Project Title</div>
						<div>{{ project.title }}</div>
					</v-col>
					<v-col xs="2">
						<div class="caption grey--text">Person</div>
						<div>{{ project.person }}</div>
					</v-col>
					<v-col xs="2">
						<div class="caption grey--text">Due Date</div>
						<div>{{ project.due }}</div>
					</v-col>
					<v-col xs="2">
						<div>
							<v-chip small :class="`${project.status} white--text caption my-3`">{{ project.status }}</v-chip>
						</div>
					</v-col>
				</v-row>
				<v-row>
					<v-divider></v-divider>
				</v-row>
			</v-card>
		</v-container>
	</div>
</template>

<script>
import Popup from "../components/Popup";
export default {
	name: "Home",
	components: { Popup },
	methods: {
		sortBy(prop) {
			this.projects.sort((a, b) => (a[prop] < b[prop] ? -1 : 1));
		},
		async getProjects() {
			const res = await fetch("http://localhost:3000/projects");
			let Projects = await res.json();
			return Projects;
		},
	},
	data() {
		return {
			projects: [],
		};
	},
	async created() {
		this.projects = await this.getProjects();
	},
};
</script>

<style lang="scss">
.project {
	&.complete {
		border-left: 4px solid #3cd1c2;
	}
	&.ongoing {
		border-left: 4px solid #e6bc4c;
	}
	&.overdue {
		border-left: 4px solid #d1663c;
	}
}
.v-chip {
	&.complete {
		background: #3cd1c2 !important;
	}
	&.ongoing {
		background: #e6bc4c !important;
	}
	&.overdue {
		background: #d1663c !important;
	}
}
</style>
