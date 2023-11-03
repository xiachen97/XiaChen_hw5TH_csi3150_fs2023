# Quiz App Tutorial

## Lesson Outcomes

This quiz app is a web application designed to provide users with a fun and interactive learning experience by testing their knowledge through a set of questions. It is provided in the form of timed quizzes on each question and real-time assessment of user answers and correct answers. And give user feedback in the final score.

## Functional features

- Users can click “start quiz”.
- Users need to read some rules to determine start quiz or exit.
- Questions are presented one at a time with a time limit of 15 seconds.
- Users must select an answer before the timer runs out.
- Once an answer is selected, it cannot be changed.
- The app provides immediate feedback on whether the answer is correct or not.
- The user's final score is calculated based on the number of correct answers.
- Users can replay the quiz or exit it at the end.

## Technology Stack

- HTML
- CSS
- JavaScript

## Project Directory Structure
```
C:\Desktop\GitHub\XiaChen_hw5TH_csi3150_fs2023
├─js
| ├─questions.js
| └quizApp.js
├─css
| └style.css
├─README.md
├─index.html
```
## Code explanations

### <span style="color: blue;">index.html</span>

```
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz App Demo</title>

    <!-- CSS FILE -->
    <link rel="stylesheet" href="css/style.css">
    <!-- This is my personal font awesome kit code. you will have to add your own after you register with email-->
    <script src="https://kit.fontawesome.com/4a4f4b55b0.js" crossorigin="anonymous"></script>

     <!-- Add questions list -->
    <script src="js/questions.js" defer></script>

    <!-- Main logic of the app -->
    <script src="js/quizApp.js" defer></script>
</head>
```

1. The head section contains the document's meta-information, styles, and scripts to ensure that the web page displays correctly and has the required interactivity.

CODE:

* link rel="stylesheet" : references an external CSS style sheet, which determines the appearance and style of the web page.

* script src is fontawesome.com : Icons can be used in pages by referencing Font Awesome's icon library.

* script src is js/questions.js defer and js/quizApp.js defer are two asynchronously loaded external JavaScript files. The first one contain questions and answers Data, the second contain the main logic and interactive behavior of Quiz App.

```
<body>
    <!-- Quiz START Button -->
    <div class="start_btn"><button>Start Quiz</button></div>

    <!-- Instruction box wrapper -->
    <div class="info_box">
        <div class="info-title"><span>Some Rules of this Quiz</span></div>
        <div class="info-list">
            <div class="info">1. You will have only <span>15 seconds</span> per each question.</div>
            <div class="info">2. Once you select your answer, it can't be undone.</div>
            <div class="info">3. You can't select any option once time goes off.</div>
            <div class="info">4. You can't exit from the Quiz while you're playing.</div>
            <div class="info">5. You'll get points on the basis of your correct answers.</div>
        </div>
        <div class="buttons">
            <button class="quit">Exit Quiz</button>
            <button class="restart">Continue</button>
        </div>
    </div>

    <!-- Quiz Box -->
    <div class="quiz_box">
        <header>
            <div class="title">Demo Quiz App in JavaScript</div>
            <div class="timer">
                <div class="time_left_txt">Time Left</div>
                <div class="timer_sec">15</div>
            </div>
            <div class="time_line"></div>
        </header>
        <section>
            <div class="que_text">
                <!-- Insert questions from ./js/questions.js -->
            </div>
            <div class="option_list">
                <!-- Insert options to questions from ./js/questions.js -->
            </div>
        </section>

        <!-- footer of Quiz Box -->
        <footer>
            <div class="total_que">
                <!-- insert Question Count Number dynamically from JavaScript App logic -->
            </div>
            <button class="next_btn">Next Que</button>
        </footer>
    </div>

    <!-- Result Box -->
    <div class="result_box">
        <div class="icon">
            <i class="fas fa-crown"></i>
        </div>
        <div class="complete_text">You've completed the Quiz!</div>
        <div class="score_text">
            <!-- insert dynamic user score as Result from JavaScript -->
        </div>
        <div class="buttons">
            <button class="restart">Replay Quiz</button>
            <button class="quit">Quit Quiz</button>
        </div>
    </div>

</body>
```
2. The body of this HTML code block contains the key elements of the quiz application page.

CODE:

* class is "start_btn": A button element that users can click to start or start answering a question.
* class is "info_box": A wrapper containing the rules for answering questions, including a title, a list of rules, and buttons(quit and start).
* class is "quiz_box": The main answering area, including title, timer, question text, answer options, dynamic statistics questions and next question button.
* class is"result_box": Result display area, including crown icon, completion text, user score text and restart/exit button.

