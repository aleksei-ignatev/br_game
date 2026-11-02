<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="utf-8">
<title>DOOM-ish JS</title>
<style>
  html, body {
    margin: 0; padding: 0;
    background: #111;
    color: #ccc;
    font-family: monospace;
    overflow: hidden;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  #wrap { position: relative; }
  canvas {
    display: block;
    image-rendering: pixelated;
    image-rendering: crisp-edges;
    border: 2px solid #333;
    cursor: crosshair;
  }
  #help {
    margin-top: 10px;
    font-size: 13px;
    text-align: center;
  }
  #overlay {
    position: absolute; inset: 0;
    display: flex; align-items: center; justify-content: center;
    background: rgba(0,0,0,0.7);
    color: #f55; font-size: 32px;
    font-weight: bold;
    pointer-events: none;
    display: none;
  }
</style>
</head>
<body>
<div id="wrap">
  <canvas id="screen" width="640" height="400"></canvas>
  <div id="overlay">GAME OVER</div>
</div>
<div id="help">
  <b>W/S</b> — вперёд/назад &nbsp;|&nbsp;
  <b>A/D</b> — поворот &nbsp;|&nbsp;
  <b>Q/E</b> — стрейф &nbsp;|&nbsp;
  <b>Space / клик</b> — выстрел &nbsp;|&nbsp;
  <b>R</b> — рестарт
</div>

