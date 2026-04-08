<script setup lang="ts">
type CardPosition = {
  id: number
}

const homeTeamName = 'Wolverhampton'
const awayTeamName = 'Manchester'

const totalCards = 10
const activeSlide = ref(0)
const cards: CardPosition[] = Array.from({ length: totalCards }, (_, index) => ({ id: index + 1 }))
const slideIndexes = Array.from({ length: 7 }, (_, index) => index)

const shouldMarquee = (name: string) => name.length > 15
</script>

<template>
  <main class="page">
    <NuxtRouteAnnouncer />

    <section class="figma-frame" aria-label="English Premier League betting cards">
      <img class="combined-background" src="/figma/background-1.png" alt="">

      <div class="cards-carousel">
        <div class="cards-track" :style="{ transform: `translateX(-${activeSlide * 274}px)` }">
          <div v-for="card in cards" :key="card.id" class="card-frame">
            <article class="betting-card">
              <span class="red-glow" />
              <span class="blue-glow" />
              <span class="top-line" />

              <span class="time-box" />
              <span class="time-text">2022-09-17TO7:35:00</span>

              <div class="league">
                <img src="/figma/soccer-epl.svg" alt="">
                <span>ENGLISH PREMIER LEAGUE</span>
              </div>

              <div class="home-team">
                <span class="logo-ring" />
                <img class="home-logo" src="/figma/wolverhampton.png" :alt="homeTeamName">
                <strong class="team-name" :class="{ 'is-marquee': shouldMarquee(homeTeamName) }">
                  <span>{{ homeTeamName }}</span>
                </strong>
              </div>

              <div class="score-area">
                <span class="score score-home">0</span>
                <span class="score-separator">-</span>
                <span class="score score-away">0</span>
                <strong class="team-name" :class="{ 'is-marquee': shouldMarquee(awayTeamName) }">
                  <span>{{ awayTeamName }}</span>
                </strong>
              </div>

              <div class="away-team">
                <span class="logo-ring" />
                <img src="/figma/manchester-epl.png" :alt="awayTeamName">
              </div>

              <button class="bet-now" type="button">BetNow</button>

              <button class="odd-button odd-left" type="button">
                <span>1.25</span>
                <strong>-0.83</strong>
              </button>
              <button class="odd-button odd-right" type="button">
                <span>-1.25</span>
                <strong>0.76</strong>
              </button>
            </article>
          </div>
        </div>
      </div>

      <div class="carousel-dots" aria-label="Card carousel pagination">
        <button
          v-for="index in slideIndexes"
          :key="index"
          type="button"
          class="carousel-dot"
          :class="{ active: activeSlide === index }"
          :aria-label="`Show card ${index + 1}`"
          :aria-pressed="activeSlide === index"
          @click="activeSlide = index"
        />
      </div>
    </section>
  </main>
</template>

<style>
* {
  box-sizing: border-box;
}

html,
body,
#__nuxt {
  min-height: 100%;
  margin: 0;
}

body {
  min-width: 320px;
  background: #242424;
  color: #fff;
  font-family: Inter, Arial, sans-serif;
}

button {
  border: 0;
  font: inherit;
}

.page {
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 20px;
  background: #242424;
  overflow: hidden;
}

.figma-frame {
  position: relative;
  width: 1168px;
  height: 243.255px;
  overflow: hidden;
}

.figma-frame img {
  user-select: none;
  pointer-events: none;
}

.combined-background {
  position: absolute;
  left: 48px;
  top: 19px;
  width: 1120px;
  height: 205px;
  object-fit: cover;
}

.cards-carousel {
  position: absolute;
  left: 342px;
  top: 42px;
  width: 826px;
  height: 160px;
  overflow: hidden;
}

.cards-track {
  display: flex;
  width: max-content;
  height: 160px;
  transition: transform 240ms ease;
  will-change: transform;
}

.card-frame {
  position: relative;
  flex: 0 0 274px;
  width: 274px;
  height: 160px;
}

.betting-card {
  position: absolute;
  inset: 0 auto auto 0;
  width: 253px;
  height: 160px;
  overflow: hidden;
  border: 1px solid rgb(255 255 255 / 42%);
  border-radius: 14px;
  background-image: linear-gradient(147.69deg, rgb(252 21 25 / 0%) 0%, rgb(252 21 25 / 37%) 50%, rgb(24 2 2 / 56%) 100%);
  transition: border-color 180ms ease;
}

.betting-card::after {
  position: absolute;
  top: -40px;
  left: -80px;
  z-index: 2;
  width: 72px;
  height: 240px;
  content: "";
  pointer-events: none;
  opacity: 0;
  background: linear-gradient(90deg, rgb(255 255 255 / 0%) 0%, rgb(255 255 255 / 42%) 50%, rgb(255 255 255 / 0%) 100%);
  filter: blur(2px);
  transform: rotate(18deg) translateX(0);
}

.betting-card:hover {
  border-color: rgb(255 255 255 / 62%);
}

.betting-card:hover::after {
  animation: card-glare 680ms ease-out 1;
}

@keyframes card-glare {
  0% {
    opacity: 0;
    transform: rotate(18deg) translateX(0);
  }

  20% {
    opacity: 1;
  }

  100% {
    opacity: 0;
    transform: rotate(18deg) translateX(390px);
  }
}

.red-glow,
.blue-glow {
  position: absolute;
  width: 128px;
  height: 128px;
  border-radius: 999px;
  filter: blur(64px);
}

.red-glow {
  left: 100.5px;
  top: 1px;
  background: #2f0505;
  opacity: 0.96;
}

.blue-glow {
  left: 171.5px;
  top: 268px;
  background: rgb(21 93 252 / 20%);
}

