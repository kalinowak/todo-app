<template>
  <nav class="toolbar">
  <div>
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
  </div>
  </nav>
  <router-view/>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700;900&display=swap');

$border: 2px solid
	rgba(
		$color: #153f36,
		$alpha: 0.35,
	);

$size1: 6px;
$size2: 12px;
$size3: 18px;
$size4: 24px;
$size5: 48px;

$backgroundColor: #F5F5F5;
$textColor: #0d221e;
$primaryColor: #153f36;
$secondTextColor: #d3f1e9;

body {
	margin: 0;
	padding: 0;
	font-family: 'Lato', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	background-color: $backgroundColor;
	color: $textColor;
	#app {
		max-width: 600px;
		margin-left: auto;
		margin-right: auto;
		padding: 20px;
		h1 {
			font-weight: bold;
			font-size: $size4;
			text-align: center;
		}
		form {
			display: flex;
			flex-direction: column;
			width: 100%;
			label {
				font-size: $size2;
				font-weight: bold;
			}
			input,
			button {
				height: $size5;
				box-shadow: none;
				outline: none;
				padding-left: $size2;
				padding-right: $size2;
				border-radius: $size1;
				font-size: 18px;
				margin-top: $size1;
				margin-bottom: $size2;
			}
			input {
				background-color: transparent;
				border: $border;
				color: inherit;
			}
		}
		button {
			cursor: pointer;
			background-color: $primaryColor;
			border: 1px solid $primaryColor;
			color: $secondTextColor;
			font-weight: bold;
			outline: none;
			border-radius: $size1;
		}
		h2 {
			font-size: 22px;
			border-bottom: $border;
			padding-bottom: $size1;
		}
		ul {
			padding: 10px;
			li {
				display: flex;
				justify-content: space-between;
				align-items: center;
				border: $border;
				padding: $size2 $size4;
				border-radius: $size1;
				margin-bottom: $size2;
				span {
					cursor: pointer;
				}
				.done {
					text-decoration: line-through;
				}
				button {
					font-size: $size2;
					padding: $size1;
				}
			}
		}
		h4 {
			text-align: center;
			opacity: 0.5;
			margin: 0;
		}
	}
}
</style>