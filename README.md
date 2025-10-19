# TEAMSPADE
TEAMSPADE
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Team Spade - Virtual Betting Site (Presentation)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&family=Noto+Sans+KR:wght@400;700&display=swap" rel="stylesheet">
    
    <style>
        /* --- CSS Styles --- */
        :root {
            --accent-color: #A855F7; /* Violet-500: Accent Color (보라색 유지) */
            --bg-dark: #121212; /* Background */
            --card-bg: #1F1F1F; /* Card Background */
        }
        body {
            font-family: 'Inter', 'Noto Sans KR', sans-serif;
            background-color: var(--bg-dark);
            color: #E0E0E0;
            display: flex;
            justify-content: center;
            align-items: flex-start; 
            min-height: 100vh;
            padding: 20px; 
            box-sizing: border-box;
        }
        
        .app-container {
            max-width: 400px;
            width: 100%;
            background: var(--bg-dark);
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
            padding: 24px;
            margin-top: 40px; 
            margin-bottom: 40px; 
        }

        @media (max-width: 480px) {
            body {
                padding: 10px;
            }
            .app-container {
                margin-top: 20px;
                margin-bottom: 20px;
            }
        }
        
        .fade-in-out {
            opacity: 0;
            transform: translateY(10px);
            animation: fadeIn 0.5s forwards;
        }
        @keyframes fadeIn {
            to { opacity: 1; transform: translateY(0); }
        }

        .click-effect {
            transition: transform 0.1s ease;
        }
        .click-effect:active {
            transform: scale(0.98);
        }

        /* 스페이드 아이콘: 보라색으로 고정 */
        .spade-icon::before {
            content: '\2660'; 
            line-height: 1;
        }
        /* 스페이드 아이콘 폰트 색상을 직접 보라색 변수로 지정 */
        .logo-with-icon .spade-icon {
            color: var(--accent-color); /* #A855F7 */
        }

        .choice-icon {
            font-family: 'Inter', sans-serif;
            font-weight: 900;
            color: var(--accent-color); /* 보라색 */
            display: block;
        }

        .choice-card {
            background-color: var(--card-bg);
            border: 2px solid #333;
            padding: 20px;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            text-align: center;
        }
        .choice-card:hover {
            border-color: var(--accent-color);
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(168, 85, 247, 0.3);
        }
        .choice-card.selected {
            border-color: #4ADE80; /* Green */
            box-shadow: 0 0 20px rgba(74, 222, 128, 0.5);
            transform: scale(1.05);
        }

        .fade-out {
            opacity: 0 !important;
            transform: translateY(10px) !important;
            transition: opacity 0.3s, transform 0.3s;
        }

        #loginScreen .app-container {
            animation: none; 
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.7);
            margin: 0 20px; 
        }
        #loginScreen {
            padding: 0 20px;
        }
    </style>
</head>
<body>

<div id="loginScreen" class="fixed inset-0 bg-black z-50 flex items-center justify-center fade-in-out">
    <div class="app-container p-8 bg-zinc-900 shadow-2xl">
        <div class="logo-with-icon mb-10 text-center">
            <span class="spade-icon text-5xl text-violet-500 mr-2"></span>
            <h1 class="text-4xl font-black text-white inline-block align-middle">TEAM SPADE</h1>
        </div>

        <h2 id="loginHeader" class="text-xl font-bold mb-6 text-gray-300 text-center">Account Access</h2>
        
        <input type="text" id="userId" placeholder="ID" class="w-full p-4 bg-zinc-800 rounded-lg mb-4 text-white focus:outline-none focus:ring-2 focus:ring-violet-500 border border-transparent hover:border-violet-500 transition">
        <input type="password" id="userPin" placeholder="PIN (4 digits minimum)" maxlength="4" class="w-full p-4 bg-zinc-800 rounded-lg mb-6 text-white focus:outline-none focus:ring-2 focus:ring-violet-500 border border-transparent hover:border-violet-500 transition">

        <button id="loginButton" class="w-full py-4 bg-violet-600 hover:bg-violet-700 text-white font-extrabold rounded-xl transition-all click-effect shadow-violet-500/50 shadow-lg">
            Access
        </button>
        <p id="loginHint" class="text-xs text-center mt-4 text-gray-500">Virtual login for presentation purposes.</p>
    </div>