<script>
(() => {
"use strict";

// ============ Константы ============
const SCREEN_W = 640;
const SCREEN_H = 400;
const MAP_W = 24;
const MAP_H = 24;
const NUM_MONSTERS = 8;
const TEX_SIZE = 64;

// ============ Карта ============
const worldMap = [
    [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,1,0,0,0,1,1,1,1,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,1,0,0,0,1,0,0,1,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,1,0,0,0,1,1,1,1,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1,1,1,1,1,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
];

// ============ Canvas ============
const canvas = document.getElementById('screen');
const ctx = canvas.getContext('2d');
ctx.imageSmoothingEnabled = false;

// ImageData — наш пиксельный буфер (RGBA)
const imageData = ctx.createImageData(SCREEN_W, SCREEN_H);
const buf = new Uint32Array(imageData.data.buffer); // ABGR в little-endian = 0xAABBGGRR

const overlay = document.getElementById('overlay');

// ============ Цвета ============
// В Uint32Array на little-endian порядок байтов: 0xAABBGGRR
function rgb(r, g, b) {
    return (255 << 24) | (b << 16) | (g << 8) | r;
}

function putPixel(x, y, c) {
    if (x < 0 || x >= SCREEN_W || y < 0 || y >= SCREEN_H) return;
    buf[y * SCREEN_W + x] = c;
}

function fillRect(x, y, w, h, c) {
    const x0 = Math.max(0, x), y0 = Math.max(0, y);
    const x1 = Math.min(SCREEN_W, x + w), y1 = Math.min(SCREEN_H, y + h);
    for (let j = y0; j < y1; j++)
        for (let i = x0; i < x1; i++)
            buf[j * SCREEN_W + i] = c;
}

// ============ Текстуры ============
// Храним как Uint32Array[TEX_SIZE*TEX_SIZE] для каждой из 3 текстур
const tex = [
    new Uint32Array(TEX_SIZE * TEX_SIZE),
    new Uint32Array(TEX_SIZE * TEX_SIZE),
    new Uint32Array(TEX_SIZE * TEX_SIZE),
];

function genBrick(out) {
    for (let y = 0; y < TEX_SIZE; y++) {
        for (let x = 0; x < TEX_SIZE; x++) {
            const by = Math.floor(y / 16);
            const shift = (by & 1) ? 16 : 0;
            const bx = (x + shift) % 32;
            let c;
            if (y % 16 < 2 || bx < 2) c = rgb(60, 30, 20);
            else {
                const noise = ((x * 13 + y * 7) % 30) - 15;
                c = rgb(140 + noise, 70 + (noise >> 1), 50 + (noise >> 1));
            }
            out[y * TEX_SIZE + x] = c;
        }
    }
}

function genStone(out) {
    for (let y = 0; y < TEX_SIZE; y++) {
        for (let x = 0; x < TEX_SIZE; x++) {
            const n = ((x * 91 + y * 37) ^ (x * y * 7)) & 0x3F;
            const v = 90 + n;
            out[y * TEX_SIZE + x] = rgb(v, v, v - 10);
        }
    }
}

function genPanel(out) {
    for (let y = 0; y < TEX_SIZE; y++) {
        for (let x = 0; x < TEX_SIZE; x++) {
            const border = (x < 4 || x >= TEX_SIZE - 4 || y < 4 || y >= TEX_SIZE - 4);
            const inner = (x > 8 && x < TEX_SIZE - 8 && y > 8 && y < TEX_SIZE - 8);
            let c;
            if (border) c = rgb(40, 40, 50);
            else if (inner) c = rgb(100, 120, 160);
            else c = rgb(70, 80, 100);
            out[y * TEX_SIZE + x] = c;
        }
    }
}

genBrick(tex[0]);
genStone(tex[1]);
genPanel(tex[2]);

function texIndexFor(mx, my) {
    return ((mx * 7 + my * 13) % 3);
}

// ============ Спрайт монстра ============
function monsterPixel(nx, ny, flash, out) {
    const r2 = nx * nx + ny * ny;
    if (r2 > 1.0) return false;

    const body = flash ? rgb(255, 100, 100) : rgb(180, 40, 40);
    const dark = flash ? rgb(180, 0, 0) : rgb(70, 20, 20);
    const eyeCol = flash ? rgb(255, 255, 0) : rgb(255, 230, 0);

    // Рога
    if (ny < -0.5 && ny > -1.0) {
        const halfW = 0.15 * (1.0 - (-ny - 0.5) * 2.0);
        if (Math.abs(nx - 0.35) < halfW || Math.abs(nx + 0.35) < halfW) {
            out.c = dark; return true;
        }
    }
    // Глаза
    const ex = 0.3, ey = -0.15, er = 0.15;
    if ((nx - ex) * (nx - ex) + (ny - ey) * (ny - ey) < er * er ||
        (nx + ex) * (nx + ex) + (ny - ey) * (ny - ey) < er * er) {
        out.c = eyeCol; return true;
    }
    // Рот
    if (ny > 0.3 && ny < 0.4 && Math.abs(nx) < 0.4) {
        out.c = dark; return true;
    }
    out.c = (ny > 0.5) ? dark : body;
    return true;
}

// ============ Оружие ============
function drawGun(phase) {
    const cx = SCREEN_W >> 1;
    const baseY = SCREEN_H - 10;
    const kick = (phase > 0) ? 8 : 0;

    fillRect(cx - 20, baseY - 90 - kick, 40, 90, rgb(50, 30, 20));
    fillRect(cx - 12, baseY - 180 - kick, 24, 100, rgb(80, 80, 90));
    fillRect(cx - 6, baseY - 180 - kick, 12, 100, rgb(110, 110, 120));
    fillRect(cx - 16, baseY - 190 - kick, 32, 12, rgb(40, 40, 50));

    if (phase > 0) {
        const fr = 30 + phase * 4;
        const fr2 = fr * fr;
        for (let y = -fr; y <= fr; y++) {
            for (let x = -fr; x <= fr; x++) {
                const d2 = x * x + y * y;
                if (d2 > fr2) continue;
                let c;
                if (d2 < fr2 / 4) c = rgb(255, 255, 200);
                else if (d2 < fr2 * 3 / 5) c = rgb(255, 200, 0);
                else c = rgb(255, 100, 0);
                putPixel(cx + x, baseY - 195 - kick + y, c);
            }
        }
    }
    fillRect(cx - 60, baseY - 70, 45, 80, rgb(200, 150, 120));
    fillRect(cx + 15, baseY - 70, 45, 80, rgb(200, 150, 120));
}

function drawCrosshair() {
    const cx = SCREEN_W >> 1, cy = SCREEN_H >> 1;
    const col = rgb(0, 255, 0);
    for (let i = -8; i <= 8; i++) {
        if (i === 0) continue;
        putPixel(cx + i, cy, col);
        putPixel(cx, cy + i, col);
    }
}

// ============ Состояние игры ============
let state;
const zBuffer = new Float64Array(SCREEN_W);

// Ввод
const keys = {};

function initGame() {
    state = {
        posX: 2.5, posY: 2.5,
        dirX: 1.0, dirY: 0.0,
        planeX: 0.0, planeY: 0.66,
        gun: { firing: 0, fireStart: 0, ammo: 100 },
        playerHealth: 100,
        monsters: [],
        gameOver: false,
        lastTick: performance.now(),
    };

    // Спавн монстров
    for (let i = 0; i < NUM_MONSTERS; i++) {
        let mx, my;
        do {
            mx = 1 + Math.floor(Math.random() * (MAP_W - 2));
            my = 1 + Math.floor(Math.random() * (MAP_H - 2));
        } while (worldMap[mx][my] !== 0);
        state.monsters.push({
            x: mx + 0.5,
            y: my + 0.5,
            alive: true,
            health: 3,
            hitFlashUntil: 0,
            lastBite: 0,
            speed: 1.2 + Math.random(),
        });
    }

    overlay.style.display = 'none';
}

// ============ Стрельба ============
function tryShoot() {
    const s = state;
    let bestDist = 1e30;
    let bestIdx = -1;
    for (let i = 0; i < s.monsters.length; i++) {
        const m = s.monsters[i];
        if (!m.alive) continue;
        const dx = m.x - s.posX;
        const dy = m.y - s.posY;
        const dist = Math.sqrt(dx * dx + dy * dy);
        if (dist > 20) continue;
        const dot = (dx * s.dirX + dy * s.dirY) / (dist * Math.sqrt(s.dirX * s.dirX + s.dirY * s.dirY));
        if (dot < 0.97) continue;
        const steps = Math.floor(dist * 4);
        let blocked = false;
        for (let k = 1; k < steps; k++) {
            const t = k / steps;
            const mx = Math.floor(s.posX + dx * t);
            const my = Math.floor(s.posY + dy * t);
            if (mx < 0 || mx >= MAP_W || my < 0 || my >= MAP_H) { blocked = true; break; }
            if (worldMap[mx][my] > 0) { blocked = true; break; }
        }
        if (!blocked && dist < bestDist) {
            bestDist = dist;
            bestIdx = i;
        }
    }
    if (bestIdx >= 0) {
        const m = s.monsters[bestIdx];
        m.health--;
        m.hitFlashUntil = performance.now() + 120;
        if (m.health <= 0) m.alive = false;
    }
}

// ============ AI ============
function hasLineOfSight(x1, y1, x2, y2) {
    const dx = x2 - x1, dy = y2 - y1;
    const dist = Math.sqrt(dx * dx + dy * dy);
    const steps = Math.floor(dist * 6);
    for (let k = 1; k < steps; k++) {
        const t = k / steps;
        const mx = Math.floor(x1 + dx * t);
        const my = Math.floor(y1 + dy * t);
        if (mx < 0 || mx >= MAP_W || my < 0 || my >= MAP_H) return false;
        if (worldMap[mx][my] > 0) return false;
    }
    return true;
}

function moveMonsterTowards(m, tx, ty, step) {
    let dx = tx - m.x;
    let dy = ty - m.y;
    const dist = Math.sqrt(dx * dx + dy * dy);
    if (dist < 1e-3) return;
    dx /= dist; dy /= dist;

    let nx = m.x + dx * step;
    let ny = m.y + dy * step;
    if (worldMap[Math.floor(nx)][Math.floor(ny)] === 0) { m.x = nx; m.y = ny; return; }
    if (worldMap[Math.floor(m.x + dx * step)][Math.floor(m.y)] === 0) { m.x += dx * step; return; }
    if (worldMap[Math.floor(m.x)][Math.floor(m.y + dy * step)] === 0) { m.y += dy * step; return; }
    const px = -dy, py = dx;
    if (worldMap[Math.floor(m.x + px * step)][Math.floor(m.y + py * step)] === 0) {
        m.x += px * step; m.y += py * step; return;
    }
    if (worldMap[Math.floor(m.x - px * step)][Math.floor(m.y - py * step)] === 0) {
        m.x -= px * step; m.y -= py * step; return;
    }
}

// ============ Ввод ============
window.addEventListener('keydown', (e) => {
    keys[e.code] = true;
    if (e.code === 'Space' || e.code === 'KeyW' || e.code === 'KeyS' ||
        e.code === 'KeyA' || e.code === 'KeyD' || e.code === 'KeyQ' || e.code === 'KeyE') {
        e.preventDefault();
    }
    if (e.code === 'KeyR') initGame();
});
window.addEventListener('keyup', (e) => {
    keys[e.code] = false;
});
canvas.addEventListener('mousedown', () => {
    keys['Space'] = true;
});
window.addEventListener('mouseup', () => {
    keys['Space'] = false;
});

// ============ Игровой цикл ============
function update(now) {
    const s = state;
    let dt = (now - s.lastTick) / 1000;
    if (dt > 0.1) dt = 0.1;
    s.lastTick = now;

    if (s.gameOver) return;

    const moveSpeed = 3.5 * dt;
    const rotSpeed = 2.5 * dt;

    // Движение
    if (keys['KeyW']) {
        const nx = s.posX + s.dirX * moveSpeed;
        const ny = s.posY + s.dirY * moveSpeed;
        if (worldMap[Math.floor(nx)][Math.floor(s.posY)] === 0) s.posX = nx;
        if (worldMap[Math.floor(s.posX)][Math.floor(ny)] === 0) s.posY = ny;
    }
    if (keys['KeyS']) {
        const nx = s.posX - s.dirX * moveSpeed;
        const ny = s.posY - s.dirY * moveSpeed;
        if (worldMap[Math.floor(nx)][Math.floor(s.posY)] === 0) s.posX = nx;
        if (worldMap[Math.floor(s.posX)][Math.floor(ny)] === 0) s.posY = ny;
    }

    // Поворот: A = влево (минус), D = вправо (плюс)
    if (keys['KeyA']) {
        const cs = Math.cos(-rotSpeed), sn = Math.sin(-rotSpeed);
        const o = s.dirX;
        s.dirX = s.dirX * cs - s.dirY * sn;
        s.dirY = o * sn + s.dirY * cs;
        const op = s.planeX;
        s.planeX = s.planeX * cs - s.planeY * sn;
        s.planeY = op * sn + s.planeY * cs;
    }
    if (keys['KeyD']) {
        const cs = Math.cos(rotSpeed), sn = Math.sin(rotSpeed);
        const o = s.dirX;
        s.dirX = s.dirX * cs - s.dirY * sn;
        s.dirY = o * sn + s.dirY * cs;
        const op = s.planeX;
        s.planeX = s.planeX * cs - s.planeY * sn;
        s.planeY = op * sn + s.planeY * cs;
    }

    // Стрейф
    if (keys['KeyQ']) {
        const nx = s.posX + s.dirY * moveSpeed;
        const ny = s.posY - s.dirX * moveSpeed;
        if (worldMap[Math.floor(nx)][Math.floor(s.posY)] === 0) s.posX = nx;
        if (worldMap[Math.floor(s.posX)][Math.floor(ny)] === 0) s.posY = ny;
    }
    if (keys['KeyE']) {
        const nx = s.posX - s.dirY * moveSpeed;
        const ny = s.posY + s.dirX * moveSpeed;
        if (worldMap[Math.floor(nx)][Math.floor(s.posY)] === 0) s.posX = nx;
        if (worldMap[Math.floor(s.posX)][Math.floor(ny)] === 0) s.posY = ny;
    }

    // Выстрел
    if (keys['Space'] && !s.gun.firing && s.gun.ammo > 0) {
        s.gun.firing = 1;
        s.gun.fireStart = now;
        s.gun.ammo--;
        tryShoot();
    }

    // AI
    for (const m of s.monsters) {
        if (!m.alive) continue;
        const dx = s.posX - m.x;
        const dy = s.posY - m.y;
        const dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 10 && hasLineOfSight(m.x, m.y, s.posX, s.posY)) {
            if (dist > 0.8) {
                moveMonsterTowards(m, s.posX, s.posY, m.speed * dt);
            } else if (now - m.lastBite > 700) {
                m.lastBite = now;
                s.playerHealth -= 8;
                if (s.playerHealth < 0) s.playerHealth = 0;
            }
        }
    }

    if (s.playerHealth <= 0) {
        s.gameOver = true;
        overlay.style.display = 'flex';
    }
}

// ============ Рендер ============
function render(now) {
    const s = state;

    if (s.gameOver) {
        fillRect(0, 0, SCREEN_W, SCREEN_H, rgb(80, 0, 0));
        ctx.putImageData(imageData, 0, 0);
        return;
    }

    // Небо / пол
    const skyCol = rgb(25, 25, 55);
    const floorCol = rgb(45, 35, 35);
    for (let y = 0; y < SCREEN_H; y++) {
        const c = (y < SCREEN_H / 2) ? skyCol : floorCol;
        const off = y * SCREEN_W;
        for (let x = 0; x < SCREEN_W; x++) buf[off + x] = c;
    }

    // Стены
    for (let x = 0; x < SCREEN_W; x++) {
        const cameraX = 2.0 * x / SCREEN_W - 1.0;
        const rdx = s.dirX + s.planeX * cameraX;
        const rdy = s.dirY + s.planeY * cameraX;

        let mapX = Math.floor(s.posX);
        let mapY = Math.floor(s.posY);

        const ddx = (rdx === 0) ? 1e30 : Math.abs(1.0 / rdx);
        const ddy = (rdy === 0) ? 1e30 : Math.abs(1.0 / rdy);
        let sdx, sdy;
        let stepX, stepY, side = 0, hit = false;

        if (rdx < 0) { stepX = -1; sdx = (s.posX - mapX) * ddx; }
        else { stepX = 1; sdx = (mapX + 1.0 - s.posX) * ddx; }
        if (rdy < 0) { stepY = -1; sdy = (s.posY - mapY) * ddy; }
        else { stepY = 1; sdy = (mapY + 1.0 - s.posY) * ddy; }

        while (!hit) {
            if (sdx < sdy) { sdx += ddx; mapX += stepX; side = 0; }
            else { sdy += ddy; mapY += stepY; side = 1; }
            if (mapX < 0 || mapX >= MAP_W || mapY < 0 || mapY >= MAP_H) break;
            if (worldMap[mapX][mapY] > 0) hit = true;
        }

        let perp;
        if (side === 0) perp = (mapX - s.posX + (1 - stepX) / 2.0) / rdx;
        else perp = (mapY - s.posY + (1 - stepY) / 2.0) / rdy;
        if (perp < 0.01) perp = 0.01;
        zBuffer[x] = perp;

        const lh = Math.floor(SCREEN_H / perp);
        let ds = -lh / 2 + SCREEN_H / 2;
        if (ds < 0) ds = 0;
        let de = lh / 2 + SCREEN_H / 2;
        if (de >= SCREEN_H) de = SCREEN_H - 1;
        ds = Math.floor(ds);
        de = Math.floor(de);

        const tIdx = texIndexFor(mapX, mapY);
        const texture = tex[tIdx];

        let wallX;
        if (side === 0) wallX = s.posY + perp * rdy;
        else wallX = s.posX + perp * rdx;
        wallX -= Math.floor(wallX);
        let texX = Math.floor(wallX * TEX_SIZE);
        if ((side === 0 && rdx > 0) || (side === 1 && rdy < 0))
            texX = TEX_SIZE - texX - 1;
        if (texX < 0) texX = 0;
        if (texX >= TEX_SIZE) texX = TEX_SIZE - 1;

        const stepTex = TEX_SIZE / lh;
        let texPos = (ds - SCREEN_H / 2 + lh / 2) * stepTex;

        for (let y = ds; y < de; y++) {
            const texY = Math.floor(texPos) & (TEX_SIZE - 1);
            texPos += stepTex;
            let c = texture[texY * TEX_SIZE + texX];
            if (side === 1) {
                // Затемнение: извлекаем BGR, умножаем на 2/3
                const r = (c & 0xFF) * 2 / 3;
                const g = ((c >> 8) & 0xFF) * 2 / 3;
                const b = ((c >> 16) & 0xFF) * 2 / 3;
                c = rgb(r | 0, g | 0, b | 0);
            }
            buf[y * SCREEN_W + x] = c;
        }
    }

    // Монстры
    const order = [];
    for (let i = 0; i < s.monsters.length; i++) {
        const m = s.monsters[i];
        if (!m.alive) continue;
        const dx = m.x - s.posX;
        const dy = m.y - s.posY;
        order.push({ i, d: dx * dx + dy * dy });
    }
    order.sort((a, b) => b.d - a.d);

    const invDet = 1.0 / (s.planeX * s.dirY - s.dirX * s.planeY);
    const tmp = { c: 0 };

    for (const { i } of order) {
        const m = s.monsters[i];
        const spriteX = m.x - s.posX;
        const spriteY = m.y - s.posY;

        const tX = invDet * (s.dirY * spriteX - s.dirX * spriteY);
        const tY = invDet * (-s.planeY * spriteX + s.planeX * spriteY);
        if (tY <= 0.2) continue;

        const spriteScreenX = Math.floor((SCREEN_W / 2) * (1 + tX / tY));
        const spriteH = Math.abs(Math.floor(SCREEN_H / tY));
        const spriteW = spriteH;
        if (spriteH < 4) continue;

        let drawStartY = Math.floor(-spriteH / 2 + SCREEN_H / 2);
        let drawEndY = Math.floor(spriteH / 2 + SCREEN_H / 2);
        let drawStartX = Math.floor(-spriteW / 2 + spriteScreenX);
        let drawEndX = Math.floor(spriteW / 2 + spriteScreenX);
        if (drawStartY < 0) drawStartY = 0;
        if (drawEndY > SCREEN_H) drawEndY = SCREEN_H;
        if (drawStartX < 0) drawStartX = 0;
        if (drawEndX > SCREEN_W) drawEndX = SCREEN_W;

        const flash = m.hitFlashUntil > now;
        const halfH = spriteH / 2;
        const halfW = spriteW / 2;
        const spriteBaseY = SCREEN_H / 2 - halfH;

        for (let yy = drawStartY; yy < drawEndY; yy++) {
            const sy = yy - spriteBaseY;
            if (sy < 0 || sy >= spriteH) continue;
            const ny = (sy / spriteH) * 2.0 - 1.0;
            const rowOff = yy * SCREEN_W;
            for (let xx = drawStartX; xx < drawEndX; xx++) {
                if (tY >= zBuffer[xx]) continue;
                const sx = xx - (spriteScreenX - halfW);
                if (sx < 0 || sx >= spriteW) continue;
                const nx = (sx / spriteW) * 2.0 - 1.0;
                if (monsterPixel(nx, ny, flash, tmp))
                    buf[rowOff + xx] = tmp.c;
            }
        }
    }

    // Оружие
    let gunPhase = 0;
    if (s.gun.firing) {
        const el = now - s.gun.fireStart;
        if (el < 120) gunPhase = 3;
        else if (el < 240) gunPhase = 2;
        else if (el < 360) gunPhase = 1;
        else s.gun.firing = 0;
    }
    drawGun(gunPhase);
    drawCrosshair();

    // HUD
    fillRect(0, SCREEN_H - 34, SCREEN_W, 34, rgb(20, 20, 20));
    fillRect(10, SCREEN_H - 26, s.gun.ammo * 2, 14, rgb(255, 200, 0));
    let hpCol;
    if (s.playerHealth > 50) hpCol = rgb(0, 200, 0);
    else if (s.playerHealth > 25) hpCol = rgb(220, 180, 0);
    else hpCol = rgb(220, 0, 0);
    fillRect(SCREEN_W - 10 - s.playerHealth * 2, SCREEN_H - 26,
             s.playerHealth * 2, 14, hpCol);

    ctx.putImageData(imageData, 0, 0);
}

// ============ Цикл ============
function loop(now) {
    update(now);
    render(now);
    requestAnimationFrame(loop);
}

initGame();
requestAnimationFrame(loop);

})();
</script>
</body>
</html>