### <span style="color: blue;">style.css</span>

```
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap");
```

1. This line of code imports the "Poppins" font style from Google Fonts. It uses the @import statement to specify the URL address of the font. This font will be used in the web page.

```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

body {
  background: #a020f0;
}

::selection {
  color: #fff;
  background: #a020f0;
}
```

2. Define global styles such as text font, page background color, and color when user selects text.

CODE:

* \*{...} : Reset the margins and padding of all HTML elements to ensure there is no default spacing.

* Body{...} : Set the background color of the page to purple.

* ::selection{...} : This is a pseudo-element selector that allows customizing the color and background color when the user selects text.

```
.info_box.activeInfo,
.quiz_box.activeQuiz,
.result_box.activeResult {
  opacity: 1;
  z-index: 5;
  pointer-events: auto;
  transform: translate(-50%, -50%) scale(1);
}
```

3. CSS style code controls the appearance and interactive behavior of elements with class names "activeInfo", "activeQuiz" and "activeResult" when JavaScript is triggered. 

CODE:

* Opacity : 1 means the element is completely opaque. 
* z-index : a css property used to control the stacking order of elements on a web page. 
* pointer-events: auto; : means the element can respond to mouse events, such as clicks or hovers. 
* scale(1) : means that the size of the element is not scaled.

4. All unannotated CSS code basically defines the style and appearance of the web page.

### <span style="color: blue;">questions.js</span>

This text contains a JavaScript array, where each element is an object consists of the following members: question number, questions, options, and answers. 
The main function of this array is to store the questions and answer options of the quiz game or test for display and interaction on the web page.

### <span style="color: blue;">quizApp.js</span>

```
const start_btn = document.querySelector(".start_btn button");
const info_box = document.querySelector(".info_box");
const exit_btn = info_box.querySelector(".buttons .quit");
const continue_btn = info_box.querySelector(".buttons .restart");
const quiz_box = document.querySelector(".quiz_box");
const result_box = document.querySelector(".result_box");
const restart_quiz = result_box.querySelector(".buttons .restart");
const quit_quiz = result_box.querySelector(".buttons .quit");
const option_list = document.querySelector(".option_list");
const time_line = document.querySelector("header .time_line");
const timeText = document.querySelector(".timer .time_left_txt");
const timeCount = document.querySelector(".timer .timer_sec");
const next_btn = document.querySelector("footer .next_btn");
const bottom_ques_counter = document.querySelector("footer .total_que");
```

1. Get HTML elements by querying a specific CSS selector in the document

```
// if startQuiz button clicked
start_btn.addEventListener("click", (e) => {
  info_box.classList.add("activeInfo"); //show info box
});

// if exitQuiz button clicked
exit_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
});

// if continueQuiz button clicked
continue_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
  quiz_box.classList.add("activeQuiz"); //show quiz box
  showQuetions(0); //calling showQestions function
  queCounter(1); //passing 1 parameter to queCounter
  startTimer(15); //calling startTimer function
  startTimerLine(0); //calling startTimerLine function
});

```

2. When "start_btn", "exit_btn", "continue_btn" is clicked, trigger CSS rules to change the visibility of the element. 
showQuetions(0), queCounter(1), startTimer(15), startTimerLine(0) are the four functions be called in this file. 
The purpose of these code snippets is to initialize and start various aspects of the quiz game, including displaying questions, counters, timers, and timelines.

```
// if Next Question button is clicked
next_btn.addEventListener("click", (e) => {
  //check if it does not exceed max questions
  if (que_count < questions.length - 1) {
    que_count++; //increment the que_count value
    que_numb++; //increment the que_numb value
    showQuetions(que_count); //calling showQestions function
    queCounter(que_numb); //passing que_numb value to queCounter
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    startTimer(timeValue); //calling startTimer function
    startTimerLine(widthValue); //calling startTimerLine function
    timeText.textContent = "Time Left"; //change the timeText to Time Left
    next_btn.classList.remove("show"); //hide the next button
  } else {
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    showResult(); //calling showResult function
  }
});
```

3. This code is used to load the next question when the user clicks the "Next Question" button and also checks if all questions have been answered. If so, clears the counter and counterline to call showResult() function to display the final quiz results.

CODE:

* if (que_count < questions.length - 1){...} : Checks if the question counter is less than the length of the questions array minus one, ensuring that the number of questions is not exceeded.

* que_count++; : Increment the question counter to point to the next question.

* que_numb++; : Increment the question number value to represent the next question number.

* showQuetions(que_count); : Call the "showQuetions" function to show the next question (pass the "que_count" parameter here)

