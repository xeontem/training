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
