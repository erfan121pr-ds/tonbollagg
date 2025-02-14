<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TANBLA Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            text-align: center;
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: #333;
        }
        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            margin: 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
        .cards {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 20px;
        }
        .card {
            width: 100px;
            height: 150px;
            background-color: #e9ecef;
            border: 2px solid #ccc;
            border-radius: 5px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            font-weight: bold;
            color: #333;
        }
        .winner {
            background-color: #d4edda;
            color: #155724;
            padding: 10px;
            border-radius: 5px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>TANBLA Game</h1>
        <button id="startGame">Start Game</button>
        <button id="buyCard">Buy Card (1 TON)</button>
        <button id="checkCards">Check Cards</button>
        <button id="showWinners">Show Winners</button>

        <div class="cards" id="cardsContainer"></div>

        <div id="winnerMessage" class="winner" style="display: none;">
            Congratulations! You are a winner!
        </div>
    </div>

    <script>
        // Simulated game logic
        const cardsContainer = document.getElementById('cardsContainer');
        const winnerMessage = document.getElementById('winnerMessage');

        let userCards = [];
        let announcedNumbers = [];

        // Buy Card
        document.getElementById('buyCard').addEventListener('click', () => {
            if (userCards.length >= 5) {
                alert('You can only buy up to 5 cards.');
                return;
            }
            const cardNumbers = Array.from({ length: 15 }, () => Math.floor(Math.random() * 99) + 1);
            userCards.push(cardNumbers);

            renderCards();
            alert('You have successfully purchased a card!');
        });

        // Check Cards
        document.getElementById('checkCards').addEventListener('click', () => {
            if (userCards.length === 0) {
                alert('You have no cards. Buy a card first.');
                return;
            }

            const isWinner = userCards.some(card => card.every(num => announcedNumbers.includes(num)));
            if (isWinner) {
                winnerMessage.style.display = 'block';
            } else {
                alert('Your cards are not complete yet.');
            }
        });

        // Show Winners
        document.getElementById('showWinners').addEventListener('click', () => {
            alert('Winners will be displayed here.');
        });

        // Render Cards
        function renderCards() {
            cardsContainer.innerHTML = '';
            userCards.forEach((card, index) => {
                const cardDiv = document.createElement('div');
                cardDiv.className = 'card';
                cardDiv.textContent = card.slice(0, 5).join(', ');
                cardsContainer.appendChild(cardDiv);
            });
        }

        // Announce Numbers (Simulated)
        document.getElementById('startGame').addEventListener('click', () => {
            announcedNumbers = [];
            for (let i = 0; i < 15; i++) {
                const number = Math.floor(Math.random() * 99) + 1;
                if (!announcedNumbers.includes(number)) {
                    announcedNumbers.push(number);
                }
            }
            alert(`Announced numbers: ${announcedNumbers.join(', ')}`);
        });
    </script>
</body>
</html>
