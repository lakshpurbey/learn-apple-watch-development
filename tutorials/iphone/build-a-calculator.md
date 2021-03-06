# Build a Calculator

Now that you're equipped with the basics of **_Swift_**, we'll be using some of the skills to build our very first iOS app.

**You'll need:**  
* Xcode (version **8.1** or _above_)
    * You can follow along in other versions but you may encounter some issues  

>**Content**  
[MVC](understanding-mvc)  
[Numbers](#numbers)  
[Operators](#operators)  
[Product](#product)

### Create a Project
**if you haven't done this before, we'd recommend that you follow the [project setup guide](https://github.com/dwyl/learn-apple-watch-development/blob/master/setup/project-setup.md)**

### Understanding MVC
![mvc](https://cloud.githubusercontent.com/assets/2305591/20435146/e24db028-ada2-11e6-8fc0-bd2018fc7995.png)
**MVC (Model View Controller)** is a design pattern for building applications, It splits up the application into three components:
* **Model**
    * What your application is
    * e.g. functions that do calculation for us
* **Controller**
    * How your **_Model_** is displayed to the user (UI Logic)
    * It interprets the **_Model_** information for the **_View_**
    * e.g. what text/buttons should be displayed
* **View**
    * Things the **_Controllers_** will use to put things on screen
    * such as Buttons, labels
    * and getting input data from the users etc.


#### **Main Relationship between MVC**

* **_Controller_** can talk to the Model
* **_Controller_** can talk to the View
* **_Model_** and **_View_** never talk to each other
    * **_Model_** is UI independent
    * **_View_** is completely UI dependent
    * All Comms between the two have to pass through the **_Controller_**
* **_View_** can talk to the **_Controller_** in a structured (pre-defined) way. (we'll find out more when we get coding)
* **_Model_** can't talk to the **_Controller_**  
    * However if data changes in the **_Model_**, you can _broadcast_📻 the changes which the **_Controller_** can be listening🎶 for. _(Pub/Sub)_


### Numbers
Enough of me talking lets **build this calculator** already! We'll start by building the user interface. (numbers/display)

#### Interface Builder: In iOS you don't have to code the visuals, just drag and drop them (wire them onto the logic afterwards)

**Our first Button**
- Drag and drop a button from the utilities list
- Edit the text by double clicking
- Edit the Font Size and Colour using the attributes inspector in utilities

<img width="1680" alt="screen shot 2016-11-01 at 14 24 27" src="https://cloud.githubusercontent.com/assets/2305591/19892993/6b877a34-a03f-11e6-9e96-ca02f8989834.png">

- Compile and Run the app in a simulator
- We have our very first app! :smile:

**But nothing happens when we click the button :cry:**

#### Connect the button to from the UI to the controller by creating a method

- open up the Assistant editor to view the `controller` file alongside the `storyboard`
- select the button whilst holding the `control` key
![9gnTm2](http://i.makeagif.com/media/11-18-2016/9gnTm2.gif)  
- drag it into the `ViewController` class
    - Fill in all the information as found in the screenshot below:
<img width="302" alt="screen shot 2016-11-01 at 14 38 07" src="https://cloud.githubusercontent.com/assets/2305591/19893368/d90fb1e2-a040-11e6-9a0e-956f6ca59369.png">
- we have now connected our very first UI item to the controller by creating a method! :smile:

#### Create your layout for the calculator
<img width="1680" alt="screen shot 2016-11-01 at 14 48 28" src="https://cloud.githubusercontent.com/assets/2305591/19894152/df79a846-a043-11e6-8042-d34613056487.png">

#### Now print the digit that you are selecting
<img width="1680" alt="screen shot 2016-11-01 at 15 00 36" src="https://cloud.githubusercontent.com/assets/2305591/19894177/f7fed256-a043-11e6-97a4-80941a66a018.png">
```js
@IBAction func touchDigit(_ sender: UIButton) {
  let digit = sender.currentTitle!
  print("touched \(digit) digit")
}

```

**HINT**
- By selecting the option button and hovering over method names/arguments you'll see a little question mark ❓ (try this by hovering over the UIButton text)
- When you select the given text, it will open up a popup
- selecting the Class Reference link will open up the API Documentation which can be pretty handy when we are trying to find out the method for accessing the title for the digit.    

**HINT**

#### Add a Display to the UI

- select a label from the interface (drag & drop)
- link the label to the controller as an outlet
<img width="1680" alt="screen shot 2016-11-01 at 15 12 45" src="https://cloud.githubusercontent.com/assets/2305591/19895506/f39facb2-a048-11e6-9942-a1992e4b36e0.png">

#### Get rid of the trailing zero

- set a global variable called `userIsTyping` and set it to `false`
- modify the `currentTextInDisplay` with an `if` statement

**HINT**
- **All properties need to have an initial value**

**HINT**

```js
@IBOutlet private weak var display: UILabel!

private var userIsTyping = false

// @IBAction is just for viewing what part of the method is connected to
// the method, by hovering the little grey circle
// func just defining that this is a function
// touchDigit is the name of the method
// (###) contains the argument
@IBAction private func touchDigit(_ sender: UIButton) {
    let digit = sender.currentTitle!
    print("touched \(digit) digit")

    if userIsTyping {
        let currentTextInDisplay = display.text!
        display.text = currentTextInDisplay + digit
    } else {
        display.text = digit
    }
    userIsTyping = true
}
// You'll notice that I've added the keyword `private` in front of all
// of my functions and methods. This means that it is not open and available
// in the API
```
##### You've built your first ever kind of functioning calculator using swift on iOS! :tada:

### Operators

It's all well and good having some numbers that display on a screen when selected, but what about all the calculations? _Well_ if you remember when we talked about the **MVC**, we said that the brains of the app would live inside the _Model_.

#### Create Operator buttons and link them to an action
* create all the operators you'd like to use for your calculations
    * Add
    * Multiply
    * Divide
    * Square root
* Link all of the operators to the same Action `performOperation`

```js
@IBAction private func performOperation(_ sender: UIButton) {
 // code here
}
```
<img width="1680" alt="screen shot 2016-11-01 at 15 38 24" src="https://cloud.githubusercontent.com/assets/2305591/19895664/8a363c40-a049-11e6-9dd8-6d4ae25d339d.png">

> We could start adding the operator functionality inside of the controller <br>
but As we've mentioned above it's best practice to follow the **MVC** model and put it inside a seperate file

#### Setup the Model and connect it to the controller

* Create a new file called `calculator_model_brain.swift` in the same directory
    * Create a class `calculatorModelBrain`
    ```js
    class calculatorModelBrain {
      // functionality to go in here
    }
    ```
* connect the model to our controller
```js
private var brain = calculatorModelBrain() // just above our performOperation Action
```

#### Create our first Operation Key
The **Model** needs to be able to take all the inputs and also return the calculated value back to the controller so that it can be displayed on screen. To do so, we need to have:

  * `accumulator` for keeping track of the total
  * `performOperation` for doing the calculations
      * this function has multiple steps and requires us to create `Dictionary`, `enum` & `structs` [Reading material here](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html#//apple_ref/doc/uid/TP40014097-CH5-ID309)
  * `result` for returning the accumulated result


  #### Constants
  Our first example will be to make our calculator work with constants such as π
  * Create the methods required in calculatorModelBrain


  ```js
  class calculatorModelBrain {

    // accumulator for keeping track of the total
    private var accumulator = 0.0

    // number on which the calculation should occcur
    func setOperand(operand: Double) {
        accumulator = operand
    }

    // table that contains keys and values.
    private var operations: Dictionary<String,Operation> = [
        "π" : M_PI
    ]

    // Function that will return the calculated values
    func performOperation(symbol: String) {
        if let operation = operations[symbol] {
          accumulator = constant
        }
    }

    var result: Double {
        get {
            return accumulator
        }
    }
}
  ```

* Connect it up to the controller by adding the following inside the controller

```js
// link the calculatorModelBrain class and initialise it
private var brain = calculatorModelBrain()

// This var is a calculated property
// when we get displayValue, it will return a double
// when we set displayValue, it will set display to string
private var displayValue: Double {
    get {
        return Double(display.text!)!
    }
    set {
        display.text = String(newValue)
    }
}

@IBAction private func performOperation(_ sender: UIButton) {
    // when user is typing then it will set operand to what the user has input
    if userIsTyping {
        brain.setOperand(operand: displayValue)
        userIsTyping = false
    }
    // perform operation when mathematical symbol is selected by user
    if let mathematicalSymbol = sender.currentTitle {
       brain.performOperation(symbol: mathematicalSymbol)
    }
    // after the operation has been calculated we want to display the result
    displayValue = brain.result
}

```

##### You've built the functionality for constants in your calculator :tada:

#### UnaryOperators, Binary Operators and Equals
Now with a few changes to the **Model** we can add the ability to perform other functionality such as `Add`, `Multiply`, `Square root` etc.

```js
class calculatorModelBrain {

    private var accumulator = 0.0
    func setOperand(operand: Double) {
        accumulator = operand
    }

    // Dictionary contains all the different types of operations
    private var operations: Dictionary<String,Operation> = [
        "π" : Operation.Constant(M_PI),
        "e": Operation.Constant(M_E),
        "√": Operation.UnaryOperation(sqrt),
        "cos": Operation.UnaryOperation(cos),
        "±": Operation.UnaryOperation({ -$0 }),
        "×": Operation.BinaryOperation({(op1: Double, op2: Double) -> Double in
            return op1 * op2
            }
        ),
        "+": Operation.BinaryOperation({(op1, op2) in return op1 + op2}),
        "−": Operation.BinaryOperation({ $0 - $1 }),
        "÷": Operation.BinaryOperation({ $0 / $1 }),
        "=": Operation.Equals
    ]

    // enum contains all the Operations
    private enum Operation {
        case Constant(Double)
        case UnaryOperation((Double) -> Double)
        case BinaryOperation((Double, Double) -> Double)
        case Equals
    }

    // All the operation types cases are now covered by this switch statement
    func performOperation(symbol: String) {
        if let operation = operations[symbol] {
            switch operation {
            case .Constant(let associatedValue):
                accumulator = associatedValue
            case .UnaryOperation(let function):
                accumulator = function(accumulator)
            case .BinaryOperation(let function):
                executePendingBinaryOperation()
                pending = PendingBinaryOperationInfo(binaryFunction: function, firstOperand: accumulator)
            case .Equals:
                executePendingBinaryOperation()
            }
        }
    }

    // This function executed any pending operations
    // so that the user does not have to select equals every time
    // 1 + 2 + 3 + 4 = 10
    // 1 + 2 = + 3 = + 4 = 10
    private func executePendingBinaryOperation() {
        if pending != nil {
            accumulator = pending!.binaryFunction(pending!.firstOperand, accumulator)
            pending = nil
        }
    }

    private var pending: PendingBinaryOperationInfo? // optional variable pending which is either nil or the struct below

    private struct PendingBinaryOperationInfo {
        var binaryFunction: (Double, Double) -> Double
        var firstOperand: Double
    }

    var result: Double {
        get {
            return accumulator
        }
    }
}
```
### Product
#### Our final product is a functioning calculator :tada: :smile:

![screen shot 2016-11-21 at 12 52 18](https://cloud.githubusercontent.com/assets/2305591/20483340/6233a48a-afe9-11e6-9de8-8968fc5181b1.png)

There is a lot more that can be done to the calculator:
* Clearing the display to 0
* Using decimal points

#### Feel free to tackle any of the above features in your own time! :smile: But, if you are happy with the functionality and would like to style the calculator so that it works well on all screen sizes then follow the [Styling a calculator guide](./styling-a-calculator)

**If you've come across any issues and are unable to get your code up and running then here is the [link to the XCode project](resources/calculator) for this Tutorial.**
