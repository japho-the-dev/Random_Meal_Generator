Random Meal Generator
This API helps you to get meals data like recipes, meal Images, Country Origin of that particular meal, videos, its category, and description.

HTML Code
<div class="container">
 <div class="row text-center">
  <h3>
   Feeling hungry?
  </h3>
  <h5>Get a random meal by clicking below</h5>
  <button class="button-primary" id="get_meal">Get Meal 🍔</button>

 </div>
 <div id="meal" class="row meal"></div>
</div>
CSS
@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');

* {
 box-sizing: border-box;
}

body {
 display: flex;
 flex-direction: column;
 justify-content: center;
 align-items: center;
 padding: 30px 0;
 min-height: 100vh;
}

img {
 max-width: 100%;
}

p {
 margin-bottom: 5px;
}

h3 {
 margin: 0;
}

h5 {
 margin: 10px 0;
}

li {
 margin-bottom: 0;
}

.meal {
 margin: 20px 0;
}

.text-center {
 text-align: center;
}

.videoWrapper {
 position: relative;
 padding-bottom: 56.25%;
 padding-top: 25px;
 height: 0;
}

.videoWrapper iframe {
 position: absolute;
 top: 0;
 left: 0;
 width: 100%;
 height: 100%;
}











/* SOCIAL PANEL CSS */
.social-panel-container {
 position: fixed;
 right: 0;
 bottom: 80px;
 transform: translateX(100%);
 transition: transform 0.4s ease-in-out;
}

.social-panel-container.visible {
 transform: translateX(-10px);
}

.social-panel {
 background-color: #fff;
 border-radius: 16px;
 box-shadow: 0 16px 31px -17px rgba(0,31,97,0.6);
 border: 5px solid #001F61;
 display: flex;
 flex-direction: column;
 justify-content: center;
 align-items: center;
 font-family: 'Muli';
 position: relative;
 height: 169px;
 width: 370px;
 max-width: calc(100% - 10px);
}

.social-panel button.close-btn {
 border: 0;
 color: #97A5CE;
 cursor: pointer;
 font-size: 20px;
 line-height: 0;
 height: auto;
 padding: 0;
 position: absolute;
 top: 5px;
 right: 5px;
}

.social-panel button.close-btn:focus {
 outline: none;
}

.social-panel p {
 background-color: #001F61;
 border-radius: 0 0 10px 10px;
 color: #fff;
 font-size: 14px;
 line-height: 18px;
 padding: 2px 17px 6px;
 position: absolute;
 top: 0;
 left: 50%;
 margin: 0;
 transform: translateX(-50%);
 text-align: center;
 width: 235px;
}

.social-panel p i {
 margin: 0 5px;
}

.social-panel p a {
 color: #FF7500;
 text-decoration: none;
}

.social-panel h4 {
 margin: 20px 0;
 color: #97A5CE;
 font-family: 'Muli';
 font-size: 14px;
 line-height: 18px;
 text-transform: uppercase;
}

.social-panel ul {
 display: flex;
 list-style-type: none;
 padding: 0;
 margin: 0;
}

.social-panel ul li {
 margin: 0 10px;
}

.social-panel ul li a {
 border: 1px solid #DCE1F2;
 border-radius: 50%;
 color: #001F61;
 font-size: 20px;
 display: flex;
 justify-content: center;
 align-items: center;
 height: 50px;
 width: 50px;
 text-decoration: none;
}

.social-panel ul li a:hover {
 border-color: #FF6A00;
 box-shadow: 0 9px 12px -9px #FF6A00;
}

.floating-btn {
 border-radius: 26.5px;
 background-color: #001F61;
 border: 1px solid #001F61;
 box-shadow: 0 16px 22px -17px #03153B;
 color: #fff;
 cursor: pointer;
 font-family: 'Muli';
 font-size: 16px;
 line-height: 20px;
 height: auto;
 padding: 12px 20px;
 position: fixed;
 bottom: 20px;
 right: 20px;
 z-index: 999;
 text-transform: none;
}

button.floating-btn:focus {
 color: white;
 outline: none;
}

button.floating-btn:hover {
 background-color: #ffffff;
 color: #001F61;
}

.floating-text {
 background-color: #001F61;
 border-radius: 10px 10px 0 0;
 color: #fff;
 font-family: 'Muli';
 padding: 7px 15px;
 position: fixed;
 bottom: 0;
 left: 50%;
 transform: translateX(-50%);
}

.floating-text a {
 color: #FF7500;
 text-decoration: none;
}

@media screen and (max-width: 480px) {

 .social-panel-container.visible {
  transform: translateX(0px);
 }

 .floating-btn {
  right: 10px;
 }
}
Javascript Code
const get_meal_btn = document.getElementById('get_meal');
const meal_container = document.getElementById('meal');

get_meal_btn.addEventListener('click', () => {
 fetch('https://www.themealdb.com/api/json/v1/1/random.php')
  .then(res => res.json())
  .then(res => {
  createMeal(res.meals[0]);
 });
});

const createMeal = (meal) => {
 const ingredients = [];
 // Get all ingredients from the object. Up to 20
 for(let i=1; i<=20; i++) {
  if(meal[`strIngredient${i}`]) {
   ingredients.push(`${meal[`strIngredient${i}`]} - ${meal[`strMeasure${i}`]}`)
  } else {
   // Stop if no more ingredients
   break;
  }
 }

 const newInnerHTML = `
  <div class="row">
   <div class="columns five">
    <img src="${meal.strMealThumb}" alt="Meal Image">
    ${meal.strCategory ? `<p><strong>Category:</strong> ${meal.strCategory}</p>` : ''}
    ${meal.strArea ? `<p><strong>Area:</strong> ${meal.strArea}</p>` : ''}
    ${meal.strTags ? `<p><strong>Tags:</strong> ${meal.strTags.split(',').join(', ')}</p>` : ''}
    <h5>Ingredients:</h5>
    <ul>
     ${ingredients.map(ingredient => `<li>${ingredient}</li>`).join('')}
    </ul>
   </div>
   <div class="columns seven">
    <h4>${meal.strMeal}</h4>
    <p>${meal.strInstructions}</p>
   </div>
  </div>
  ${meal.strYoutube ? `
  <div class="row">
   <h5>Video Recipe</h5>
   <div class="videoWrapper">
    <iframe width="420" height="315"
    src="https://www.youtube.com/embed/${meal.strYoutube.slice(-11)}">
    </iframe>
   </div>
  </div>` : ''}
 `;

 meal_container.innerHTML = newInnerHTML;
}







// SOCIAL PANEL JS
const floating_btn = document.querySelector('.floating-btn');
const close_btn = document.querySelector('.close-btn');
const social_panel_container = document.querySelector('.social-panel-container');

floating_btn.addEventListener('click', () => {
 social_panel_container.classList.toggle('visible')
});

close_btn.addEventListener('click', () => {
 social_panel_container.classList.remove('visible')
});