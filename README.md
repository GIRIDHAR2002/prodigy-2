# prodigy-2



html
<div class="container">
  <div class="stopwatch">
    <p id="display">00:00:00</p>
    <div class="btns">
      <button class="btn" type="button" id="start">Play</button>
      <button class="btn" type="button" id="pause">Pause</button>
      <button class="btn" type="button" id="reset">Reset</button>
    </div>
  </div>
</div>

css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f2f2f2;
}

.stopwatch {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-right: 2rem;
}

.stopwatch p {
  font-size: 2rem;
  margin-bottom: 0;
}

.btns {
  display: flex;
  flex-direction: column;
}

.btn {
  font-size: 1.2rem;
  padding: 0.5rem 1rem;
  margin-bottom: 0.5rem;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 0.2rem;
  cursor: pointer;
}

.btn:hover {
  background-color: #45a049;
}

java script
let startTime;
let elapsedTime;
let timerInterval;

function timeToString(time) {
  let diffInHrs = time / 3600000;
  let hh = Math.floor(diffInHrs);
  let diffInMin = (diffInHrs - hh) * 60;
  let mm = Math.floor(diffInMin);
  let diffInSec = (diffInMin - mm) * 60;
  let ss = Math.floor(diffInSec);
  let diffInMs = (diffInSec - ss) * 100;
  let ms = Math.floor(diffInMs);
  let formattedHH = hh.toString().padStart(2, "0");
  let formattedMM = mm.toString().padStart(2, "0");
  let formattedSS = ss.toString().padStart(2, "0");
  let formattedMS = ms.toString().padStart(2, "0");
  return `${formattedHH}:${formattedMM}:${formattedSS}.${formattedMS}`;
}

function print(txt) {
  document.getElementById("display").innerHTML = txt;
}

function start() {
  startTime = Date.now();
  timerInterval = setInterval(function printTime() {
    elapsedTime = Date.now() - startTime;
    print(timeToString(elapsedTime));
  }, 10);
  document.getElementById("start").style.display = "none";
  document.getElementById("pause").style.display = "block";
}

function pause() {
  clearInterval(timerInterval);
  document.getElementById("start").style.display = "block";
  document.getElementById("pause").style.display = "none";
}

function reset() {
  clearInterval(timerInterval);
  print("00:00:00");
  elapsedTime = 0;
  document.getElementById("start").style.display = "block";
  document.getElementById("pause").style.display = "none";
}

document.getElementById("start").addEventListener("click", start);
document.getElementById("pause").addEventListener("click", pause);
document.getElementById("reset").addEventListener("click", reset);


