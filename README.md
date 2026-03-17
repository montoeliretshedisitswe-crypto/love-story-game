<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Love Story Game</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 40px; background: #fdf6f6; }
    #game { max-width: 600px; margin: auto; padding: 20px; border: 2px solid #d66; border-radius: 10px; background: #fff; }
    button { margin: 5px; padding: 10px 20px; border: none; border-radius: 5px; background: #d66; color: #fff; cursor: pointer; }
    button:hover { background: #a44; }
    #progress { margin-top: 20px; font-size: 0.9em; color: #333; }
  </style>
</head>
<body>
  <div id="game">
    <h2>Welcome to the beginning of a love story that started the moment I met you.</h2>
    <div id="story"></div>
    <div id="choices"></div>
    <div id="progress"><strong>Progress:</strong> <span id="log"></span></div>
  </div>

  <script>
    const storyDiv = document.getElementById("story");
    const choicesDiv = document.getElementById("choices");
    const logSpan = document.getElementById("log");
    let progress = [];

    function updateProgress(choice) {
      progress.push(choice);
      logSpan.textContent = progress.join(" → ");
    }

    function crashGame() {
      // Simulate a crash by throwing an error
      storyDiv.innerHTML = "<h3 style='color:red'>GAME OVER!! Site crashed 💥</h3>";
      choicesDiv.innerHTML = "";
      // Force a crash
      throw new Error("Game crashed intentionally!");
    }

    function showStory(text, options) {
      storyDiv.innerHTML = "<p>" + text + "</p>";
      choicesDiv.innerHTML = "";
      options.forEach(opt => {
        const btn = document.createElement("button");
        btn.textContent = opt.label;
        btn.onclick = () => {
          updateProgress(opt.label);
          opt.action();
        };
        choicesDiv.appendChild(btn);
      });
    }

    function startGame() {
      progress = [];
      updateProgress("Start");
      showStory("Do you prefer going out for a Sushi date or Pizza date?", [
        { label: "Sushi", action: sushiBranch },
        { label: "Pizza", action: pizzaBranch }
      ]);
    }

    // Sushi storyline
    function sushiBranch() {
      showStory("Would you rather have a lifetime supply of your fave snack or eat any meal for free at one restaurant?", [
        { label: "Snack", action: snackBranch },
        { label: "Restaurant", action: restaurantBranch }
      ]);
    }

    function snackBranch() {
      showStory("Would you prefer listening to RNB or Soul music when eating your snacks?", [
        { label: "RNB", action: rnbBranch },
        { label: "Soul", action: soulBranch }
      ]);
    }

    function rnbBranch() {
      showStory("Khopotso wants to know if you’d like to go out as friends or something more?", [
        { label: "More", action: () => showStory("I love you mtase... Please pick a date and come tell me so we may talk about us.", [{label:"Play Again", action:startGame}]) },
        { label: "Friends", action: crashGame }
      ]);
    }

    function soulBranch() {
      showStory("Soul music is for people with more love. May I be part of that love too?", [
        { label: "Yes", action: () => showStory("Let’s go have a snack date. You win!!", [{label:"Play Again", action:startGame}]) },
        { label: "No", action: crashGame }
      ]);
    }

    function restaurantBranch() {
      showStory("Do you want to go with me next time to the restaurant and eat the dish together?", [
        { label: "Yes", action: () => showStory("Choose a date that will work for you and come by my desk and tell me so we can go together.", [{label:"Play Again", action:startGame}]) },
        { label: "No", action: crashGame }
      ]);
    }

    // Pizza storyline
    function pizzaBranch() {
      showStory("Pizza is actually my fave too! Would you rather share a giant pizza together or try making one from scratch?", [
        { label: "Share", action: sharePizza },
        { label: "Make", action: makePizza }
      ]);
    }

    function sharePizza() {
      showStory("Do you want to watch a movie while eating pizza or go for a walk afterwards?", [
        { label: "Movie", action: () => showStory("Perfect! A pizza + movie night sounds romantic. You win!!", [{label:"Play Again", action:startGame}]) },
        { label: "Walk", action: () => showStory("A walk after pizza is sweet. Let’s plan it soon. You win!!", [{label:"Play Again", action:startGame}]) }
      ]);
    }

    function makePizza() {
      showStory("Making pizza together is fun! Would you like to bake a classic Margherita or experiment with wild toppings?", [
        { label: "Classic", action: () => showStory("A simple Margherita shows true love for tradition. You win!!", [{label:"Play Again", action:startGame}]) },
        { label: "Wild", action: () => showStory("Wild toppings mean wild love. Let’s try it together. You win!!", [{label:"Play Again", action:startGame}]) }
      ]);
    }

    // Start the game
    startGame();
  </script>
</body>
</html>
