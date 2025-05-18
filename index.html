const canvas = document.getElementById('tetris');
const context = canvas.getContext('2d');

const nextCanvas = document.getElementById('next');
const nextCtx = nextCanvas.getContext('2d');

const gameOverElement = document.getElementById('gameOver');
const nameInput = document.getElementById('nameInput');
const restartBtn = document.getElementById('restartBtn');
const scoreElement = document.getElementById('highscore');
const highscoreList = document.getElementById('highscoreList');
const gameOverSound = document.getElementById('gameOverSound');

let arena = createMatrix(10, 20);
let player = {
    pos: {
        x: 0,
        y: 0
    },
    matrix: null,
    next: null,
    score: 0,
    name: ''
};

const colors = [
    null,
    '#0ff', '#f0f', '#ff0', '#0f0', '#00f', '#f00', '#0fa'
];

let dropCounter = 0;
let dropInterval = 1000;
let lastTime = 0;
let frameId;
let paused = false;
let moveDirection = 0; // -1 for left, 1 for right
let rotateDirection = 0; // 1 for clockwise, -1 for counterclockwise
let dropInProgress = false;

function resizeCanvas() {
    const containerWidth = window.innerWidth;
    const containerHeight = window.innerHeight;
    const gameSize = Math.min(containerWidth, containerHeight); // Use the smaller dimension

    canvas.width = gameSize * 0.5; // Adjust the proportion as needed
    canvas.height = gameSize;

    nextCanvas.width = gameSize * 0.2; // Adjust size of next canvas
    nextCanvas.height = nextCanvas.width;

    context.scale(canvas.width / 10, canvas.height / 20); // Scale based on canvas width
    nextCtx.scale(nextCanvas.width / 5, nextCanvas.height / 5);

    draw(); // Redraw the game
    drawNext();
}

function createMatrix(w, h) {
    const matrix = [];
    while (h--) {
        matrix.push(new Array(w).fill(0));
    }
    return matrix;
}

function createPiece(type) {
    if (type === 'T') return [
        [0, 0, 0],
        [1, 1, 1],
        [0, 1, 0]
    ];
    if (type === 'O') return [
        [2, 2],
        [2, 2]
    ];
    if (type === 'L') return [
        [0, 3, 0],
        [0, 3, 0],
        [0, 3, 3]
    ];
    if (type === 'J') return [
        [0, 4, 0],
        [0, 4, 0],
        [4, 4, 0]
    ];
    if (type === 'I') return [
        [0, 5, 0, 0],
        [0, 5, 0, 0],
        [0, 5, 0, 0],
        [0, 5, 0, 0]
    ];
    if (type === 'S') return [
        [0, 6, 6],
        [6, 6, 0],
        [0, 0, 0]
    ];
    if (type === 'Z') return [
        [7, 7, 0],
        [0, 7, 7],
        [0, 0, 0]
    ];
}

function drawMatrix(matrix, offset, ctx = context) {
    matrix.forEach((row, y) => {
        row.forEach((value, x) => {
            if (value !== 0) {
                ctx.fillStyle = colors[value];
                ctx.fillRect(x + offset.x, y + offset.y, 1, 1);
            }
        });
    });
}

function draw() {
    context.fillStyle = '#111';
    context.fillRect(0, 0, canvas.width, canvas.height);
    drawMatrix(arena, {
        x: 0,
        y: 0
    });
    drawMatrix(player.matrix, player.pos);
}

function merge(arena, player) {
    player.matrix.forEach((row, y) => {
        row.forEach((value, x) => {
            if (value !== 0) {
                arena[y + player.pos.y][x + player.pos.x] = value;
            }
        });
    });
}

function collide(arena, player) {
    const m = player.matrix;
    const o = player.pos;
    for (let y = 0; y < m.length; ++y) {
        for (let x = 0; x < m[y].length; ++x) {
            if (m[y][x] !== 0 &&
                (arena[y + o.y] && arena[y + o.y][x + o.x]) !== 0) {
                return true;
            }
        }
    }
    return false;
}

function playerDrop() {
    player.pos.y++;
    if (collide(arena, player)) {
        player.pos.y--;
        merge(arena, player);
        playerReset();
        arenaSweep();
        updateScore();
    }
    dropCounter = 0;
}

function playerMove(dir) {
    player.pos.x += dir;
    if (collide(arena, player)) {
        player.pos.x -= dir;
    }
}

function playerReset() {
    if (!player.next) {
        player.next = createPiece('TJLOSZI'[Math.floor(Math.random() * 7)]);
    }
    player.matrix = player.next;
    player.next = createPiece('TJLOSZI'[Math.floor(Math.random() * 7)]);
    player.pos.y = 0;
    player.pos.x = Math.floor(arena[0].length / 2) - Math.floor(player.matrix[0].length / 2);
    if (collide(arena, player)) {
        gameOver();
    }
    drawNext();
}

function playerRotate(dir) {
    const pos = player.pos.x;
    let offset = 1;
    rotate(player.matrix, dir);
    while (collide(arena, player)) {
        player.pos.x += offset;
        offset = -(offset + (offset > 0 ? 1 : -1));
        if (offset > player.matrix[0].length) {
            rotate(player.matrix, -dir);
            player.pos.x = pos;
            return;
        }
    }
}

function rotate(matrix, dir) {
    for (let y = 0; y < matrix.length; ++y) {
        for (let x = 0; x < y; ++x) {
            [matrix[x][y], matrix[y][x]] = [matrix[y][x], matrix[x][y]];
        }
    }
    if (dir > 0) matrix.forEach(row => row.reverse());
    else matrix.reverse();
}

function arenaSweep() {
    let lines = 0;
    outer: for (let y = arena.length - 1; y >= 0; --y) {
        for (let x = 0; x < arena[y].length; ++x) {
            if (arena[y][x] === 0) {
                continue outer;
            }
        }
        const row = arena.splice(y, 1)[0].fill(0);
        arena.unshift(row);
        ++y;
        lines++;
    }

    const linePoints = [0, 100, 300, 500, 800];
    if (lines > 0) {
        player.score += linePoints[lines] || lines * 200;
    }
}

function updateScore() {
    scoreElement.innerText = player.score;
}

function drawNext() {
    nextCtx.fillStyle = '#111';
    nextCtx.fillRect(0, 0, nextCanvas.width, nextCanvas.height);
    if (player.next) {
        const offsetX = Math.floor((5 - player.next[0].length) / 2);
        const offsetY = Math.floor((5 - player.next.length) / 2);
        drawMatrix(player.next, {
            x: offsetX,
            y: offsetY
        }, nextCtx);
    }
}

function update(time = 0) {
    if (