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
