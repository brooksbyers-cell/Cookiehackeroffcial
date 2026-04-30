// Initial Game State
let cookies = 0;
let autoClickers = 0;
let cursorPrice = 15;
let grandmaPrice = 100;
let cookiesPerSecond = 0;

// DOM Elements
const cookieDisplay = document.getElementById('cookie-count');
const cpsDisplay = document.getElementById('cps-count');
const cookieBtn = document.getElementById('cookie-button');
const cursorBtn = document.getElementById('buy-cursor');

// 1. Manual Click Function
cookieBtn.addEventListener('click', () => {
    cookies++;
    updateDisplay();
});

// 2. Buy Upgrade Function
cursorBtn.addEventListener('click', () => {
    if (cookies >= cursorPrice) {
        cookies -= cursorPrice;
        autoClickers += 0.1; // Each cursor adds 0.1 cookies per second
        cursorPrice = Math.floor(cursorPrice * 1.15); // Increase price for next one
        
        cursorBtn.innerText = `Buy Cursor (Cost: ${cursorPrice})`;
        updateDisplay();
    }
});

// 3. Update the UI
function updateDisplay() {
    cookieDisplay.innerText = Math.floor(cookies);
    cpsDisplay.innerText = autoClickers.toFixed(1);
}

// 4. The Game Loop (Runs every second)
setInterval(() => {
    cookies += autoClickers;
    updateDisplay();
}, 1000);
