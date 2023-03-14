# Notes_JS
Notes regarding important information about Javascript


## -----------------> Reduce
As an input needs an array, so, if we receive an string for instance it's useful to manipulate the string as follows and then apply the reduce method in once:
```js
Array.from(string).reduce() => {}
```
Once we have then input data in the format needed, we go deep in to know how reduce works
First of all, as we commented in advance, the input data needed is an array
The first parameter is the callback, if there's not, we will open double brackets and left empty the first one, and the second and third parameters are the acumulator and actual value:

```js
Array.reduce((previous, current) => {
...
})

        //The logic inside this method and the use that we will want to give is the following:

        const reducer = (value) => {
            let result = value[0];
            Array.from(value).reduce((previous, current) => {
                if (/[aeiouAEIOU]/.test(previous) && !/[aeiouAEIOU]/.test(current)) {
                    result += current.toUpperCase()
                    console.log('previous --> ' + previous);
                    console.log('current --> ' + current);
                    console.log('accumulator --> ' + result);
                } else result += current
                console.log('previous --> ' + previous);
                console.log('current --> ' + current);
                console.log('accumulator --> ' + result);

                if (!/[a-zA-Z]/.test(current)) {
                    return previous
                } else return current

            })

            return result
```
The number of iterations/loops depends on the lenght that the array has. On each iteration the reduce function picks two values following the order of the element of the array. 
(Running the "reducer" function above, we will understand how the two values iteration works graphically)
Therefore, in each iteration the previous and the current elements of the array are captured, then we are able to carry on an operation with this two elements, like sum up them, or whatever we want.

In the "reducer" function, given a string we convert into capital every consonant into capital if comes after a vowel.
In this particular case, it's important to initialize an accumulator that add every letter to a variable



## -----------------> Test

Do not confuse with the utils of testing library (jest,...)
When we work with string could be very useful to use this method combine with regex
Data input needed are a string and a regex (with regex format!!)


Is quite simple, basically is a method of a regex which takes the string as a parameter:

