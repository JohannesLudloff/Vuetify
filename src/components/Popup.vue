<template>
	<v-dialog v-model="dialog" persistent max-width="600px">
		<template v-slot:activator="{ on, attrs }">
			<v-btn v-bind="attrs" v-on="on" icon>
				{{ btn_description }}
				<v-icon color="primary">
					{{ btn_icon }}
				</v-icon>
			</v-btn>
		</template>
		<v-card>
			<v-card-title>
				<span class="headline">Add Project</span>
			</v-card-title>
			<v-card-text>
				<v-form ref="form">
					<v-row>
						<v-col cols="12">
							<v-text-field
								required
								label="Project Title*"
								v-model="title"
								prepend-icon="mdi-folder"
								hint="Give a unique name to your project"
								:rules="inputRules"
							></v-text-field>
						</v-col>
						<v-col cols="12">
							<v-textarea label="Information" prepend-icon="mdi-pencil" v-model="content" :rules="inputRules"></v-textarea>
						</v-col>
						<v-col cols="6">
							<v-menu min-width="auto">
								<template v-slot:activator="{ on }">
									<v-text-field
										prepend-icon="mdi-calendar-range"
										:value="computedDateFormattedMomentjs"
										clearable
										label="Due Date"
										readonly
										v-on="on"
										@click:clear="date = null"
										:rules="inputRules"
									></v-text-field>
								</template>
								<v-date-picker v-model="date"></v-date-picker>
							</v-menu>
						</v-col>
					</v-row>
				</v-form>
				<small>*indicates required field</small>
			</v-card-text>
			<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn color="primary darken-1" text @click="dialog = false">
					Close
				</v-btn>
				<v-btn color="primary darken-1" text @click="submit">
					Save
				</v-btn>
			</v-card-actions>
		</v-card>
	</v-dialog>
</template>

<script>
import moment from "moment";
import { format, parseISO } from "date-fns";
export default {
	data: () => ({
		dialog: false,
		title: "",
		content: "",
		date: format(parseISO(new Date().toISOString()), "yyyy-MM-dd"),
		inputRules: [(v) => v.length >= 5 || "Minimum length is 5 characters"],
	}),
	props: {
		btn_description: String,
		btn_icon: String,
	},
	methods: {
		submit() {
			if (this.$refs.form.validate()) {
				const project = {
					// ! care ! not creating an id here in this object, this will only work with json server as it creates the id for itself
					title: this.title,
					content: this.content,
					due: this.due,
					person: "Me",
					status: "ongoing",
				};
				// save data here
				const options = {
					method: "POST",
					headers: {
						"Content-Type": "application/json",
					},
					body: JSON.stringify(project),
				};
				fetch("http://localhost:3000/projects", options);
				this.dialog = false;
			}
		},
	},
	computed: {
		computedDateFormattedMomentjs() {
			return this.date ? moment(this.date).format("DD.MM.YYYY") : "";
		},
	},
};
</script>
