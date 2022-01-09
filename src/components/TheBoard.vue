<script>
import TheSquare from "@/components/TheSquare";

export default {
  render() {
    return (
        <div>
          <div class="status">{this.status}</div>
          <div class="board-row">
            {this.renderSquare(0)}
            {this.renderSquare(1)}
            {this.renderSquare(2)}
          </div>
          <div class="board-row">
            {this.renderSquare(3)}
            {this.renderSquare(4)}
            {this.renderSquare(5)}
          </div>
          <div class="board-row">
            {this.renderSquare(6)}
            {this.renderSquare(7)}
            {this.renderSquare(8)}
          </div>
        </div>
    )
  },
  data() {
    return {
      status: null,
      squares: Array(9).fill(null),
      xIsNext: true
    }
  },
  updated() {
    const winner = calculateWinner(this.squares)

    if(winner) {
      this.status = `${winner} win!`
    } else {
      // eslint-disable-next-line no-unused-vars
      this.status = `Next player: ${this.xIsNext ? 'X' : 'O'}`;
    }
  },
  methods: {
    handleClick(i) {
      if(calculateWinner(this.squares) || this.squares[i]) {
        return;
      }

      const squares = this.squares.slice();
      squares[i] = this.xIsNext ? 'X' : 'O'

      // this.$set(this.$data, 'squares', squares)
      this.squares = squares;
      this.xIsNext = !this.xIsNext;
    },
    renderSquare(i) {
      return (
          <TheSquare value={this.squares[i]} vOn:onClick={() => this.handleClick(i)} />
      )
    }
  }
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
</script>
