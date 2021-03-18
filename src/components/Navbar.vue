<template>
	<nav>
		<v-app-bar flat app>
			<v-icon left class="grey--text" @click="drawer = !drawer">mdi-menu</v-icon>
			<v-toolbar-title class="grey--text">
				<span class="font-weight-light">Todo</span>
				<span class="primary--text text--accent-2 font-weight-bold">Ninja</span>
			</v-toolbar-title>
			<v-spacer></v-spacer>
			<v-btn text color="grey">
				<span>sign out</span>
				<v-icon right>mdi-exit-to-app</v-icon>
			</v-btn>
		</v-app-bar>
		<v-navigation-drawer disable-resize-watcher temporary app class="primary" v-model="drawer">
			<v-list>
				<v-list-item v-for="link in links" :key="link.text" router :to="link.route">
					<v-list-item-action>
						<v-icon class="white--text">{{ link.icon }}</v-icon>
					</v-list-item-action>
					<v-list-item-content class="white--text">
						{{ link.text }}
					</v-list-item-content>
				</v-list-item>
			</v-list>
		</v-navigation-drawer>
	</nav>
</template>

<script>
export default {
	name: "Navbar",
	data() {
		return {
			drawer: false,
			links: [
				{ icon: "mdi-view-dashboard", text: "Dashboard", route: "/" },
				{ icon: "mdi-folder", text: "My Projects", route: "/projects" },
				{ icon: "mdi-account-supervisor-circle", text: "Team", route: "/team" },
			],
		};
	},
};
</script>
