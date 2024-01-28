

# Team RATs with Nøtteknekker











<video  class="figure-img img-fluid rounded" controls>
	<source src="figures/solve.mp4" type="video/mp4">
	Your browser does not support the video tag. The video shows a student revealing the proper answer of a question with the Nøtteknekker app.
</video>



# Preparing RATs with Nøtteknekker


## Step 1: Develop Your RAT

To use Nøtteknekker, you need between 5 and 12 questions.
Each question must have four answer alternatives (A, B, C, D), where one answer is considered *best*.
Write the test in any format convenient for you.

Shuffle the answer alternatives randomly, and write down the sequence of best or correct answers.
For instance, in a test with 10 questions, our answer alternatives could be `ABBDCAACBB`.
This means, the correct answer of the first question is `A`, and `B` of the second question, and so on.

In the following, we use the same answer alternatives for the individual students and the teams.
For trying our RATs your first time, this is probably the easiest option and works well. 
If you want to automatically create different answer alternatives for each student and each team, you can use the [Teampy Program](https://falkr.github.io/teampy/).



## Step 2: Printing the Individual RATs

Print one copy for each individual student.




## Step 3: Printing the Team RATs

When the students do the individual tests, they don't receive the correct answer while they solve the test, so there is nothing for us to do.
But during the team test, the teams reveal the right answer with each question they solve.
For that, we use the Nøtteknekker app.
This app reveals the right answer step by step, it just has to be loaded with the encoded form of the answers which we will generate below.

Enter below the answer alternatives for your RAT. In our example with 10 questions that was `ABBDCAACBB`. 
On the right side you see the Nøtteknekker code. In our example that would be `CGU3DB`.



<div class="container">
	  <div class="input-group mb-3">
		  <input type="text" class="form-control" id="inputString" placeholder="Enter answers...">
		  <span class="input-group-text"><i class="bi bi-arrow-right"></i></span>
		  <input type="text" class="form-control" id="reversedString" readonly>
		</div>
		<small id="okText" class="error-messagex"></small>
		<small id="errorText" class="error-message"></small>
</div>
<style>
  .error-message {
	  color: red;
	  margin-top: 5px;
  }
</style>
<script>
  const base5Digits = ['X', 'A', 'B', 'C', 'D'];
  const base32Digits = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ234567'.split('');
  function base5ToBase32(base5Array) {
	  let base10Number = 0;
	  for (let digit of base5Array) {
		  if (!base5Digits.includes(digit)) {
			  return ['I', 'n', 'v', 'a', 'l', 'i', 'd'];
		  }
		  let position = base5Digits.indexOf(digit);
		  base10Number = base10Number * 5 + position;
	  }
	  let base32Array = [];
	  while (base10Number > 0) {
		  let remainder = base10Number % 32;
		  base32Array.unshift(base32Digits[remainder]);
		  base10Number = Math.floor(base10Number / 32);
	  }
	  return base32Array.length === 0 ? ['0'] : base32Array;
  }
  document.getElementById('inputString').addEventListener('input', function(e) {
	  var inputVal = e.target.value.toUpperCase();
	  // Filter out unwanted characters
	  inputVal = inputVal.replace(/[^ABCDX]/gi, '');
	  e.target.value = inputVal;
	  if(inputVal.length < 5) {
		  document.getElementById('errorText').textContent = 'Please enter at least 5 characters.';
		  document.getElementById('okText').textContent = '';
	  } else if(inputVal.length > 12) {
		document.getElementById('errorText').textContent = 'There can be at most 12 questions.';
		document.getElementById('okText').textContent = '';
	  } else {
		document.getElementById('errorText').textContent = '';
		  document.getElementById('okText').textContent = inputVal.length + ' questions.';
	  }
	  inputVal = inputVal.padEnd(12, 'X');
	  let outputVal = base5ToBase32(inputVal.split(''));
	  document.getElementById('reversedString').value = outputVal.join('');
  });
</script>


Write this 6-letter code at the top of the team RAT before you print it. Alternatively, show it to your students on your slides presentation.

**Only one student per team** needs an iPhone (or iPad) and install the app *Nøtteknekker*.
They open the app, and enter the 6-digit code that corresponds to your answer alternatives.  



<figure class="figure">
  <a href="https://apps.apple.com/no/app/nøtteknekker/id1667651492">
	<img src="figures/appstore.png" class="figure-img img-fluid rounded" alt="" style="width:160px; height: 54px">
  </a>
</figure>