<template>
	<div class="user-profile">
		<div class="user-profile__user-panel">
			<h1 class="user-profile__username">@{{ user.username }}</h1>
			<div class="user-profile__admin-badge" v-if="user.isAdmin">
				Admin
			</div>
			<div class="user-profile__follower-count">
				<strong>Followers: </strong> {{ followers }}
			</div>
		</div>
		<div class="user-profile__twoots-wrapper">
			<TwootItem 
				v-for="twoot in user.twoots" 
				:key="twoot.id" 
				:username="user.username" 
				:twoot="twoot" 
				@favourite="toggleFavourite(twoot.id)"
			/>
		</div>
	</div>
</template>

<script>

import TwootItem from "./TwootItem";

export default {
	name: 'UserProfile',
	data(){
	return{
		followers: 0,
		user: {
		id:1,
		username: '_HH',
		firstName: 'Hans-Henrik',
		lastName: 'Høgsted',
		email: 'hh@debtia.dk',
		isAdmin: true,
		twoots: [
			{id: 1, content: 'Twotter is amazing!'},
			{id: 2, content: 'Follow @_HH'},
			{id: 3, content: 'Twotter go BRRRRR'}
		]
		}
	}
	},
	methods:{
	followUser(){
		this.followers++;
	},
	toggleFavourite(id){
		console.log(`Favourited Twoot #${id}`)
	}
	},
	computed:{
	fullName(){
		return `${this.user.firstName} ${this.user.lastName}`;
	}
	},
	mounted(){
	},
	watch: {
		followers(newFollowerCount, oldFollowerCount){
			if(oldFollowerCount < newFollowerCount){
			console.log(`${this.user.username} has gained a follower!`);
			}
		}
	},
	components:{
		TwootItem
	}
}
</script>

<style>
.user-profile{
	display: grid;
	grid-template-columns: 1fr 3fr;
	width: 100%;
	padding: 50px 5%;
}

.user-profile__user-panel{
	display: flex;
	flex-direction: column;
	margin-right: 50px;
	padding: 20px;
	background-color: white;
	border-radius: 5px;
	border: 1px solid #DFE3E8;
}

.user-profile__admin-badge{
	padding: 2px 10px;
	background: rebeccapurple;
	color: gold;
	border-radius: 5px;
	margin-right: auto;
}

h1{
	margin: 0;
}

</style>
