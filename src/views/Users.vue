<template>
	<div class="page-main__inner">
		<section class="page-section">
			<UIError
				v-if="usersList.length === 0"
				:error="errorUsers"
			/>
			<UsersList
				v-else
				:users="usersList"
				:state-hidden="infoUserHidden"
			/>
			<UsersButtons
				@hide="hideInfoUser"
				@get-all="getUsers"
				@add-Inc-user="addUsers"
				@remove-all="removeAllUsers"
			/>
		</section>
	</div>
</template>

<script>
	import UsersList from '@/components/User/UserList';
	import UsersButtons from '@/components/User/UserButtons';
	import UIError from '@/components/UI/UIError';

	export default {
		name: 'Users',
		components: {
			UsersList,
			UsersButtons,
			UIError
		},
		props: {
			usersFetch: Array
		},
		data() {
			return {
				usersList: this.usersFetch,
				infoUserHidden: false,
				errorUsers: {
					message: 'Users not found',
					solution: "Click on the button 'GET USERS'"
				}
			};
		},
		watch: {
			usersFetch(newVal, oldVal) {
				if (newVal !== oldVal) {
					this.usersList = newVal;
				}
			},
			usersList(newVal, oldVal) {
				if (newVal !== oldVal) {
					this.usersList = newVal;
					this.$tools.setLocalStorage('users', this.usersList);
				}
			}
		},
		methods: {
			hideInfoUser() {
				this.infoUserHidden = !this.infoUserHidden;
			},
			async getUsers() {
				await this.$parent.setUsers();
			},
			async addUsers() {
				/*
				 * console.log('addUsers');
				 * const response = await fetch('https://randomuser.me/api/?results=1');
				 * const data = await response.json();
				 * console.log(data);
				 * this.usersList = this.usersList.push(data);
				 */
				await this.$parent.addUsers();
			},
			removeAllUsers() {
				this.usersList = [];
			}
		}
	};
</script>

<style lang="scss">
	.page-users {
		.page-body {
			padding-bottom: 7rem;
		}
	}
</style>
