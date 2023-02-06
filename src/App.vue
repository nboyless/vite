<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3 + Vite" />
  <div class="controls">
  <button id="cardnew" class="button">toggle clone card</button>
  <button id="cardtitle" class="button">change clone title</button>
  <button id="cardbg" class="button">toggle clone bg color</button>
</div>
<div id="cards" class="cards">
  <div id="card" class="card">
    <img src="https://media.istockphoto.com/id/1147544807/vector/thumbnail-image-vector-graphic.jpg?s=612x612&w=0&k=20&c=rnCKVbdxqkjlcs3xH87-9gocETqpspHFXu5dIGB4wuM=" id="image">
    <h2 id="title">Placeholder Card</h2>
    <p id="description">placeholder card description</p>
    <button id="details" class="button" onclick="toggleDescription()">details</button>
  </div>
</div>

</template>

<script setup>
import HelloWorld from './components/HelloWorld.vue'

const btn_cardnew = document.getElementById('cardnew');
const btn_cardtitle = document.getElementById('cardtitle');
const btn_cardbg = document.getElementById('cardbg');
const btn_details = document.getElementById('details');

btn_cardnew.addEventListener("click", (e) => { 
  if (document.getElementById('dupecard') == null) {
    const clone = document.getElementById('card').cloneNode(true);
    clone.setAttribute('id', 'dupecard');
    document.getElementById('cards').appendChild(clone);
    let btn_clonedetails = clone.children[3];
    btn_clonedetails.addEventListener("click", (e) => { 
      let desc = btn_clonedetails.previousElementSibling;
      (desc.style.display == 'none') ? (desc.style.display = '') : (desc.style.display = 'none');
    });
  }
  else {
    document.getElementById('cards').removeChild(document.getElementById('dupecard'));
  }
});
btn_cardtitle.addEventListener("click", (e) => { 
  if (document.getElementById('dupecard') != null) {
    const clone = document.getElementById('dupecard');
    title = prompt("Enter new title for the card");
    clone.children[1].innerHTML = title;
  }
});
btn_cardbg.addEventListener("click", (e) => { 
  if (document.getElementById('dupecard') != null) {
    const clone = document.getElementById('dupecard');
    color = prompt("Enter a color such as red, or green or white to return to default");
    clone.style.backgroundColor = color;
  }
});
btn_details.addEventListener("click", (e) => { 
  let desc = btn_details.previousElementSibling;
  (desc.style.display == 'none') ? (desc.style.display = '') : (desc.style.display = 'none');
});
// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap');

.controls {
  margin: 16px auto;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

.cards {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.3);
  max-width: 300px;
  margin: 16px 16px;
  text-align: center;
  font-family: 'Roboto Mono', monospace;
}
.card img {
  width: 100%;
}
.card p {
  padding: 16px;
}
.card>.button {
  display: none;
}

.button {
  background-color: #2895e8; /* Blue */
  border: none;
  color: white;
  padding: 8px 2vw;
  text-align: center;
  text-decoration: none;
  font-size: 14px;
  margin-bottom: 8px;
  cursor: pointer;
  border-radius: 4px;
  width: 25%;
  transform: scale(1);
  transition: 0.6s;
}
.button:hover, .button:focus {
  transform: scale(1.05);
  box-shadow: 0px 0px 48px 10px rgba(40,149,232,.7);
}

@media (min-width: 501px) and (max-width: 800px) {
  .card>.button {
    display: inline-block;
  }
}
@media (max-width: 500px) {
  .card {
    transform: scale(1.1);
  }
}

</style>