if (!/[a-zA-Z]/.test(string)  // Important to put the regex sintax inside /[...]/

With this line we implement this method inside a conditional, otherwise, without it, the method only throws back a boolean
This line is saying that if a string matches any character from lowercase "a" through uppercase "Z"



## -----------------> ReplaceAll

Looks similar to an excel function and quite simple and intuitive:

let delimitador = ","
string = "5 4 6 8 9"
string = string.replaceAll(delimitador, ",")



## -----------------> Join

Data input is an array and a string which is going to join all the elements of the array and converts into a string
Very useful inside a loop which is pushing elements to a variable to present the final result:

if (numerosNegativos.length > 0) {
    return 'Los números negativos no están permitidos. '+ numerosNegativos.join(",") // All the elements of the "numerosNegativos" array are going to be concatenated using "," between each element
    


## -----------------> Push & Split

Data input needed is an array where the method is implemented and a string or another array which are going to be added at the end of the first array as last element. Very useful inside a loop:

const numeros = str.split(','); // Every time that "," appears in "str" we will cut it and create another element of a new array called "numeros", otherwise, we will not be able to operate with forEach

```js
numeros.forEach(numero => {
    
    let n = Number(numero);
    if (n < 0) {
        numerosNegativos.push(n);
    } else {
        if (n > 1000) 
          return numerosNegativos;        
    };

```
On another hand, if we want to apply the same logic but with a string, we can do the following instead of --> "numerosNegativos.push":

numerosNegativos += n



## -----------------> Regex

Given that every input that we receive from html is going to be consider as a string in JS 
sometimes, we will need to carry on the validation with strings. Here some examples:

```js
const isNegative = () => {

    const num1 = document.getElementById("numb1-input").value
    const num2 = document.getElementById("numb2-input").value
    const onlyNegativeNumbers = /^-\d+$/
    const onlyPositiveNumbers = /^\d+$/
    

    if (num1.match(onlyNegativeNumbers)) {
        document.getElementById("result-message").innerHTML = "Hay un numero negativo en el primer numero"
        return
    }

    if (num2.match(onlyNegativeNumbers)) {
        document.getElementById("result-message").innerHTML = "Hay un numero negativo en el segundo numero"
        return
    }

    if (!num1.match(onlyPositiveNumbers)) {
        document.getElementById("result-message").innerHTML = "El formato en el primer numero no es correcto"
        return
    }

    if (!num2.match(onlyPositiveNumbers)) {
        document.getElementById("result-message").innerHTML = "El formato en el segundo numero no es correcto"
        return
    }
   
    document.getElementById("result-message").innerHTML = "Correcto"

}
```

In this code we can see how we validate with negative or positive intengers inside a string using match() method and regex.
Find more regex examples here: https://stackoverflow.com/questions/15814592/how-do-i-include-negative-decimal-numbers-in-this-regular-expression


## -----------------> Destructuring

When we are working with different functions and using them as a callbacks, we want to retrieve some values from one fuction to another
That's where we will need to use the destructuring. Here the example:

```js
function retrieveValues () {

        const firstNum = Number(document.getElementById("input1").value)
        const secondNum = Number(document.getElementById("input2").value)
        
        return { num1: firstNum, num2: secondNum }  // If we want to assign the input values to a different variable name's
                                                    // Alternatively, if we don't want to use different variable's name
                                                    // we could use: return { firstNum, secondNum }
        
        }

function suma () {

        const values = retrieveValues()
        const { num1, num2 } = values
        const sum = num1 + num2
```


## -----------------> Data type validation

We can use two keyboards to validate
Either "typeof" or "instaceof"
For the first one, we will have to put the data type in commas. Example: if (Callback typeof "function" === true)
On the second example, it should be without commas and in capital letter first. Example: if (Callback instaceof Function === true)

For a function:

    if (! functionToDo instanceof Function) { 
        return console.log("El segundo parámetro debe ser una función")
    }
    

## -----------------> Return in function

Example to understand better how returns in functions scopes works and which are the good practices to implement:

```js
function myMap (myArr, functionToDo) {
    const result = []  // Even if we are going to do a push() to modificate this array, we should create as a "const" to make sure that any side effect occurs or 
                       // someone assigns result equal to another thing.
                       // Moreover, this has to be skipped to be declared in the global scope. Like this, we make sure that it's only accesible if it's returned
                       // by the function itself

    if (!functionToDo instanceof Function) {
        return "El segundo parámetro debe ser una función"
    }

    for (let index = 0; index < myArr.length; index++) {
        result.push(functionToDo(myArr[index]))
    }

    return result
}

const multiplyByTwo = (num) =>  num * 2 // Arrow function so "return" keyword is not needed

const multiplyByTen = (num) => num * 10

const convertToUpperCase = (str) => str.toUpperCase()

const nums = [1, 4, 9, 2, 22]
const citiesNames = ['Barcelona', 'Paris', 'Roma', 'Londres', 'Berlin']

const result = myMap(citiesNames, convertToUpperCase) // Similar to what we do with prompt. We store the call of a function inside a variable
                                                      // Even if it's the same name, this result is not the same that exists inside the myMap() function
                                                      // By doing this, we make sure that all what we want to be returned by the function, is accesible outside the 
                                                      // function

console.log(result)                                             
document.getElementById("result-message").innerHTML = result
```


## -----------------> Callbacks

We will see the different ways to write the array method "map()" with its callback

![image](https://user-images.githubusercontent.com/71343560/219028396-0d831610-5d26-484b-88b8-ef8aba7455ce.png)



```js
const nums = [1,2,3,4,5]

const parseToString = function (n) {             // In this example as function are consider citizens of first class in JS, we can assign a variable to a function
        return n.toString()
}

const numsToString = nums.map( parseToString )  // And this first class citizen function will be called as callback inside the map method
                                                // numsToString is the new array that the map() method return by itself

```
-----------OR----------------
```js
const numsToString = nums.map(function (n) {    // We save the step of declaring the callback function inside a variable. Instead, we declare the function that we
                                                // want inside the map() method in the callback space
        return n.toString()
})
```
-----------OR----------------
```js
const numsToString = nums.map((n) => n.toString())  // Finally, we transform the callback function inside the map into a arrow function.
                                                    // In this manner, we can save the curly braces, the return (if it's one line) and the "function" keyword
```

## -----------------> Class

Let's see an example of a class constructor encapsulated and with private propierties:

```js
class Car  {

    #brand  // Mandatory to add the hash before to make it private
    #model  // this means that outside the block we will not be able to see it neither modify
    #color
    constructor(brand, model, color) {
        this.#brand = this.#validate( brand,  'Brand')  // Everytime that we are creating a new instace, the private 
        this.#model = this.#validate(model, 'Model')    // function #validate will be called and its validations         
        this.#color = this.#validate(color, 'Color')    // will be carried on 
    }

    #validate(value, name) {                            // Here, we are creating the private function that we mentioned
        if (!value) throw Error(${name} can not be empty)
        if (typeof value !== 'string') throw Error (${name} should be a string)
        return value
    }

    getBrand () {
        return this.#brand      // As it is a private propierty, is the only way that we can see outside the block
    }                           // by running myCar.Brand will not work, instead, myCar.getBrand

    getModel () {
        return this.#model
    }

    getColor () {
        return this.#color
    }

    setColor (color) {
        this.#color = this.#validate(color, 'Color')    // As it is a private propierty, is the only way that we can see outside the block
    }                                                   // but it's important to repeat the validation here
                                                        // if not, at the moment of instancing a data number won't be accepted, but once is setted, a number will be accepted (which is not the behaviour expected)

    driving() {
        console.log('🚙')
    }
}
```

## -----------------> Package.json

We can understand it as the place were we declare the instructions and details of the project.
There are parameters which only have a naming character, but there are other that will have a functional impact.

```
{
    "name": "my-awesome-package",  //Naming
    "version": "1.0.0",  
    "author": "Your Name <email@example.com>",  //Naming
    "scripts": {                
        "test": "jest"           // Every time that we put "npm run test" in the terminal, we have decided that "jest" will be run
        "start": "node index.js" // Instead of typing node index.js every time that we want to check the output,
                                 // we can add this line to the scripts and by adding "npm start" (without "run") 
                                 // we will have the same impact. Take note that the main scripts such as start, stop,
                                 // restart, install, version or test do not require run command
    },
    "dependencies": {            // In this spot, we will append all the external modules that are needed to be imported by someone who, 
                                 // for example, has cloned the repository and to run properly has to add some external libraries or modules
                                 // In this case, this project will be implemented if "jest" is imported, but, if we import jest, the node_modules
                                 // folder will be created. However, we don't want to add this folder in the github repository, therefore,
                                 // be add this folder in the .gitignore and like this we will not overweight the size of the project. 
                                 // Only by scripting "npm i" all the modules in "dependencies" will be initialized
        "jest": "^29.5.0"
    }
}


```js
