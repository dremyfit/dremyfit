<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dremy Fit - Outfit Generator</title>
  <link rel="stylesheet" href="styles.css">
</head>

<body>
  <header>
    <h1>Dremy Fit - Outfit Generator</h1>
  </header>
  <main>
    <div class="outfit-display">
      <!-- Outfit items will be displayed here -->
    </div>
    <button id="generateOutfit">Generate Outfit</button>
  </main>
  <script src="script.js"></script>
</body>

</html>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

header {
  background-color: #f0f0f0;
  padding: 20px;
  text-align: center;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 20px;
}

.outfit-display {
  /* Style for displayed outfit */
}

button {
  padding: 10px 20px;
  margin-top: 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
/* ... (Previous CSS) ... */

.outfit-display {
  text-align: center;
  margin-top: 20px;
}

.outfit-item {
  margin-bottom: 10px;
}

.color-options {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.color-box {
  width: 30px;
  height: 30px;
  border: 1px solid #000;
  margin: 0 5px;
  cursor: pointer;
}

.selected-color {
  border-width: 3px;
} // Define outfit items (You might have more categories and items)
const tops = ['Blouse', 'T-shirt', 'Sweater'];
const bottoms = ['Skirt', 'Pants', 'Shorts'];
const accessories = ['Necklace', 'Earrings', 'Hat'];
// Add more items or categories as needed

function generateRandomItem(items) {
  return items[Math.floor(Math.random() * items.length)];
}

function generateOutfit() {
  const top = generateRandomItem(tops);
  const bottom = generateRandomItem(bottoms);
  const accessory = generateRandomItem(accessories);

  const outfitDisplay = document.querySelector('.outfit-display');
  outfitDisplay.innerHTML = `
    <p>Top: ${top}</p>
    <p>Bottom: ${bottom}</p>
    <p>Accessory: ${accessory}</p>
  `;
}

document.getElementById('generateOutfit').addEventListener('click', generateOutfit);
// Define outfit items with colors
const tops = [
  { name: 'Blouse', colors: ['Red', 'Blue', 'Yellow'] },
  { name: 'T-shirt', colors: ['Black', 'White', 'Green'] },
  { name: 'Sweater', colors: ['Pink', 'Purple', 'Gray'] }
];
const bottoms = [
  { name: 'Skirt', colors: ['Blue', 'Black', 'Red'] },
  { name: 'Pants', colors: ['Black', 'Gray', 'Brown'] },
  { name: 'Shorts', colors: ['White', 'Green', 'Yellow'] }
];
const accessories = [
  { name: 'Necklace', colors: ['Silver', 'Gold'] },
  { name: 'Earrings', colors: ['Gold', 'Diamond'] },
  { name: 'Hat', colors: ['Black', 'Brown'] }
];
// Add more items or categories as needed

function generateRandomItem(items) {
  const randomItem = items[Math.floor(Math.random() * items.length)];
  const randomColor = randomItem.colors[Math.floor(Math.random() * randomItem.colors.length)];
  return { name: randomItem.name, color: randomColor };
}

function displayOutfit(outfit) {
  const outfitDisplay = document.querySelector('.outfit-display');
  outfitDisplay.innerHTML = '';

  for (const item in outfit) {
    const outfitItem = outfit[item];
    const div = document.createElement('div');
    div.classList.add('outfit-item');
    div.innerHTML = `<p>${item}: ${outfitItem.name} (${outfitItem.color})</p>`;
    outfitDisplay.appendChild(div);
  }
}

function generateOutfit() {
  const top = generateRandomItem(tops);
  const bottom = generateRandomItem(bottoms);
  const accessory = generateRandomItem(accessories);

  displayOutfit({ Top: top, Bottom: bottom, Accessory: accessory });
}

document.getElementById('generateOutfit').addEventListener('click', generateOutfit);

function selectColor(item, color) {
  const items = {
    Top: tops,
    Bottom: bottoms,
    Accessory: accessories
  };

  items[item] = items[item].map(i => ({ ...i, selected: i.name === items[item].find(it => it.name === item).name && i.color === color }));
  displayOutfit({ [item]: items[item].find(i => i.selected) });
}

// Display color options
const colorOptions = document.createElement('div');
colorOptions.classList.add('color-options');
for (const category in { Top: tops, Bottom: bottoms, Accessory: accessories }) {
  const categoryColors = document.createElement('div');
  for (const item of { Top: tops, Bottom: bottoms, Accessory: accessories }[category]) {
    categoryColors.innerHTML += item.colors.map(color =>
      `<div class="color-box" style="background-color: ${color}" onclick="selectColor('${item.name}', '${color}')"></div>`
    ).join('');
  }
  colorOptions.appendChild(categoryColors);
}

document.querySelector('main').appendChild(colorOptions);


![image](https://github.com/dremyfit/dremyfit/assets/152036570/824d8682-d5ce-4033-9c94-e040d95c476c)
