My little example of suspension(multithreading) in nodejs

So a loop is running(blocking) on the main thread, you need to interrupt it but cannnot because the loop won't give way to that.
A simple solution is to suspend the function (to another thread kinda).


```js
    /**
    * blah blah blah... sets up the keypressed event
    **/
    const readline = require('readline');
    readline.emitKeypressEvents(process.stdin);
    process.stdin.setRawMode(true);
    
    //the variable we will toggle when the key is pressed
    let state = true

    //our suspension function
    setTimeout(() => process.stdin.on('keypress', (str, key) => {
      if ( key.name === 'q') {
          state = false
        process.exit();
      }
    }), 0)
    
    
    console.log('Press any key...');

    
    while(state) {
        console.log("The text will keep printing until killed by pressing 'q' on keyboard")
    }
    
```
