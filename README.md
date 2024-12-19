
const calculatorMap = [1, 2, 4, 8, 16, 32, 64, 128];
var listinerId = 0;

function run() {
  listinerId = setInterval(() => {
   
    document.querySelector(".window.modal.fade-enter-done>.modal-body>button")?.click();

   
    const problem = document.querySelector(".problem:not(.blank-exit)");
  
    if (problem) {
   
      const div = problem.querySelector(".problem-wrapper>.sub-wrapper");

     
      if (problem.querySelector(".isProblem")) {
       

      
        div.querySelector(".digits").click();

        
        let sum = 0;
        div.querySelectorAll(".bit").forEach((e, i) => {
          sum += Number(e.innerText) * 2 ** (7 - i);
        });

        console.log("answer:", sum);

     
        Array.from(String(sum), Number).forEach((e) => {
          document.querySelector(`.calculator :nth-child(${calculatorMap[e]})`).click();
        });

      
        document.querySelector(`.calculator :nth-child(3)`).click();
      } else {


        let correct = Number(div.querySelector(".digits").innerText);

       
        let correctBin = new Array(8).fill(false);
        for (let index = 7; correct > 0 && index >= 0; index--) {
          correctBin[index] = Boolean(correct % 2);
          correct = Math.floor(correct / 2);
        }

        console.log("answer:", correctBin);

        div.querySelectorAll("button.bit").forEach((e, i) => {
        
          if ((e.innerText == "1") != correctBin[i]) {
            e.click();
          }
        });
      }
    }
  }, 500);
}

function stop() {
  clearInterval(listinerId);
}

document.addEventListener('keydown', function(event) {
  if (event.key === '`') {
    run();
  }
});

document.addEventListener('keydown', function(event) {
  if (event.key === '-') {
    stop();
  }
});