</div>

<div id="app" class="app-container fade-in-out hidden">
    <header class="flex justify-between items-center mb-6">
        <div class="logo-with-icon flex-shrink-0">
            <span class="spade-icon text-2xl text-violet-500 mr-1"></span>
            <h1 class="text-2xl font-black text-white inline-block align-middle">TEAM SPADE</h1>
        </div>
        <div class="text-right flex-shrink-0 ml-4">
            <p class="text-xl font-extrabold text-white whitespace-nowrap" id="currentBalance">50,000 RBX</p>
            <p class="text-xs text-gray-400">Balance (Virtual)</p>
        </div>
    </header>

    <main id="mainGame" class="fade-in-out" style="animation-delay: 0.1s;">
        <h2 class="text-3xl font-extrabold mb-8 text-center">RBX Challenge💰</h2>

        <div class="p-5 bg-zinc-800 rounded-xl mb-6 shadow-lg">
            <label for="betAmount" class="block text-sm font-semibold mb-2 text-gray-300">Bet Amount (RBX)</label>
            <div class="flex items-center">
                <input type="number" id="betAmount" value="1000" min="1000" step="1000" class="w-full text-2xl p-2 bg-transparent border-b-2 border-violet-500 focus:outline-none focus:border-violet-300 transition-colors click-effect text-white">
                <span class="text-xl ml-2 text-violet-400">RBX</span>
            </div>
            <p class="text-xs text-red-400 mt-2 hidden" id="balanceError">Insufficient Balance.</p>
        </div>

        <div id="choiceSelection" class="grid grid-cols-3 gap-4 mb-8">
            <div class="choice-card click-effect fade-in-out" data-choice="rock" style="animation-delay: 0.2s;">
                <span class="text-5xl choice-icon">R</span>
                <p class="font-bold mt-2">Rock</p>
            </div>
            <div class="choice-card click-effect fade-in-out" data-choice="scissors" style="animation-delay: 0.3s;">
                <span class="text-5xl choice-icon">S</span>
                <p class="font-bold mt-2">Scissors</p>
            </div>
            <div class="choice-card click-effect fade-in-out" data-choice="paper" style="animation-delay: 0.4s;">
                <span class="text-5xl choice-icon">P</span>
                <p class="font-bold mt-2">Paper</p>
            </div>
        </div>

        <div class="text-center">
            <button id="betButton" class="w-full py-4 bg-violet-600 hover:bg-violet-700 text-white font-extrabold rounded-xl transition-all click-effect shadow-violet-500/50 shadow-lg" disabled>
                Select a Choice to Bet
            </button>
            <p id="resultMessage" class="mt-4 text-lg font-semibold text-center hidden"></p>
        </div>

    </main>
</div>

<div id="transferModal" class="fixed inset-0 bg-black bg-opacity-70 z-40 hidden items-center justify-center">
    <div id="modalContent" class="bg-zinc-800 p-6 rounded-xl w-11/12 max-w-sm fade-in-out">
        <h3 class="text-2xl font-bold mb-4">RBX Transfer/Balance Check (Virtual)</h3>
        <p class="text-sm text-gray-400 mb-4">Current Balance: <span class="font-bold text-violet-400" id="modalBalance">50,000 RBX</span></p>
        
        <label for="transferId" class="block text-sm font-semibold mb-1 text-gray-300">Recipient ID</label>
        <input type="text" id="transferId" placeholder="Enter ID" class="w-full p-3 bg-zinc-700 rounded-lg mb-4 text-white focus:outline-none focus:ring-2 focus:ring-violet-500">
        
        <label for="transferAmount" class="block text-sm font-semibold mb-1 text-gray-300">Transfer Amount (RBX)</label>
        <input type="number" id="transferAmount" value="0" min="1" class="w-full p-3 bg-zinc-700 rounded-lg mb-6 text-white focus:outline-none focus:ring-2 focus:ring-violet-500">
        
        <div class="flex justify-end space-x-3">
            <button class="py-2 px-4 bg-gray-600 hover:bg-gray-700 rounded-lg text-white font-semibold click-effect" onclick="closeTransferModal()">Cancel</button>
            <button class="py-2 px-4 bg-violet-600 hover:bg-violet-700 rounded-lg text-white font-semibold click-effect" onclick="handleTransfer()">Execute Transfer</button>
        </div>
    </div>