* startTimer(timeValue); : Call the "startTimer" function to start timing a new question and set the time to the initial value.

* startTimerLine(widthValue); : Call the "startTimerLine" function to restart the timeline or progress bar and set the width to the initial value.

* timeText.textContent = "Time Left"; : Change the content of the time text to "Time Left" to prompt the user for the remaining time.

```
function optionSelected(answer) {
  clearInterval(counter); //clear counter
  clearInterval(counterLine); //clear counterLine
  let userAns = answer.textContent; //getting user selected option
  let correcAns = questions[que_count].answer; //getting correct answer from array
  const allOptions = option_list.children.length; //getting all option items

  //if user selected option is equal to array's correct answer
  if (userAns == correcAns) {
    userScore += 1; //update total score value increment by 1
    answer.classList.add("correct"); //add green color to correct selected option
    answer.insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to correct selected option
    console.log("Correct Answer");
    console.log("Your correct answers = " + userScore);
  } else {
    answer.classList.add("incorrect"); //add red color to correct selected option
    answer.insertAdjacentHTML("beforeend", crossIconTag); //add cross icon to correct selected option
    console.log("Wrong Answer");

    for (i = 0; i < allOptions; i++) {
      if (option_list.children[i].textContent == correcAns) {
        //if there is an option which is matched to an array answer
        option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
        option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
        console.log("Auto selected correct answer.");
      }
    }
  }
  for (i = 0; i < allOptions; i++) {
    option_list.children[i].classList.add("disabled"); //once user select an option, disable all options
  }
  next_btn.classList.add("show"); //show the next button if user selected any option
}
```

4. This code is used to handle the logic after the user selects a question option, including updating the score and style based on the user's selection, and displaying the correct answer if needed.

```
// control the timer and actions associated to it
function startTimer(time) {
  counter = setInterval(timer, 1000);
  function timer() {
    timeCount.textContent = time; //change the value of timeCount with time value
    time--; //decrement the time value
    if (time < 9) {
      //if timer is less than 9
      let addZero = timeCount.textContent;
      timeCount.textContent = "0" + addZero; //add a 0 before time value
    }
    if (time < 0) {
      //if timer is less than 0
      clearInterval(counter); //clear counter
      timeText.textContent = "Time Off"; //change the time text to time off
      const allOptions = option_list.children.length; //get all option items
      let correcAns = questions[que_count].answer; //get correct answer from array
      for (i = 0; i < allOptions; i++) {
        if (option_list.children[i].textContent == correcAns) {
          //if there is an option which is matched to an array answer
          option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
          option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
          console.log("Time Off: Auto selected correct answer.");
        }
      }
      for (i = 0; i < allOptions; i++) {
        option_list.children[i].classList.add("disabled"); //once user select an option then disabled all options
      }
      next_btn.classList.add("show"); //show the next button if user selected any option
    }
  }
}
```

5. It is used to start a timer, countdown counter to control remaining time in quiz application.

CODE:

* function startTimer(time){...} : It accepts a parameter time, which represents the initial countdown time.
* counter = setInterval(timer, 1000); : This line of code uses the setInterval function to create a timer with an interval of 1000 milliseconds (1 second) and assigns it to a variable named counter. This timer will execute a function named timer every second.
* function timer(){...} : This is an internally defined function called timer that actually does the countdown and updates the display of remaining time.
* let addZero = timeCount.textContent; : If the time is less than 9, it will get the current time text.
* timeCount.textContent = "0" + addZero; : Then add a "0" before the time to ensure that the displayed time format is two digits.

```
// Shows a progress bar mirroring timer value left
function startTimerLine(time) {
  counterLine = setInterval(timer, 29);
  function timer() {
    time += 1; //upgrading time value with 1
    time_line.style.width = time + "px"; //increasing width of time_line with px by time value
    if (time > 549) {
      //if time value is greater than 549
      clearInterval(counterLine); //clear counterLine
    }
  }
}
```

6. This code creates a horizontal timer bar, increases its width every 29 milliseconds until the width reaches the specified value (549 pixels), and then stops the timer. The timing entry is used to display the user's remaining time.

```
function queCounter(index) {
  //creating a new span tag and passing the question number and total question
  let totalQueCounTag =
    "<span><p>" +
    index +
    "</p> of <p>" +
    questions.length +
    "</p> Questions</span>";
  bottom_ques_counter.innerHTML = totalQueCounTag; //adding new span tag inside bottom_ques_counter
}
```

7. The purpose of this code is to update the displayed question count based on the index of the question currently answered by the user. Tell the user which question they are answering and how many questions need to be answered.
