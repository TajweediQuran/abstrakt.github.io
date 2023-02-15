# abstrakt.github.io
<!DOCTYPE html>
<html>
  <head>
    <title>Tic Tac Toe</title>
    <style>
      table {
        border-collapse: collapse;
        margin: 0 auto;
      }
      td {
        width: 100px;
        height: 100px;
        text-align: center;
        vertical-align: middle;
        border: 1px solid black;
        font-size: 40px;
        font-weight: bold;
        cursor: pointer;
      }
      .empty {
        background-color: white;
      }
      .x {
        background-color: #f2f2f2;
      }
      .o {
        background-color: #e6e6e6;
      }
    </style>
  </head>
  <body>
    <table>
      <tr>
        <td class="empty" id="0" onclick="makeMove(0)"></td>
        <td class="empty" id="1" onclick="makeMove(1)"></td>
        <td class="empty" id="2" onclick="makeMove(2)"></td>
      </tr>
      <tr>
        <td class="empty" id="3" onclick="makeMove(3)"></td>
        <td class="empty" id="4" onclick="makeMove(4)"></td>
        <td class="empty" id="5" onclick="makeMove(5)"></td>
      </tr>
      <tr>
        <td class="empty" id="6" onclick="makeMove(6)"></td>
        <td class="empty" id="7" onclick="makeMove(7)"></td>
        <td class="empty" id="8" onclick="makeMove(8)"></td>
      </tr>
    </table>
    <script>
      var board = ['', '', '', '', '', '', '', '', ''];
      var player = 'x';
      var computer = 'o';
      var gameover = false;

      function displayBoard() {
        for (var i = 0; i < board.length; i++) {
          var cell = document.getElementById(i);
          if (board[i] == '') {
            cell.innerHTML = '';
            cell.className = 'empty';
          } else if (board[i] == 'x') {
            cell.innerHTML = 'X';
            cell.className = 'x';
          } else if (board[i] == 'o') {
            cell.innerHTML = 'O';
            cell.className = 'o';
          }
        }
      }

      function makeMove(cell) {
        if (!gameover && board[cell] == '') {
          board[cell] = player;
          displayBoard();
          checkWin();
          if (!gameover) {
            computerMove();
          }
        }
      }

      function computerMove() {
        var move = minimax(board, computer).index;
        board[move] = computer;
        displayBoard();
        checkWin();
      }

      function checkWin() {
        var winning_combinations = [
          [0, 1, 2],
          [3, 4, 5],
          [6, 7, 8],
          [0, 3, 6],
          [1, 4, 7],
          [2, 5, 8],
          [0, 4, 8],
          [2, 4, 6]
        ];
        for (var i = 0; i < winning_combinations.length; i++) {
          var [a, b, c]
