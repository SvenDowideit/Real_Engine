<!--
-- Copyright (c) 2017 Ned Hoy <nedhoy@gmail.com>
-- 
-- Permission is hereby granted, free of charge, to any person obtaining a copy
-- of this software and associated documentation files (the "Software"), to deal
-- in the Software without restriction, including without limitation the rights
-- to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
-- copies of the Software, and to permit persons to whom the Software is
-- furnished to do so, subject to the following conditions:
-- 
-- The above copyright notice and this permission notice shall be included in all
-- copies or substantial portions of the Software.
-- 
-- THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
-- IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
-- FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
-- AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
-- LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
-- OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
-- SOFTWARE.
-->

<template>
	<div class="maincontent" id="entities">
		<div v-if="loading">
			Loading...
		</div>

		<div v-else>
			<div class="row">
				<div class="col-md-2">
					<div class="lists">
						<h4>Current Entities</h4>
						<ul>
							<li v-for="entity in entities" v-bind:key="entity.id">
								<router-link :to="{ name: 'entities', params: { id: entity.id } }" @click.native="disableInstancing">
									{{ entity.title }}
								</router-link>
								<div>
									<button class="btn btn-xs">Add child</button>
									<button class="btn btn-xs" v-if="entity.children.length == 0" v-on:click="newInstance(entity.id)">Add instance</button>
								</div>
								<!--Tree View-->
								<!--<ul>-->
									<!--<li v-for="child in entity.children">-->
										<!--{{ child.title }}-->
									<!--</li>-->
								<!--</ul>-->
							</li>
						</ul>
						<button class="btn btn-primary" v-on:click="newEntity">New Entity</button>
						<br />
					</div>
				</div>
				<div class="col-md-10 inner-section" v-if="!instancing">
					<div v-if="id !== undefined">
						<h2>Virtual Entity</h2>
						<entity-edit :id="id"></entity-edit>
					</div>
					<div v-else>
						<h4> No entity selected</h4>
					</div>
				</div>
				<div class="col-md-10 inner-section" v-else>
					<div>
						<h2>Instance Entity for [INSERT VUE VAR]</h2>
						<!--<entity-edit :id="id"></entity-edit>-->
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import EntityEdit from "./EntityEdit.vue";

	export default {
		props: ['id'],

		data: () => ({
			loading: true,
			instancing: false
		}),

		components: {
			'entity-edit': EntityEdit,
		},

		methods: {
			newEntity: function() {
				this.$store.dispatch('newEntity')
					.then(entity => {
						this.$router.push({ name: 'entities', params: { id: entity.id } })
					})
					.catch(console.log)
			},

			newInstance(entityId) {
			    console.log("NEW INSTANCE -- PASSED IN VE ID: " + entityId);
				this.instancing = true;

				this.$store.dispatch('newInstance', { entityId })
					.then(instance => {
			        	//this.$router.push({ name: 'events', params: {id: sceneId, eventId: evt.id}})
					    console.log(instance);
					})
					.catch(console.log)
			},

			disableInstancing: function() {
			    this.instancing = false;
			},
		},

		computed: {
			entities() {
				return this.$store.state.entities.entities;
			},

			entity() {
				return this.$store.getters.entityById(this.$props.id);
			},
		},

		async created() {
			await this.$store.dispatch('fetchEntities');
			this.loading = false;
		}
	}
</script>

<style>
	#entity-view-wrapper {
		display: grid;
		grid-template-columns: 1fr 3fr;
	}
</style>
