<template>
	<div class="bulma">
		<h2 class="bulma-title">Component - Card</h2>
		<card>
			<template slot="name">Robert Cooper</template>
			<template slot="handle">@RobertCooper_RC</template>
			This card is a component made with Bulma. I'm using Vue and named slots to put together to content inside of this card component.
      <a>@bulmaio</a>&nbsp;<a href="#">#css</a>&nbsp;<a href="#">#responsive</a>
		</card>
		<made-with-bulma/>
		<h2 class="bulma-title">Component - Message</h2>
		<message :displayMessage="displayMessage" @close="displayMessage = false">
			<template slot="title">Message Title</template>
			This is the content of the message. The styling applied to the message is used on message components that convey information to a website's users. Blue is the colour commonly associated with these types of information boxes.
		</message>
		<button v-if="!displayMessage" class="button is-info" @click="displayMessage = true">Display Message</button>
		<made-with-bulma/>
		<h2 class="bulma-title">Component - Dropdown</h2>
		<dropdown :class="{'is-active': showDropdown}" @toggle="showDropdown = !showDropdown">
		</dropdown>
		<made-with-bulma/>
	</div>
</template>

<script>
	import Card from './Card'
	import Message from './Message'
	import Dropdown from './Dropdown'
	import MadeWithBulma from './MadeWithBulma'
	export default {
  name: 'hello',
	components: { Card, Message, Dropdown, MadeWithBulma },
  data () {
    return {
     displayMessage: true,
		 showDropdown: false
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.bulma {
		margin-top: 40px;
	}
	.bulma-title {
		font-weight: normal;
		font-size: 1.4rem;
		margin-bottom: 20px;
		font-weight: bold;
	}
	ul {
		list-style-type: none;
		padding: 0;
	}

	li {
		display: inline-block;
		margin: 0 10px;
	}
</style>