</div>

<button class="fixed bottom-4 left-4 py-2 px-4 bg-gray-700 hover:bg-gray-600 rounded-lg text-white font-semibold click-effect fade-in-out hidden" id="transferButton" style="z-index: 30;">
    ⚙️ More/Settings
</button>

<script>
    /* --- JavaScript Code --- */

    // --- Audio Setup (Completely Removed to prevent errors) ---
    // 오디오 관련 변수와 함수를 모두 제거하여 오류를 방지합니다.

    // --- Account and Balance Management ---
    const BALANCE_KEY = 'spade_rbs_balance_v2'; 
    const ACCOUNT_KEY = 'spade_user_id_v2';
    const PIN_KEY = 'spade_user_pin_v2';
    const INITIAL_BALANCE = 50000; 

    let balance = loadBalance();
    let storedId = localStorage.getItem(ACCOUNT_KEY);
    let storedPin = localStorage.getItem(PIN_KEY);

    function loadBalance() {
        const storedBalance = localStorage.getItem(BALANCE_KEY);
        if (storedBalance) {
            return parseInt(storedBalance);
        }
        localStorage.setItem(BALANCE_KEY, INITIAL_BALANCE);
        return INITIAL_BALANCE;
    }

    function updateBalance(amount) {
        balance += amount;
        localStorage.setItem(BALANCE_KEY, balance);
        const formattedBalance = formatBalance(balance) + ' RBX';
        
        const currentBalanceEl = document.getElementById('currentBalance');
        if (currentBalanceEl) {
            currentBalanceEl.textContent = formattedBalance;
        }
        const modalBalanceEl = document.getElementById('modalBalance');
        if (modalBalanceEl) {
            modalBalanceEl.textContent = formattedBalance;
        }

        if (balance <= 0) {
            if (currentBalanceEl) currentBalanceEl.classList.add('text-red-500');
            if (currentBalanceEl) currentBalanceEl.classList.remove('text-white');
        } else {
            if (currentBalanceEl) currentBalanceEl.classList.remove('text-red-500');
            if (currentBalanceEl) currentBalanceEl.classList.add('text-white');
        }
    }

    function formatBalance(num) {
        return Math.round(num).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }

    // --- Login System Logic ---
    const loginScreen = document.getElementById('loginScreen');
    const loginButton = document.getElementById('loginButton');
    const mainApp = document.getElementById('app');
    const transferButton = document.getElementById('transferButton');
    const userIdInput = document.getElementById('userId');
    const userPinInput = document.getElementById('userPin');
    const loginHeader = document.getElementById('loginHeader');
    const loginHint = document.getElementById('loginHint');

    // Pre-check and update login screen UI
    function initializeLoginUI() {
        storedId = localStorage.getItem(ACCOUNT_KEY);
        storedPin = localStorage.getItem(PIN_KEY);

        if (storedId && storedPin) {
            // Account Exists: Prompt for Login
            userIdInput.value = storedId;
            userIdInput.setAttribute('readonly', 'readonly'); 
            loginHeader.textContent = "Welcome Back, " + storedId;
            loginButton.textContent = "Access Account";
            loginHint.textContent = "Enter your PIN (4 digits) to access your personalized account.";
            userPinInput.setAttribute('type', 'password'); 
            userIdInput.style.pointerEvents = 'none'; 
        } else {
            // No Account: Prompt for Setup
            loginHeader.textContent = "Create New Account";
            loginButton.textContent = "Set ID & PIN";
            loginHint.textContent = "Set your personal ID and PIN. This cannot be changed later.";
            userPinInput.setAttribute('type', 'text'); 
        }
        
        updateBalance(0); 
    }

    loginButton.addEventListener('click', () => {
        // initializeAudio() 호출 제거

        const enteredId = userIdInput.value.trim();
        const enteredPin = userPinInput.value.trim();

        if (enteredId.length === 0 || enteredPin.length < 4) {
            alert("ID must not be empty, and PIN must be 4 digits or more.");
            return;
        }

        if (!storedId) {
            // Account Setup
            localStorage.setItem(ACCOUNT_KEY, enteredId);
            localStorage.setItem(PIN_KEY, enteredPin);
            storedId = enteredId;
            storedPin = enteredPin;
            login();
        } else {
            // Login Attempt
            if (enteredId === storedId && enteredPin === storedPin) {
                login();
            } else {
                alert("Incorrect ID or PIN. Please try again.");
                userPinInput.value = ''; 
            }
        }
    });

    function login() {
        loginScreen.style.opacity = 0;
        loginScreen.style.transition = 'opacity 0.5s ease-out';
        
        setTimeout(() => {
            loginScreen.classList.add('hidden');
            mainApp.classList.remove('hidden');
            transferButton.classList.remove('hidden');
            updateBalance(0); 
        }, 500);
    }

    // Run initial UI setup
    initializeLoginUI();

    // --- UI/UX Features (Click sound effect, but no audio file call) ---
    document.querySelectorAll('.click-effect').forEach(element => {
        element.addEventListener('click', () => {
            // 오디오 대신 콘솔 로그만 남기거나 아무 동작도 하지 않음
            console.log("Click detected.");
        });
    });

    // --- Betting Game Logic ---
    const choiceCards = document.querySelectorAll('.choice-card');
    const betButton = document.getElementById('betButton');
    const betAmountInput = document.getElementById('betAmount');
    const resultMessage = document.getElementById('resultMessage');
    let selectedChoice = null;

    // Rock-Paper-Scissors Choice Handling
    choiceCards.forEach(card => {
        card.addEventListener('click', () => {
            if (betButton.disabled === false && betButton.textContent.includes('Rebet')) return;

            choiceCards.forEach(c => c.classList.remove('selected'));
            card.classList.add('selected');
            selectedChoice = card.getAttribute('data-choice');
            
            checkBetValidity();
        });
    });

    // Bet Amount Validity Check and Button Text Update
    function checkBetValidity() {
        const bet = parseInt(betAmountInput.value);
        const errorElement = document.getElementById('balanceError');

        if (isNaN(bet) || bet < 1000) {
            betAmountInput.value = 1000;
        }

        if (bet > balance) {
            errorElement.classList.remove('hidden');
            betButton.disabled = true;
            betButton.textContent = "Insufficient Balance";
            return;
        } else {
            errorElement.classList.add('hidden');
        }
        
        if (selectedChoice) {
            betButton.disabled = false;
            betButton.textContent = `Bet ${formatBalance(parseInt(betAmountInput.value))} RBX`;
        } else {
            betButton.disabled = true;
            betButton.textContent = "Select Rock-Paper-Scissors";
        }
    }

    // Handle Bet Amount changes
    betAmountInput.addEventListener('input', checkBetValidity);
    betAmountInput.addEventListener('change', checkBetValidity);

    // Execute Final Bet
    betButton.addEventListener('click', () => {
        if (!selectedChoice) return;
        
        const betAmount = parseInt(betAmountInput.value);
        if (betAmount > balance) return;
        
        betButton.disabled = true;
        betButton.textContent = "Awaiting Result...";
        resultMessage.classList.add('hidden');
        
        // Directly proceed to game result after a short delay for tension
        setTimeout(() => {
            processGameResult(selectedChoice, betAmount, ['rock', 'scissors', 'paper']);
        }, 500); 
    });

    // --- Game Core Logic (Result Processing - Win Chance Biased) ---
    function processGameResult(userChoice, betAmount, choices) {
        
        // Player's chance to win: 36.3% (33.3% + 3% increase)
        const WIN_CHANCE = 0.363; 
        
        let computerChoice = '';

        if (Math.random() < WIN_CHANCE) {
            // Player is determined to WIN: Computer chooses the losing hand.
            if (userChoice === 'rock') computerChoice = 'scissors';
            else if (userChoice === 'scissors') computerChoice = 'paper';
            else if (userChoice === 'paper') computerChoice = 'rock';
        } else {
            // Player is determined to DRAW or LOSE (63.7% chance): 
            const losingHandMap = {
                'rock': 'paper', // Rock loses to Paper
                'scissors': 'rock', // Scissors loses to Rock
                'paper': 'scissors' // Paper loses to Scissors
            };
            
            const drawingHand = userChoice;
            
            // Randomly pick between the computer's "Losing" hand (Loses to player) 
            // and "Drawing" hand (Draws with player) to split the 63.7% chance.
            if (Math.random() < 0.5) { 
                computerChoice = drawingHand; // Draw (Computer plays the same hand)
            } else {
                computerChoice = losingHandMap[userChoice]; // Lose (Computer plays the winning hand against player's choice)
            }
        }

        // --- Determine Final Result ---
        let result = ''; 

        if (userChoice === computerChoice) {
            result = 'draw';
        } else if (
            (userChoice === 'rock' && computerChoice === 'scissors') ||
            (userChoice === 'scissors' && computerChoice === 'paper') ||
            (userChoice === 'paper' && computerChoice === 'rock')
        ) {
            result = 'win';
        } else {
            result = 'lose';
        }

        displayResult(result, betAmount, computerChoice);
    }

    function displayResult(result, betAmount, computerChoice) {
        let message = '';

        const choiceMap = { 'rock': 'Rock', 'scissors': 'Scissors', 'paper': 'Paper' };
        
        if (result === 'win') {
            updateBalance(betAmount);
            message = `**[WIN]** Computer: ${choiceMap[computerChoice]}. **+${formatBalance(betAmount)} RBX** Acquired!`;
            resultMessage.className = 'mt-4 text-xl font-extrabold text-green-400 text-center fade-in-out';
        } else if (result === 'lose') {
            updateBalance(-betAmount);
            message = `**[LOSE]** Computer: ${choiceMap[computerChoice]}. **-${formatBalance(betAmount)} RBX** Deducted.`;
            resultMessage.className = 'mt-4 text-xl font-extrabold text-red-500 text-center fade-in-out';
            if (balance <= 0) {
                 message += "<br>💸 **All Balance Depleted!**";
            }
        } else {
            message = `**[DRAW]** Computer: ${choiceMap[computerChoice]}. Bet Amount Maintained.`;
            resultMessage.className = 'mt-4 text-xl font-extrabold text-yellow-400 text-center fade-in-out';
        }

        resultMessage.innerHTML = message;
        resultMessage.classList.remove('hidden');
        betButton.disabled = false;
        betButton.textContent = "Rebet";
        selectedChoice = null; 
        choiceCards.forEach(c => c.classList.remove('selected'));

        // 오디오 재생 코드 제거
    }

    // --- Virtual Transfer Modal Feature (More/Settings) ---
    const transferModal = document.getElementById('transferModal');
    const modalContent = document.getElementById('modalContent');

    transferButton.addEventListener('click', openTransferModal);

    function openTransferModal() {
        updateBalance(0); 
        transferModal.classList.remove('hidden');
        transferModal.style.display = 'flex';
        modalContent.classList.remove('fade-out'); 
        modalContent.classList.add('fade-in-out');
    }

    function closeTransferModal() {
        modalContent.classList.add('fade-out');
        modalContent.classList.remove('fade-in-out');
        setTimeout(() => {
            transferModal.classList.add('hidden');
            transferModal.style.display = 'none';
        }, 300);
    }

    function handleTransfer() {
        const amount = parseInt(document.getElementById('transferAmount').value);
        const id = document.getElementById('transferId').value;

        if (amount > 0 && id.length > 0) {
            if (amount > balance) {
                alert("Insufficient transfer balance!");
                return;
            }
            updateBalance(-amount);
            alert(`[Virtual Transfer Complete] ${formatBalance(amount)} RBX successfully sent to ${id}!`);
            closeTransferModal();
            checkBetValidity();
        } else {
            alert("Please accurately enter the Recipient ID and Transfer Amount.");
        }
    }
</script>
</body>
</html>
