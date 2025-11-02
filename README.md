# my-html-project-tic-tac-toe
tic-tac-toe game in which it is made up of HTML,CSS,JAVASCRIPT
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tic Tac Toe</title>
<style>
  *{margin:0;padding:0;box-sizing:border-box;font-family:"Poppins",sans-serif;}
  body{display:flex;justify-content:center;align-items:center;height:100vh;background:linear-gradient(135deg,#89f7fe,#66a6ff);}
  .container{background:white;padding:25px 30px;border-radius:20px;box-shadow:0 8px 25px rgba(0,0,0,0.2);text-align:center;}
  h1{margin-bottom:20px;color:#333;letter-spacing:1px;}
  .board{display:grid;grid-template-columns:repeat(3,100px);gap:10px;margin-bottom:20px;}
  .cell{width:100px;height:100px;display:flex;justify-content:center;align-items:center;font-size:2.5em;font-weight:bold;color:#333;background:#f8f8f8;border-radius:12px;cursor:pointer;transition:all 0.2s;}
  .cell:hover{background:#e9f2ff;transform:scale(1.05);}
  .status{font-size:1.1em;margin-bottom:15px;color:#555;}
  button{background:#66a6ff;color:white;padding:10px 20px;border:none;border-radius:12px;cursor:pointer;font-size:1em;transition:0.3s;}
  button:hover{background:#4d8aff;}
</style>
</head>
<body>
<div class="container">
  <h1>Tic Tac Toe</h1>
  <div class="status" id="status">Turn: X</div>
  <div class="board" id="board"></div>
  <button onclick="resetGame()">Reset</button>
</div>

<script>
  const board=document.getElementById("board");
  const status=document.getElementById("status");
  let cells=[],player="X",gameOver=false;

  function createBoard(){
    board.innerHTML="";
    cells=[];
    for(let i=0;i<9;i++){
      const cell=document.createElement("div");
      cell.classList.add("cell");
      cell.addEventListener("click",()=>makeMove(i));
      board.appendChild(cell);
      cells.push(cell);
    }
  }

  function makeMove(i){
    if(cells[i].textContent||gameOver)return;
    cells[i].textContent=player;
    if(checkWin()){
      status.textContent=`${player} wins! 🎉`;
      gameOver=true;
    }else if([...cells].every(c=>c.textContent)){
      status.textContent="It's a draw 😅";
      gameOver=true;
    }else{
      player=player==="X"?"O":"X";
      status.textContent=`Turn: ${player}`;
    }
  }

  function checkWin(){
    const w=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
    return w.some(([a,b,c])=>cells[a].textContent&&cells[a].textContent===cells[b].textContent&&cells[a].textContent===cells[c].textContent);
  }

  function resetGame(){
    player="X";gameOver=false;
    status.textContent=`Turn: ${player}`;
    createBoard();
  }

  createBoard();
</script>
</body>
</html>
