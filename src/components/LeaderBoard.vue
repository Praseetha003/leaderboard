<template>
  <b-container class="bv-example-row">
	<b-row class="text-center">
		<b-col>
			<h1>Leader Board - Hilario Mayert League</h1>
		</b-col>
	</b-row>
	<b-row class="justify-content-md-center">
		<b-col>
			<b-nav  align="center" pills>
				<b-nav-item v-for="(group,index) in groups" :active="index === activeItem" :key="index" @click="setCurrTab(group.league_group_teams,index)">
					{{group.name.toUpperCase()}}
				</b-nav-item>
			</b-nav>
		</b-col>
	</b-row>
	<b-row class="text-center">
		<b-col>
			<b-table small
				:items="items"
				:fields="fields"
				:sort-by.sync="sortBy"
				:sort-desc.sync="sortDesc"
				responsive="sm"
			>
			<template #cell(index)="data">
				<b-avatar class="rank" :text="data.index + 1"></b-avatar>
			</template>
			<template #cell(team)="row">
				<b-avatar class="mr-3" :src="row.value.image['210']"></b-avatar> {{ row.value.name }}
			</template>
			<template #cell(team_matches_win_count)="data">
				<span class="win">{{ data.value }}</span>
			</template>
			<template #cell(team_matches_lose_count)="data">
				<span class="lose">{{ data.value }}</span>
			</template>
			</b-table>
		</b-col>
	</b-row>
  </b-container>
</template>

<script>
export default {
	name: 'LeaderBoard',
	data () {
		return {
			groups: null,
			sortBy: 'team_matches_score',
			sortDesc: true,
			activeItem: 0,
			fields: [
				{ key: 'index', label: 'Rank', sortable: true, class: 'text-left' },
				{ key: 'team', label: 'Team', sortable: true , class: 'text-left'},
				{ key: 'team_matches_score', label: 'Game Points', sortable: true, class: 'text-left' },
				{ key: 'team_match_schedules_score', label: 'Match Points', sortable: true, class: 'text-left' },
				{ key: 'team_matches_played_count', label: 'Played', sortable: true,class: 'text-left' },
				{ key: 'team_matches_win_count', label: 'Win', sortable: true, class: 'text-left' },
				{ key: 'team_matches_draw_count', label: 'Draw', sortable: true, class: 'text-left' },
				{ key: 'team_matches_lose_count', label: 'Lose', sortable: true, class: 'text-left' },
			],
			items: []
		}
	},
	mounted () {
		this.$http.get('https://wamp.owow.app/v2/leagues/hilario-mayert-league/leaderboards/league-groups')
		.then((response) => {
			//console.log(response)
			this.groups = response.data;
			
			var obj = Object.keys(response.data[0].league_group_teams).map((key) => {
				return response.data[0].league_group_teams[key]
			})
			this.setCurrTab(obj,0);
		})
		.catch(function (error) {
			console.log(error)
		});
	},
	methods: {
        setCurrTab(group,i) {
			this.items = group;
			this.activeItem = i;
        }
    }
}
</script>


