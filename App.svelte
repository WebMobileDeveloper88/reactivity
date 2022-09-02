<script>
  var count = 1;
  var anotherCount = 2;
  var blockVariable = 0;

  // Using count variable in
  // another variable using $:
  $: doubleCount = count * 2;

  // We can use count as many times
  // as we want
  $: tripleCount = count * 3;

  // We can also use $: declared variable
  // in another $: variable
  $: usingDoubleCount = doubleCount * 2;

  // We can also declare a function in $:
  // This will get updated when count changes
  $: usingFunction = () => {
    return count * 10;
  };

  // We can use more than one variable
  // This will update with either count
  // or anotherCount
  $: usingFunctionAgain = () => {
    return count * 10 + anotherCount;
  };

  // Storing only returned value of function
  // Will ONLY update with change in count
  // It won't update with anotherCount
  // Because the $: statement has count only
  $: returnFunctionValue = someFunction(count);

  // You can also create a block of statements
  // Here we are running a condition to change
  // value of blockVariable. This will run only
  // when count changes
  $: {
    if (count % 2) {
      blockVariable = 1;
    } else {
      blockVariable = 0;
    }
  }

  function increaseCount() {
    count += 1;
  }

  function increaseAnotherCount() {
    anotherCount += 1;
  }

  function someFunction(count) {
    return count + anotherCount;
  }
</script>

<p>Count = {count}</p>
<p>Double Count = {doubleCount}</p>
<p>Triple Count = {tripleCount}</p>
<p>Using doubleCount = {usingDoubleCount}</p>
<p>Using function = {usingFunction()}</p>
<p>
  Using function with both variables 
  = {usingFunctionAgain()}
</p>
<p>
  Function returning value = 
  {returnFunctionValue}
</p>
<p>
 Block Variable = {blockVariable}
</p>


<button on:click={increaseCount}>
  Increase Count
</button>
<button on:click={increaseAnotherCount}>
  Increase Another Count
</button>