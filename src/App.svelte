<script>
  import Navbar from './components/Navbar.svelte';
  import Footer from './components/Footer.svelte';
	import Progress from './components/Progress.svelte';
  import Card from './components/Card.svelte';
  import CardNavigation from './components/CardNavigation.svelte';
  import Result from './components/Result.svelte';
  import { questions } from './data/questions2.js';

  let currentQuestion = 0;
	// Track selected option per question
  let answeredMap = {};
  let answeredCount = 0;
  let correctCount = 0;

  let disablePrev = true;
  let disableNext = false;

  function updateButtonStates() {
    disablePrev = currentQuestion === 0;
    disableNext = currentQuestion === questions.length - 1;
  }

  function nextQuestion() {
    if (currentQuestion < questions.length - 1) {
      currentQuestion += 1;
      updateButtonStates();
    }
  }

  function prevQuestion() {
    if (currentQuestion > 0) {
      currentQuestion -= 1;
      updateButtonStates();
    }
  }

  function onAnswered(selectedIndex) {
    const qIndex = currentQuestion;

    // Store the selected answer for this question
    if (answeredMap[qIndex] === undefined) {
      answeredMap[qIndex] = selectedIndex;
    }

    // Recalculate counts dynamically
    answeredCount = Object.keys(answeredMap).length;
    correctCount = Object.entries(answeredMap).filter(
      ([q, answer]) => answer === questions[q].correct
    ).length;
  }

  function resetQuiz() {
    currentQuestion = 0;
    answeredMap = {};
    answeredCount = 0;
    correctCount = 0;
    disablePrev = true;
    disableNext = false;
  }
</script>

<div class="d-flex flex-column min-vh-100">
  <Navbar />

  <div class="main d-flex justify-content-center align-items-center flex-fill">
    <div class="quiz-container">
			<Progress 
		    current={answeredCount} 
		    total={questions.length} 
		  />
					
      {#key currentQuestion}
        <div class="card-fade">
          <Card 
            question={questions[currentQuestion]} 
            onAnswered={onAnswered} 
            selectedAnswer={answeredMap[currentQuestion]}
          />
        </div>
      {/key}

      {#if answeredCount === questions.length}
        <Result 
          correctCount={correctCount} 
          totalQuestions={questions.length} 
          onTryAgain={resetQuiz} 
        />
      {:else}
        <CardNavigation 
          prev={prevQuestion} 
          next={nextQuestion} 
          {disablePrev} 
          {disableNext} 
        />
      {/if}
    </div>
  </div>

  <Footer />
</div>

<style>
.main {
  flex: 1;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.quiz-container {
  width: 75%;
  max-width: 360px;
}

@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}

.card-fade {
  animation: fade-in 0.3s ease forwards;
}
</style>
