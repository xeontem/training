/*-------------------- Delegation -----------------------*/

document.body.innerHTML = '';
let divWrapper = document.createElement('div');
divWrapper.style.background = 'green';
divWrapper.style.display = 'flex';
divWrapper.addEventListener('click', function(e, i) {
    console.dir(e.target);
    console.dir(this.children[e.target.id]);
    if(e.target.id == this.children[e.target.id].id) console.log('pressed on div:' + e.target.id);
});
for(let i = 0; i < 10; i++) {
    let div = document.createElement('div');
    div.id = i;
    div.style.width = '30px';
    div.style.height = '30px';
    div.style.background = 'red';
    div.style.border = '1px solid black';
    div.style.margin = '10px';
    divWrapper.appendChild(div);
}
document.body.appendChild(divWrapper);

/*----------------------- My Bind -----------------------*/

console.log('--------- My Bind ----------------- ');

Function.prototype.myBind = function(cont, arg) {
    let func = this;
    return function() {
        let argees = [].slice.call(arguments);
        argees.unshift(arg);
        return func.apply(cont, argees);
    }
}

function sum(a, b) {
    return a + b;
}

let plusThree = sum.bind(null, 3);
let myBindPlusThree = sum.myBind(null, 3);
console.log('bind: ', plusThree(3));
console.log('myBind: ', myBindPlusThree(3));

/*-------------------- My New -----------------------*/

console.log('--------- My New ----------------- ');
function myNew(func, ...args) {
    let instance = Object.create(func.prototype);
    func.apply(instance, args);
    return instance;
}

let Animal = function(name) {
    this.name = name;
    this.run = function() {
        console.log('i can run');
    }
}
Animal.prototype.fly = function() {
    console.log('i can fly');
}

let Myrabbit = myNew(Animal, 'rabbit');
let NewRabbit = new Animal('rabbit');
console.dir(NewRabbit);
console.dir(Myrabbit)

/*-------------------- MyObjectCreate -----------------------*/

console.log('--------- MyObjectCreate ----------------- ');
Object.prototype.myCreate = function(proto) {
    let Object = function(){};
    Object.prototype = proto;
    let obj = new Object();
    return obj;
}

let protoObj = {
    name: 'vasa',
    surname: 'petrov'
}

let vasaMyCreated = Object.myCreate(protoObj);
let vasaObjectCreated =Object.create(protoObj);
console.dir(vasaObjectCreated);
console.dir(vasaMyCreated);

/*------------------------- inheritance ----------------------*/

console.log('------------------------- inheritance ----------------------')
let Animal1 = function(name) {
    this.name = name;
    this.run = function() {
        console.log('i can run');
    }
}
Animal1.prototype.jump = function() {
    console.log('i can jump');
}

let Rabbit1 = function(name) {
    Animal1.call(this, name);
    this.lie = function() {
        console.log('i can lie');
    };
}
Rabbit1.prototype = Animal1.prototype;
Rabbit1.prototype.fly = function() {
    console.log('i can fly');
}

let inheritedRabbit = new Rabbit1('rabbit');

console.dir(inheritedRabbit);

/*----------- quickSort --------------------*/
console.log('----------- quickSort --------------------');

var quicksort = function(array) {
    if(array.length <= 1) return array;
    var swapPos = Math.floor((array.length - 1)/2);
    var swapValue = array[swapPos];
    var left = [];
    var right = [];
    array = array.slice(0, swapPos).concat(array.slice(swapPos + 1));
    for(var i = 0; i < array.length; i++) {
        if(array[i] < swapValue) left.push(array[i]);
        else right.push(array[i]);
    }
    return (quicksort(left)).concat([swapValue], quicksort(right));
}

quicksort([2,9,12,6,3,1,7]);
/*----------- Cookies --------------------*/
console.log('----------- Cookies --------------------');

let obj = {};
document.cookie.split('; ').map(cookie => {
    let eq = cookie.indexOf('=');
	let key = cookie.slice(0, eq);
	let value = cookie.slice(eq+1);
	obj[key] = value;
})
console.dir(obj)
