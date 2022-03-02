<template app>
  <nav class="toolbar">My<span class="font-weight-bold">Todo</span></nav>
  <div class="container">
  <div class="left">
    <!-- Left side -->
    <h2>To Do List</h2>
    <ul>
      <li
        v-for="(todo, index) in todos"
        :key="index"
        @click="doneTodo(todo)"
      >
        <span v-if="todo.done" class="material-icons checkbox">check_box</span>
        <span v-else class="material-icons checkbox">check_box_outline_blank</span>

        <span :class="{ done: todo.done }" class="content">
          <ul>
            <li class="name">{{ todo.name }}</li>
            <li v-if="todo.description" class="description">{{ todo.description }}</li>
          </ul>
        </span>
        <button @click="removeTodo(index)">
          <i class="material-icons">delete_outlined</i>
        </button>
      </li>
    </ul>
    
    <h4 v-if="todos.length === 0">No items to do!</h4>
  </div>

  <div class="right">
    <!-- Right side -->
    <h1>Add New Item</h1>
    <form @submit.prevent="addTodo()" class="flex flex-column justify-center width-50 align-center">
      <label>New ToDo</label>
      <input v-model="newTodo" type="text" name="newTodo" autocomplete="off" required />

      <label>Description</label>
      <input v-model="newDescription" type="text" name="newDescription" autocomplete="off">
      <button>Add ToDo</button>
    </form>
  </div>
</div>
</template>

<script>
import { ref } from 'vue';

export default {
  components: {},
  setup() {
    const newTodo = ref('');
    const newDescription = ref('');

    const defaultData = [{
      done: false,
      name: 'Create a Todo App',
      description: 'My first Todo app using Vue JS.'
    }];

    const todosData = JSON.parse(localStorage.getItem('todos')) || defaultData;
    const todos = ref(todosData);

    function addTodo() {
      if (newTodo.value) {
        todos.value.push({
          done: false,
          name: newTodo.value,
          description: newDescription.value
        });
        newTodo.value = '';
        newDescription.value = '';
      }
      saveData();
    }

    function doneTodo(todo) {
      todo.done = !todo.done;
      saveData();
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
      saveData();
    }

    function saveData() {
      const storageData = JSON.stringify(todos.value);
      localStorage.setItem('todos', storageData);
    }

    return {
      todos,
      newTodo,
      newDescription,
      addTodo,
      doneTodo,
      removeTodo,
      saveData
    }
  }
};

</script>


<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700;900&display=swap');

$border: 2px solid
	rgba(
		$color: #CF8BA3,
		$alpha: 0.35,
	);

$bodyText: 16px;
$labelText: 14px;
$h1: 32px;
$h2: 24px;
$h3: 20px;
$h4: 16px;
$h5: 12px;

$btnmargin: 15px 20px;

$size1: 6px;
$size2: 12px;
$size3: 18px;
$size4: 24px;
$size5: 48px;

$bgcolor: #fff;
$btntext: #fff;
$textColor: #1e182d;
$primaryColor: #6E44FF;
$secondTextColor: #634f94;
$bordercolor: #efefef;

$majorelle-blue: #6E44FF;
$medium-turquoise: #60E1E0;

body {
	margin: 0;
	padding: 0;
	font-family: 'Lato', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	background-color: $bgcolor;
	color: $textColor;
    nav.toolbar {
      width: 100%;
      background-color: $textColor;
      margin: 0;
      padding: 15px 20px;
      color: white;
      font-size: $h2;
      box-shadow: 0px 1px 8px $secondTextColor;
    }

    .container {
      display: flex;
      margin: 50px;
      flex-wrap: wrap-reverse;
      align-items: flex-start;

      .left {
        flex: 2;
        margin: 0 40px;
        margin-bottom: auto;

        span.material-icons.checkbox {
          color: $primaryColor;
        }

        li.name {
          font-weight: bold;
          font-size: $h3;
          text-align: left;
          border: none;
          padding-bottom: 8px;
          box-shadow: none;
        }

        li.description {
          font-weight: regular;
          font-size: $h4;
          text-align: left;
          border: none;
          padding-top: 0;
          box-shadow: none;
        }

        button {
          color: white;
          font-size: 16px;
          font-weight: bold;
          margin-left: auto;
          border-radius: 50%;
          padding: 19px 10px;
          cursor: pointer;
          background-color: $primaryColor;
          border: 1px solid $primaryColor;
          text-align: center;
          word-wrap: none;

          i {
            width: 50%;
            margin: auto;
          }
        }

        button:hover {
          border: 1px solid $secondTextColor;
        }
      }

      .right {
        flex: 1;
        margin: 0 40px;
        padding: 20px 30px;
        border: 2px solid $bordercolor;
        border-radius: 10px;
        box-shadow: 0 3px 10px rgb(0 0 0 / 0.1);
        max-height: 350px;
        margin-bottom: auto;
      }
    }

    .font-weight-bold {
      font-weight: bold;
    }

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
        color: $primaryColor;
        margin-top: $size4;
			}

			input,
			button {
				height: $size5;
				box-shadow: none;
				outline: none;
				padding-left: $size2;
				padding-right: $size2;
				font-size: $size3;
				margin-top: $size1;
				margin-bottom: $size2;
			}

			input {
				background-color: transparent;
				border: 2px solid $bordercolor;
				color: $textColor;
        border-radius: 4px;
			}

      button {
        cursor: pointer;
        background-color: $primaryColor;
        border: 1px solid $primaryColor;
        color: $btntext;
        font-weight: bold;
        outline: none;
        border-radius: $size1;
        text-align: center;
      }

      input:focus {
        border: 2px solid $primaryColor;
      }
		}

		h2 {
			font-size: $h1;
			border-bottom: 2px solid $bordercolor;
			padding-bottom: $size1;
		}

		ul {
			padding: 10px;
			li {
				display: flex;
				align-items: center;
				border: 2px solid $bordercolor;
				padding: $size2 $size4;
				border-radius: $size1;
				margin-bottom: $size2;
				span {
					cursor: pointer;
				}
				.done {
					text-decoration: line-through;
				}
			}
		}
		h4 {
			text-align: center;
			opacity: 0.5;
			margin: 0;
		}
	}

.material-icons {
  font-family: 'Material Icons';
  font-weight: normal;
  font-style: normal;
  font-size: 24px;  /* Preferred icon size */
  display: inline-block;
  line-height: 1;
  text-transform: none;
  letter-spacing: normal;
  word-wrap: normal;
  white-space: nowrap;
  direction: ltr;

  /* Support for all WebKit browsers. */
  -webkit-font-smoothing: antialiased;
  /* Support for Safari and Chrome. */
  text-rendering: optimizeLegibility;

  /* Support for Firefox. */
  -moz-osx-font-smoothing: grayscale;

  /* Support for IE. */
  font-feature-settings: 'liga';
}
</style>