.top-line {
  position: absolute;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgb(255 255 255 / 30%), transparent);
}

.top-line {
  left: 167px;
  top: 27px;
  width: 260px;
}

.time-box {
  position: absolute;
  left: 8px;
  top: 7px;
  width: 100px;
  height: 18px;
  border: 0.5px solid rgb(255 255 255 / 35%);
  border-radius: 5px;
  background-image: linear-gradient(170.79deg, rgb(71 0 1 / 20%) 0%, rgb(46 0 1 / 50%) 100%);
}

.time-text {
  position: absolute;
  left: 15px;
  top: 8px;
  width: 99px;
  color: #ff8b00;
  font-size: 8px;
  font-weight: 600;
  line-height: 16px;
  opacity: 0.92;
}

.league {
  position: absolute;
  left: 125px;
  top: 9px;
  display: flex;
  align-items: center;
  gap: 3px;
  height: 12px;
  color: #efefef;
  font-size: 8px;
  line-height: 20px;
  white-space: nowrap;
}

.league img {
  width: 12px;
  height: 12px;
}

.home-team {
  position: absolute;
  left: 23px;
  top: 35px;
  width: 67px;
  height: 88px;
}

.home-team .logo-ring,
.away-team .logo-ring {
  position: absolute;
  border: 1px solid rgb(255 255 255 / 35%);
  border-radius: 50%;
  background-image: linear-gradient(135deg, rgb(71 0 1 / 20%) 0%, rgb(46 0 1 / 50%) 100%);
}

.home-team .logo-ring {
  left: -9px;
  top: -3px;
  width: 58px;
  height: 58px;
}

.home-team img {
  position: absolute;
  object-fit: cover;
}

.home-logo {
  left: 0;
  top: 6.191px;
  width: 38px;
  height: 39px;
}

.home-team strong {
  position: absolute;
  left: -24px;
  top: 62px;
  width: 90px;
  overflow: hidden;
  color: #fff;
  font-size: 10px;
  font-weight: 700;
  line-height: 9px;
  text-align: center;
  white-space: nowrap;
}

.team-name span {
  display: inline-block;
}

.team-name.is-marquee {
  text-align: left;
}

.team-name.is-marquee span {
  min-width: 100%;
  padding-left: 100%;
  animation: team-name-marquee 5s linear infinite;
}

.score-area {
  position: absolute;
  left: 81px;
  top: 34px;
  width: 181px;
  height: 94px;
}

.score {
  position: absolute;
  top: 0;
  display: grid;
  place-items: center;
  width: 33px;
  height: 46px;
  border: 1px solid rgb(117 105 105 / 50%);
  border-radius: 10px;
  background: #4d0607;
  color: #fff;
  font-size: 15px;
  font-weight: 700;
  line-height: 36px;
}

.score-home {
  left: 0;
}

.score-away {
  left: 56px;
  background: #500707;
}

.score-separator {
  position: absolute;
  left: 43px;
  top: 9px;
  font-size: 15px;
  font-weight: 800;
  line-height: 20px;
}

.score-area strong {
  position: absolute;
  left: 97px;
  top: 58px;
  width: 76px;
  overflow: hidden;
  color: #fff;
  font-size: 10px;
  font-weight: 700;
  line-height: 20px;
  white-space: nowrap;
}

@keyframes team-name-marquee {
  from {
    transform: translateX(0);
  }

  to {
    transform: translateX(-100%);
  }
}

.away-team {
  position: absolute;
  left: 180px;
  top: 32px;
  width: 58px;
  height: 58px;
}

.away-team .logo-ring {
  inset: 0;
}

.away-team img {
  position: absolute;
  left: 11px;
  top: 9px;
  width: 37px;
  height: 39px;
  object-fit: cover;
}

.bet-now {
  position: absolute;
  left: 86px;
  top: 89px;
  display: grid;
  place-items: center;
  width: 80px;
  height: 21px;
  border-radius: 7px;
  color: #fff;
  background-color: #a34d10;
  font-size: 10px;
  font-weight: 700;
  cursor: pointer;
}

.odd-button {
  opacity: 80%;
  position: absolute;
  top: 121.809px;
  height: 31px;
  overflow: hidden;
  border-radius: 7px;
  color: #fff;
  background-image: linear-gradient(151deg, rgb(115 66 66 / 80%) 20%, rgb(46 0 1 / 80%) 100%);
  cursor: pointer;
}

.odd-left {
  left: 4px;
  width: 118px;
}

.odd-right {
  left: 126px;
  width: 123px;
}

.odd-button span,
.odd-button strong {
  position: absolute;
  z-index: 1;
  display: block;
  opacity: 1;
  font-size: 10px;
  line-height: 32px;
  white-space: nowrap;
}

.odd-button span {
  top: 0;
  left: 15px;
  color: #f6ff00;
  font-weight: 700;
}

.odd-right span {
  left: 8px;
}

.odd-button strong {
  top: 0;
  right: 9px;
  color: #fff;
  font-weight: 700;
}

.odd-right {
  height: 30px;
}

.carousel-dots {
  position: absolute;
  left: 711px;
  top: 210px;
  z-index: 3;
  display: flex;
  align-items: center;
  gap: 5px;
}

.carousel-dot {
  width: 9px;
  height: 6px;
  padding: 0;
  border-radius: 999px;
  background: #d9d9d9;
  cursor: pointer;
}

.carousel-dot.active {
  width: 41px;
  background: #f5b719;
}

@media (max-width: 1208px) {
  .page {
    place-items: start center;
    padding: 16px;
  }

  .figma-frame {
    transform: scale(calc((100vw - 32px) / 1168));
    transform-origin: top center;
  }
}
</style>
