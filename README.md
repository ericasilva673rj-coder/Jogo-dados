<!DOCTYPE html><html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Corrida até 50</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #f0f0f0;
    }
    .container {
      margin-top: 50px;
    }
    .player {
      margin: 20px;
      padding: 15px;
      background: white;
      border-radius: 10px;
      display: inline-block;
      width: 200px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      margin-top: 20px;
      cursor: pointer;
    }
    .active {
      border: 2px solid green;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🎲 Corrida até 50</h1><div id="player1" class="player active">
  <h2>Jogador 1</h2>
  <p>Pontos: <span id="score1">0</span></p>
</div>

<div id="player2" class="player">
  <h2>Jogador 2</h2>
  <p>Pontos: <span id="score2">0</span></p>
</div>

<h2 id="dice">🎲</h2>
<button onclick="rollDice()">Rolar Dado</button>
<h3 id="message"></h3>

  </div>  <script>
    let scores = [0, 0];
    let currentPlayer = 0;

    function rollDice() {
      let dice = Math.floor(Math.random() * 6) + 1;
      document.getElementById('dice').innerText = '🎲 ' + dice;

      let message = '';

      if (dice === 1) {
        scores[currentPlayer] = Math.max(0, scores[currentPlayer] - 2);
        message = 'Tirou 1! Perdeu 2 pontos.';
        switchPlayer();
      } else {
        scores[currentPlayer] += dice;

        if (dice === 6) {
          scores[currentPlayer] += 3;
          message = 'Tirou 6! +3 pontos e joga novamente!';
        } else {
          switchPlayer();
        }
      }

      if (scores[currentPlayer] > 50) {
        scores[currentPlayer] = 45;
        message += ' Passou de 50! Volta para 45.';
      }

      updateUI(message);
      checkWinner();
    }

    function switchPlayer() {
      currentPlayer = currentPlayer === 0 ? 1 : 0;
    }

    function updateUI(message) {
      document.getElementById('score1').innerText = scores[0];
      document.getElementById('score2').innerText = scores[1];
      document.getElementById('message').innerText = message;

      document.getElementById('player1').classList.remove('active');
      document.getElementById('player2').classList.remove('active');
      document.getElementById('player' + (currentPlayer + 1)).classList.add('active');
    }

    function checkWinner() {
      if (scores[currentPlayer] === 50) {
        document.getElementById('message').innerText =
          'Jogador ' + (currentPlayer + 1) + ' venceu! 🎉';
        document.querySelector('button').disabled = true;
      }
    }
  </script></body>
</html>
