[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=14975823&assignment_repo_type=AssignmentRepo)

<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="UTF-8">
  <title>Jogo da Memória Simples</title>
  <link rel="stylesheet" href="styles.css"></link>
  <script src="scripts.js" charset="utf-8"></script>
</head>
<body>

  <h3><span id="result"></span></h3>

  <div class="board">
  </div>

</body>
</html>

"Script.js"

document.addEventListener('DOMContentLoaded', () => {
  //opções de cartas
  const cards = [
    {
      name: 'Lagarto',
      img: 'images/Lagarto.png'
    },
    {
      name: 'Macaco',
      img: 'images/macaco.png'
    },
    {
      name: 'Peixe',
      img: 'images/peixe.png'
    },
    {
      name: 'Tartaruga',
      img: 'images/tartaruga.png'
    },
    {
      name: 'Cachorro',
      img: 'images/cachorro.png'
    },
    {
      name: 'Gato',
      img: 'images/Gato.png'
    },
    {
      name: 'Lagarto',
      img: 'images/Lagarto.png'
    },
    {
      name: 'Macaco',
      img: 'images/macaco.png'
    },
    {
      name: 'Peixe',
      img: 'images/peixe.png'
    },
    {
      name: 'Tartaruga',
      img: 'images/tartaruga.png'
    },
    {
      name: 'Cachorro',
      img: 'images/cachorro.png'
    },
    {
      name: 'Gato',
      img: 'images/Gato.png'
    }
  ]

  //embaralhar todas as cartas
  cards.sort(() => 0.5 - Math.random())

  //recupaerar elementos
  const board = document.querySelector('.board')
  const resultView = document.querySelector('#result')
  let cardsChosen = [] //cartas escolhidas
  let cardsChosenId = [] //ids das cartas escolhidas para caso de click na mesma imagem
  let cardsWon = [] //cartas combinadas

  //criar o quadro de cartas
  function createBoard() {
    for (let i = 0; i < cards.length; i++) {
      const card = document.createElement('img')
      card.setAttribute('src', 'images/estrela.png')
      card.setAttribute('data-id', i)
      card.addEventListener('click', flipCard)
      board.appendChild(card)
    }
  }

  //checagem de combinações
  function checkForMatch() {
    const cards = document.querySelectorAll('img')
    const optionOneId = cardsChosenId[0]
    const optionTwoId = cardsChosenId[1]
    
    //verificar clique na mesma imagem 
    if(optionOneId == optionTwoId) {
      cards[optionOneId].setAttribute('src', 'images/estrela.png')
      cards[optionTwoId].setAttribute('src', 'images/estrela.png')
      alert('Você clicou na mesma imagem')
    }
    //verificar combinação se click em imagens diferentes
    else if (cardsChosen[0] === cardsChosen[1]) {
      alert('Você encontrou uma combinação')
      cards[optionOneId].setAttribute('src', 'images/check.png')
      cards[optionTwoId].setAttribute('src', 'images/check.png')
      cards[optionOneId].removeEventListener('click', flipCard)
      cards[optionTwoId].removeEventListener('click', flipCard)
      cardsWon.push(cardsChosen)
    } else {
      cards[optionOneId].setAttribute('src', 'images/estrela.png')
      cards[optionTwoId].setAttribute('src', 'images/estrela.png')
      alert('Errou, tente novamente')
    }
    cardsChosen = []
    cardsChosenId = []
    //mostrar placar
    resultView.textContent = 'Pares Encontrados: '+cardsWon.length
    if  (cardsWon.length === cards.length/2) {
      resultView.textContent = 'Parabéns! Você conseguiu encontrar todas as cartas'
    }
  }

  //virar as cartas
  function flipCard() {
    let cardId = this.getAttribute('data-id')
    cardsChosen.push(cards[cardId].name)
    cardsChosenId.push(cardId)
    this.setAttribute('src', cards[cardId].img)
    if (cardsChosen.length ===2) {
      setTimeout(checkForMatch, 500)
    }
  }

  createBoard()
})

"styles.css"

h3{
  text-align: center;
}
.board {
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  width: 400px;
  height: 300px;
}
