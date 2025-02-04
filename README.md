<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Adventure Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="game-container">
        <h1>🗺️ Adventure Awaits!</h1>
        <div id="game-text"></div>
        <div id="choices"></div>
    </div>

    <script>
        const gameText = document.getElementById('game-text');
        const choicesContainer = document.getElementById('choices');

        const gameData = {
            start: {
                text: "You wake up in a mysterious forest. Paths lead north and east. What do you do?",
                choices: [
                    { text: "Go North", next: "northPath" },
                    { text: "Go East", next: "eastPath" }
                ]
            },
            northPath: {
                text: "You find an old cabin. Do you enter or walk past it?",
                choices: [
                    { text: "Enter the cabin", next: "cabinInside" },
                    { text: "Walk past", next: "forestDeeper" }
                ]
            },
            eastPath: {
                text: "A river blocks your path. There's a bridge and a boat.",
                choices: [
                    { text: "Cross the bridge", next: "bridgeCrossing" },
                    { text: "Take the boat", next: "boatRide" }
                ]
            },
            cabinInside: {
                text: "Inside the cabin, you find a treasure chest! You win! 🎉",
                choices: [
                    { text: "Play Again", next: "start" }
                ]
            },
            forestDeeper: {
                text: "You get lost deeper in the forest. Game over.",
                choices: [
                    { text: "Try Again", next: "start" }
                ]
            },
            bridgeCrossing: {
                text: "The bridge collapses! You fall into the river and swim to safety but lose your supplies.",
                choices: [
                    { text: "Keep going", next: "forestDeeper" }
                ]
            },
            boatRide: {
                text: "The boat takes you to a peaceful village. You find safety. You win! 🏡",
                choices: [
                    { text: "Play Again", next: "start" }
                ]
            }
        };

        function startGame(node) {
            const currentNode = gameData[node];
            gameText.textContent = currentNode.text;
            choicesContainer.innerHTML = '';

            currentNode.choices.forEach(choice => {
                const button = document.createElement('button');
                button.textContent = choice.text;
                button.classList.add('choice-button');
                button.onclick = () => startGame(choice.next);
                choicesContainer.appendChild(button);
            });
        }

        startGame('start');
    </script>
</body>
</html>

/* style.css */
body {
    font-family: 'Arial', sans-serif;
    background-color: #121212;
    color: #f5f5f5;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.game-container {
    background: #1e1e1e;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0,0,0,0.5);
    max-width: 500px;
    text-align: center;
}

h1 {
    font-size: 2rem;
    margin-bottom: 20px;
}

#game-text {
    margin-bottom: 20px;
    font-size: 1.2rem;
}

.choice-button {
    background-color: #6200ea;
    color: white;
    padding: 10px 15px;
    margin: 10px 0;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1rem;
    width: 100%;
}

.choice-button:hover {
    background-color: #3700b3;
}

@media (max-width: 600px) {
    .game-container {
        width: 90%;
    }
}